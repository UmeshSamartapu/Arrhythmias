

### VR setup

---

### 1. Change the Django "Allowed Hosts"

By default, Django blocks any connection that isn't `localhost`. You must tell it to allow your local IP.

1. Open `cube_project/settings.py`.
2. Find the `ALLOWED_HOSTS` line and change it to:
```python
ALLOWED_HOSTS = ['*']  # This allows any device on your Wi-Fi to connect

```



### 2. Run the Server on your Local IP

If you just run `python manage.py runserver`, it only listens to your PC. You need to tell it to listen to the whole network.

1. Find your PC's IP address (Open Terminal, type `ipconfig` on Windows or `ifconfig` on Mac). Look for **IPv4 Address** (e.g., `192.168.1.15`).
2. Start your server like this:
```bash
python manage.py runserver 0.0.0.0:8000

```


*Note: `0.0.0.0` tells Django to broadcast to your entire local network.*

### 3. Check your Windows Firewall

Sometimes Windows blocks incoming connections to Python.

1. Go to **Search** > type **"Allow an app through Windows Firewall"**.
2. Find **python.exe** and make sure both **Private** and **Public** are checked.

### 4. The "HTTPS" Problem (Crucial for AR)

**This is the most common reason the AR button disappears.**
Mobile browsers (Chrome/Safari) often disable AR features unless the site is **Secure (HTTPS)**. Since you are running a local development server (`http`), the phone thinks it's unsafe.

**The Fixes:**

* **For Android (Chrome):** Open Chrome on your phone, go to `chrome://flags`, search for **"unsafely-treat-insecure-origin-as-secure"**, and add `http://192.168.1.XX:8000` (your PC IP) to the list. Enable it and relaunch.
* **The Professional Way (Ngrok):** This creates a temporary "Secure HTTPS Tunnel" to your PC.
1. Download [Ngrok](https://ngrok.com/).
2. In a new terminal, run: `ngrok http 8000`.
3. Ngrok will give you an `https://...` link. Open **that** link on your phone. AR will work immediately because it provides a valid SSL certificate.



---

### 5. Verify the AR Model Setup

Ensure your `<model-viewer>` tag in `index.html` includes the `ar` attribute and the `src` is correct:

```html
<model-viewer 
    src="{% static 'models/glowing_cube.glb' %}" 
    ar 
    ar-modes="webxr scene-viewer quick-look" 
    camera-controls>
</model-viewer>

```

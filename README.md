# firebase-ui
Polymer implementation of FirebaseUI for web

### Development
Use [polyserve](https://github.com/PolymerLabs/polyserve) to spin up the development page.

### Firebase Authentication Domains
Firebase auth requires whitelisting domains, but it doesn't let us add ports to domains. So it may be helpful to create a development domain and forward it to the proper localhost port.

- Go to your [Firebase console](https://console.firebase.google.com/)
- Select your project
- Click the Auth tab on the left nav
- Click the Sign In Method tab across the top nav
- Add an OAuth redirect domain. You can't add localhost:8080, because ports don't work with this yet, so do something like firebase-ui.dev
- Edit ```/etc/hosts``` for your local environment. Make a loopback entry in your hosts file like ```127.0.0.1  firebase-ui.dev```. This will cause your local machine to proxy firebase-ui.dev to your localhost. But you can't add ports to loopbacks like this, so proceed to the next step.
- Create a proxy server to forward firebase-ui.dev, or whatever imaginary domain you used, back to localhost:8080. I use nginx with the below config, but there must be a hundred different ways to do this.

```
server {
	listen 80;
	server_name firebase-ui.dev;

	location ~ {
		proxy_pass http://localhost:8080;
	}
}
```
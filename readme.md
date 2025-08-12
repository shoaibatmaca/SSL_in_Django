# Django Local HTTPS Setup (Development Only)

This guide explains how to enable **HTTPS** for your Django project locally using a **self-signed SSL certificate** and `django-extensions`.

> **Note:** This setup is for development and testing only.  
> Do not use self-signed certificates in production.

---

## Install Required Packages

Run the following command inside your virtual environment:

```bash
pip install django django-extensions Werkzeug pyOpenSSL
```

Add django-extensions to Installed Apps

```bash
INSTALLED_APPS = [
    # Django default apps
    'django.contrib.admin',
       ---
    # Add this for local HTTPS
    'django_extensions',
]
```

---

Now generate self-signed certificate for HTTPS.

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem
```

When prompted:
For Common Name (CN) enter: 127.0.0.1
Other fields (Country, State, etc.) can be skipped or filled with any value.
This will generate two files:
cert.pem → SSL certificate
key.pem → Private key

---

```bash
python manage.py runserver_plus --cert-file cert.pem --key-file key.pem
```

---

Do you want me to also **add a short "Troubleshooting" section** to this README so if the site doesn’t open, users know what to check? That would make it more complete.

---
layout: post
title:  "Working with Cryptography in Python"
date:   2021-10-27 20:30:43 -0300
categories: python api
---


In the last few days, I have been working with Python. I have never worked with it earlier. So, a feature that I need to develop involves cryptography. But, the project I working on today is already an implementation in Java, then my job was to migrate Java to Python. I enjoy the experience of programming in Python, until why I only programming in a compiled language like Kotlin and Java. The style is so strange when you want to discover what methods are available in the programming language, and I think that discovering material how something works is harder than Java.

```python
import base64
import logging
from cryptography import x509
from cryptography.hazmat.primitives._serialization import Encoding
from hashlib import sha256
from urllib.parse import unquote


UTF_8 = 'UTF-8'
PADDING_URL = '='


class CertificateManager:

    def __init__(self, certificate):
        self.raw_certificate = certificate

    def generate_safe_url(self):
        try:

            # the certificate come here encoded
            url = unquote(self.raw_certificate)

            # load certificate
            cert = x509.load_pem_x509_certificate(url.encode('UTF-8'))

            # prepare digest
            mDigest = sha256()
            pem_data = cert.public_bytes(Encoding.DER)
            mDigest.update(pem_data)

            # encode on url safe
            url_safe_encoded_bytes = base64.urlsafe_b64encode(mDigest.digest())
            url_safe_without_padding = url_safe_encoded_bytes.decode(UTF_8).rstrip(PADDING_URL)

            return url_safe_without_padding

        except Exception as e:
            logging.error(
                'M=get_certificate_hash MSG=error-on-generate-safe-url error={error}.'.format(error=e))
            return None
```

The source code above shows the implementation. Python does have a native way to deal with certificates, so we need to use the third party library called **cryptography**, for lucky is easy work with them.

The input of the class is an encoded PEM certificate.
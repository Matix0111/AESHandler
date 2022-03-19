# AESHandler
AESHandler is a package that makes AES encryption and decryption easy.

# Usage
```python
import aeshandler

# The aeshandler module comes with a key_from_password() method in the AESHandler class.
# This method takes in a password, and runs a KDF function to create a key.
password = b'Password1234!'
crypto_tuple = aeshandler.AESHandler.key_from_password(password) # Default KDF is Bcrypt
'''
OUTPUT: (b'password1234!', b'he0bB3t4OZtAqjQlv77QOq1LHg6wSeD9rNskEiAV5LsMYGDXS8rBkEPLDIeQNshf', b'\x14\xe8\xf0\xcf\xf1\x16\x9d\xb6J\x9b\xc0\xfe\xed\xd7\xe9\xd0\x82\x10scip\xea|L&\x81\xacH\xa8O\x0e')
First element is the password, second element is the salt used with the KDF, third element is the derived key.
'''
crypto_key = crypto_tuple[-1] # b'\x14\xe8\xf0\xcf\xf1\x16\x9d\xb6J\x9b\xc0\xfe\xed\xd7\xe9\xd0\x82\x10scip\xea|L&\x81\xacH\xa8O\x0e'

'''
AESHandler supports all AES modes. Such as CBC, CFB, XTS, and so on.
Using CBC in this instance.
This may require the padding=True argument for PKCS7 padding.
encoding=aeshandler.ENCODINGS.BASE64 will return ciphertexts in base64 format.
encoding=aeshandler.ENCODINGS.HEX will return ciphertexts in hex format.
encoding=aeshandler.ENCODINGS.RAW will return ciphertexts in raw format. (this is the default)
'''
a = aeshandler.AESHandler(crypto_key, aeshandler.modes.CBC, padding=True, encoding=aeshandler.ENCODINGS.BASE64)
ciphertext = a.encrypt('Hello!') # M4ENqqe0m0ys4a7e1fnWHtJD+DbGNY5ckfbJBShxkJ0=
print(ciphertext)
print(a.decrypt(ciphertext)) # b'Hello!'
```

# Security API
[[System Security Challenge 3 Report|PIN verification]]
# PKCS\#11
Standard API to cryptographic devices.
Keys have **attributes** that are references via **handles**.
Sensitive keys should never be accessible (as plaintext) outside the crypto device, every operation must be inside the device.
If an attacker can extract those keys (e.g. via a compromised host) then the attacker can clone the device.
## Problems
PKCS\#11 is broken.
There have been attempts to fix the API but they're not compliant with the standard. Those fix include *offline key management* and **no key wrap**.
Some simple mitigation include monitoring/filtering API calls.
Another possible fix is to add the **wrap_with_trusted** attribute where keys can be wrapped only by trusted keys. But how are trusted keys generated or managed? And what happens if a trusted key is compromised?
### Cloud HSM
HSM hardware accessible online
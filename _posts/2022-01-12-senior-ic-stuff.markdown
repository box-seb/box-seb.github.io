---
layout: post
title:  "Senior IC stuff"
date:   2022-01-12 19:03:04 +1200
---

Smart stuff about senior IC engineering track.

(The secret to getting to the Staff+ level? Leverage)[https://leaddev.com/career-paths-progression-promotion/secret-getting-staff-level-leverage]

(A Readme for Staff Engineers)[https://medium.com/criteo-engineering/a-readme-for-staff-engineers-cbe0d39fa5f2]

(StaffEng)[https://staffeng.com/]



FIDO alliance inititated for prevent data breaches, due to password 
- asynchronouse auth based on private/public key
- passkey

Credentials not stored on the server
- removeing it removes credential stealing

WebAuthN SDKs
- roaming authenticator, usb device (something you can detach unplug from the physical device), used to first time use to auth new device, bootstrapping, 
- platform authenticator

Adoption
- FIDO is to replace passwords and OTPS
- Support in enterprise
- Microsoft build in support to all its platforms
- Consumers progress is there, developers can use JS asks to implement logins without passwords
- UX guidlines how to deploy FIDO

https://identityunlocked.auth0.com/public/49/Identity%2C-Unlocked.--bed7fada/23fe1152

UX guidlines
https://fidoalliance.org/ux-guidelines/

Platforms:
- Microsoft, Google, Apple
- Vast majority users use those platforms
- That adds up to adoption

Recovery
- Multiple devices in ecosystem
- Adding new devices


Multidevice credential model
- Adding new devices
- Loosing devices

Platforms help user localize credentials
Developrs no need to worry where are the credentials
Extendign the definition of platform to provide credentials

Hardware security keys are going to stay

How we can help it make a reality
- This is a journey
- Next 12 months will be giant dev trial
- Realistically in 24 months we can see relying parties remove passwords


Apple:
- https://support.apple.com/en-us/HT213305
- On Apple devices with Touch ID or Face ID available, they can be used to authorize use of the passkey, which then authenticates the user to the app or website.
- Passkeys sync across a user's devices using iCloud Keychain.
- To sign in for the first time on any new device, two pieces of information are required—the Apple ID password and a six-digit verification code that's displayed on the user's trusted devices or sent to a trusted phone number.


Google:
- https://developers.google.com/identity/fido
- On Android, we aim to have passkey support available to developers towards the end of 2022.
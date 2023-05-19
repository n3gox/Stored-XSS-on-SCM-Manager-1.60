# Stored-XSS-on-SCM-Manager-1.60

## Summary

A vulnerability is discovered in the SCM Manager 1.2 <= 1.60 version that is vulnerable to inject javascript code in specific fields that allows a Stored XSS.

This Proof of Concept is maded in a local environment deploying a SCM Manager 1.60 using docker

## Installing SCM Manager 1.60

Copy and paste this bash script in a script.sh file, bring execution permissions and execute the file:

```
#!/bin/bash

mkdir /var/lib/scm
chown 1000:1000 /var/lib/scm
docker run -v /var/lib/scm:/var/lib/scm -p 8080:8080 sdorra/scm-manager

```
The script is created by sdorra, here is the oficial link:
https://bitbucket.org/sdorra/docker-scm-manager/src/master/

NOTE: You need to have installed docker previously.

Once you have installed the SCM Manager 1.60, it will request you a username and a password:

Username : scmadmin
Password: scmadmin

Proof of Concept:

![PoC1](https://github.com/n3gox/Stored-XSS-on-SCM-Manager-1.60/assets/85514196/06faf448-e332-4396-b4b2-8ee935304f97)

2- Create a new repository with whatever type but in the **Description** field is the vulnerable, so let's inject the payload and it will be triggered:

![PoC2](https://github.com/n3gox/Stored-XSS-on-SCM-Manager-1.60/assets/85514196/71426354-aadd-4181-bdcd-6fa709e7ebc2)

3- Create a new user and the specific vulnerable field is **Display Name**, so inject the payload introduced before:

![PoC3](https://github.com/n3gox/Stored-XSS-on-SCM-Manager-1.60/assets/85514196/5c12e35a-320e-4072-a46e-2f6b5c77dc05)
![PoC4](https://github.com/n3gox/Stored-XSS-on-SCM-Manager-1.60/assets/85514196/4487a4d2-5caf-4c7e-9d71-ce437598b25b)

4- Create a new group and the specific vulnerable field is **Description**, so inject our payload:

![PoC5](https://github.com/n3gox/Stored-XSS-on-SCM-Manager-1.60/assets/85514196/041a029b-6c05-46a9-9284-879cc46aa85f)

USED PAYLOAD: ``` <img src=x onerror=alert(1)> ```

## FIX
New Versions of the SCM Manager are fixed.

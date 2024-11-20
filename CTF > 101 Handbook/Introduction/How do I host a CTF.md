# How do I run a CTF?

> "Is it really a CTF if you don't solve the infrastructure problem in the 24 hours before the competition?"

## Before you start
- Consider a few of the following before starting a CTF.
	- How many people will play in my CTF?
	- What type of challenges do I want to write?
	- How do you want to host your challenges?
	- What is my budget?


## **Open Source Frameworks**
- CTFd
	- CTFd makes it easy to spin up an instance able to support a CTF at any time. Starting a local server is as easy as:

```
docker run -p 8000:8000 -it ctfd/ctfd #
```

- kCTF
	- kCTF is a framework written by Google built on Kubernetes. It has built in load balancing at the platform level.
- rCTF
	- Written by the redPWN CTF team, rCTF has a separate CI/CD module for supporting challenge deployment as well.

```
curl https://get.rctf.redpwn.net | sh
```


## **Paid CTF Hosting**
- CTFd Enterprise
	- Three-tiered pricing service with hosting services and on-call support.
	- Supports professional workshops generally reserved for industry security teams exercises.
- Hack The Box CTF
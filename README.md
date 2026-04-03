# Important: Unauthorized access to our vantage6 image registry

## 2 April 2026 - 10:15
Dear community members,

We are hereby reporting unauthorized access to the community Harbor image registry. A malicious user has gained admin access to the application and injected a malicious binary into some of the images. This malicious binary is a malware downloader. In other words, once this application is started it will download a malicious application.

The attacker seems not to have targeted the vantage6 registry specifically, but rather was attacking diverse harbor registries. This makes it less likely the attacker is after sensitive data. Also, fortunately, NO node images have been affected with the exception of the unreleased version 5 images. This means that production nodes should have functioned as normal.

The most important images that are affected are:

- infrastructure/server:cotopaxi - affected since 24/3, containing version 4.14
- version 5 infrastructure images tagged with Uluru

A complete of overview of all affected images is in the attachment. Also, the malicious cotopaxi server image does not start (see issue [BUG] Server 4.14.0 (cotopaxi): /wrapper.sh permission denied on container start · Issue #2578 · vantage6/vantage6).

We expect that there is only an impact for those of you who have run the version 5 beta images. However, we encourage you to investigate if any of the affected images might have run in your projects. Note that also many algorithm images have been affected, but since algorithms in vantage6 lack an internet connection, we do not expect that the malware download succeeded. However, note that the image with the downloader may still be present.

After discovering the presence of malicious images, we shutdown the harbor2 service yesterday evening. We will get back to you when the service will be resumed.

Apart from investigating the impact to your project, we would advise you to purge any affected vantage6 images.

We will keep you informed of any new updates.

Kind regards,
The vantage6 team

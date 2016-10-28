---
layout: post
title: "GANZ PixelPro secondary RTSP stream"
date: 2014-04-01 15:38:55 +0200
comments: true
categories: 
---
GANZ PixelPro ZN-MB243M IP surveillance Camera supports two live streams (RTSP or MJPEG), that can be enabled and configured directly from control web panel.
However the manual doesn't mention about direct stream URL's.

The first one is quite easy to find on the Internet webpages with list of available camera streams (like [1](http://www.ispyconnect.com/sources.aspx#info) or [2](http://www.bluecherrydvr.com/2012/01/technical-information-list-of-mjpeg-and-rtsp-paths-for-network-cameras/)):

```
rtsp://IP:554/gnz_media/main
```

But the second stream is a MYSTERY! I [found only one google result](http://www.google.pl/search?q=%22gnz_media%2Fsecond%22) - march 2014 (+few autocrawlers) with it. It is an Excel file on some russian page: <http://freudgroup.ru/userfiles/ipcameras.xls>

```
rtsp://IP:554/gnz_media/second
```

To be exact there is a third MJPEG stream, that is displayed on the Live Preview page, but it only accepts one connection at a time.

```
http://ADMIN:1234@IP/cgi-bin/jpg.fcgi?count=-1
```

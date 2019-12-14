---
title: "Nginx 로 다중 서버 로드 밸런싱"
header:
  image: https://live.staticflickr.com/8084/8396909762_813a2b1829_h.jpg
categories:
  - load balancing
tags:
  - nginx
  - was
toc: true
toc_label: "목차"
toc_icon: "heart"
toc_sticky: true
---

Proxying HTTP Traffic to a Group of Servers

# Nginx 설치
- 우분투에서 nginx 최신버전 설치하는 방법
    - https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#installing-a-prebuilt-ubuntu-package-from-the-official-nginx-repository

```console
$ sudo wget https://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key

$ sudo vi /etc/apt/sources.list
# vi 로 아래 두 라인 추가
deb https://nginx.org/packages/ubuntu/ xenial nginx
deb-src https://nginx.org/packages/ubuntu/ xenial nginx

$ sudo apt-get remove nginx-common
$ sudo apt-get update
$ sudo apt-get install nginx
$ sudo nginx

# nginx 작동 테스트
$ curl -I 127.0.0.1
```

# Docker 로 테스트 was 2개 띄우기


# Nginx 로 로드 밸런싱

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/#overview


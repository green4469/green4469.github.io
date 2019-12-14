---
title: "docker 개념 입문"
header:
  image: https://miro.medium.com/max/1200/1*Y5hFnMpixqzmWXOp4EQGUQ.jpeg
categories:
  - docker
tags:
  - container
  - deployment
  - virtualization
toc: true
toc_label: "목차"
toc_icon: "heart"
toc_sticky: true
---

# 도커?

> Docker is an open platform for developing, shipping, and running applications. Docker enables you to **separate your applications from your infrastructure so you can deliver software quickly.** - [Docker official docs](https://docs.docker.com/engine/docker-overview/)

애플리케이션을 인프라로부터 추상화해 코드의 배포를 쉽게 만들어준다.

# 도커 컨테이너
컨테이너는 애플리케이션을 실행하기 위한 독립된 환경이다. 다음과 같은 특징을 갖는다.
- 컨테이너는 호스트로부터 독립된 환경을 갖는다. 호스트 입장에서 컨테이너는 하나의 프로세스에 불과하다.
- 컨테이너는 VM 을 필요로하지 않고, 호스트의 커널을 직접 사용한다.
    - 직접 커널을 사용하기때문에 VM 에 비하여 성능이 훨씬 좋다.

# 도커 엔진
도커 엔진은 도커 객체들(이미지, 컨테이너, 네트워크, 데이터 볼륨)의 서버 역할을 하는 어플리케이션이다.
![docker-architecture](https://docs.docker.com/engine/images/engine-components-flow.png)

# 도커 컨테이너 띄우기 (was)

하나의 서버에 여러 컨테이너를 띄우고 싶다면 어떻게 해야할까? 예를 들어 MySQL 데이터베이스 서버 컨테이너, Tomcat WAS 컨테이너, Nginx 로드밸런서 건테이너가 있다면? Tomcat WAS 컨테이너가 하나가 아니라 여러개라면? 

각각의 컨테이너를 생성하고, 실행하고, 제거하는 작업은 docker-CLI 로 일일이 타이핑하기엔 너무 귀찮고 반복적인 작업이다. 이를 해결하기위해 존재하는 것이 docker-compose 이다.

docker-compose 는 도커와 별도로 설치해야하는 프로그램이다. [여기](https://docs.docker.com/compose/install/)서 OS별 설치 방법을 알아볼 수 있다.

[docker-compose](https://docs.docker.com/compose/) 은 한 호스트 내에서 여러 컨테이너를 띄울 때 사용한다. 각 컨테이너들은 독립된 환경을 한 호스트(컴퓨터) 위에서 제공받는다.


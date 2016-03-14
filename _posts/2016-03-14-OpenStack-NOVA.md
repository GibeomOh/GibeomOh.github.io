---
layout: post
title: OpenStack에 대해 알아보자
date: 2016-03-14
tags: OpenStack
category: thinking
---

## Summary
![OpenStack](https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/The_OpenStack_logo.svg/270px-The_OpenStack_logo.svg.png)
OpenStack에 대해 알아보자!

## OpenStack..?
  오픈스택(OpenStack)은 IaaS 형태의 클라우드 컴퓨팅 오픈 소스 프로젝트를 말한다. 2012년 창설된 비영리 단체인 OpenStack Foundation에서 유지, 보수하고 있으며 아파치 라이선스하에 배포된다. AMD, 인텔, 캐노니컬, 수세 리눅스, 레드햇, 시스코 시스템즈, 델, HP, IBM, NEC, VM웨어, 야후! 등 150개 이상의 회사가 이 프로젝트에 참가하고 있으며, 주로 리눅스 기반으로 운용과 개발이 이루어진다. 프로세싱, 저장공간, 네트워킹의 가용자원을 제어하는 목적의 여러개의 하위 프로젝트로 이루어져 있다.


## 한 번 더 OpenStack이란..?
[OpenStack](http://openstack.org)에 나와있는 그림을 살펴보자.
![](http://www.openstack.org/themes/openstack/images/software/openstack-software-diagram.png)
OpenStack 사이트의 원문을 해석해보면, OpenStack은 데이터 센터를 통해 컴퓨팅, 스토리지 및 네트워킹 자원의 풀을 데어하는 클라우드 운영 시스템이고, Dashboard를 이용하여 모든 웹 인터페이스를 통해 제공하는 리소스에 대해 자신의 사용자 권한을 부여하면서 관리자가 제어 할 수 있습니다.. 라고 말한다.
  즉, 간단히 설명하면 클라우드 형태의 가상화 프로그램인데, VMware가 유료라면 Openstack은 무료 프로그램이라고 생각하면 된다.

  
## OpenStack의 구성 요소
![](http://cfile8.uf.tistory.com/image/230F033656446B712FC2E7)


- SWIFT: 사용자별로 저장공간을 나눠주는 스토리지 서비스(오브젝트 서비스)를 말한다. Swift-proxy, account, container, object로 구분된다. 디스크 드라이브의 위치로 파일을 참조한다는 기존의 생각과는 달리 개발자는 파일을 참조하는 고유 식별자를 이용하여 정보 저장 위치를 OpenStack이 결정하도록 할 수 있다. 개발자는 소프트웨어 뒤에 단일 시스템에서 용량에 대한 걱정을 하지 않아도 되며 확장에 용이하다는 장점이 있습니다. 또한 데이터가 서버나 네트워크의 장애시에도 자동으로 백업이 되는 장점이 있다.
- KEYSTONE: OpenStack에서 제공하는 모든 서비스에 대한 인증 서비스를 제공한다. KEYSTONE 등록된 사용자들만 OpenStack을 사용할 수 있다.
- NOVA: 인스턴스의 생성/삭제/메모리 관리를 수행하는 요소를 말한다. 여기서 인스턴스는 흔히 알고 있는 각각의 가상 컴퓨터를 말한다. 
- NEUTRON: 인스턴스의 네트워크를 담당하는 부분
- CINDER: Block Storage 를 관리하는 요소. 각각의 인스턴스의 저장소를 관리하는 것을 말한다.
- GLANCE: 인스턴스의 운영체제에 해당하는 이미지를 관리한다. GLANCE에 있는 이미지를 이용하여 사용자들은 OS를 설치할 수 있다.


## 그 중 NOVA에 대해 알아보자
nova는 openstack 초창기 모델부터 있었던 openstack의 필수 구성요소 중 하나다. (빨간색으로 표시된 부분이 nova의 영향을 받는 부분)
![](http://postfiles13.naver.net/20150805_156/junhyung17_1438753806687dBA0o_PNG/%B0%B3%B3%E4%B5%B5.png?type=w2)


 1. NOVA는 Dashboard나 커맨드 라인 명령어가 호출하는 nova-api로부터 시작된다.
 
 2. nova-api는 Queue를 통해 nova-compute에 인스턴스를 생성하는 명령어를 전달한다.
 
 3. nova-compute는 하이퍼바이저 라이브러리를 통해 하이퍼바이저에게 인스턴스를 생성하라는 명령어를 전달한다.
 
 4. 하이퍼바이저는 인스턴스를 생성한다.
 
 5. 생성된 인스턴스는 nova-console을 통해 사용자가 접근할 수 있게 된다.
 
 
### nova-api란?
- Nova에서 중추적인 역할을 수행하는 데몬 
- Nova-api는 openstack API 또는 EC2 API 쿼리에 다른 요소들과 연결이 가능한 매개체를 제공 
- 인스턴스를 실행하는 것과 같은 대부분의 조직화 활동을 개시되게 하고 몇몇의 정책을 실행
![](http://postfiles6.naver.net/20150805_261/junhyung17_1438753819643yKdvi_PNG/nova-api.png?type=w2)


### nova-scheduler란?
- 대기열로 부터 VM 인스턴스 요청을 수행하고 nova가 적정한 위치에서 실행되도록 결정
- Nova-schedule은 스케쥴링을 위한 알고리즘을 운영할 수 있는 구조를 구현
![](http://postfiles7.naver.net/20150805_166/junhyung17_1438753831278PpW7P_JPEG/nova-scheduler.jpg?type=w2)


### nova-compute란?
- Nova-compute는 VM 인스턴스를 생성하고 제거하는 역할을 하는 데몬
- 대기열에서 작업을 수락하고 데이터베이스의 상태를 업데이트 하는 동안 KVM 인스턴스 시작과 같은 시스템 일련의 명령을 수행
 
 
### nova-conductor란?
- Nova-conductor는 grizzly 버전부터 생긴 모듈로 nova-compute와 데이터베이스 사이에서 상호작용을 조절하는 역할 수행
- Nova-compute에 의해 만들어진 클라우드 데이터베이스에 직접 접근하여 제거하는 것을 목표로 함


### nova-volume이란?
- Nova-volume은 인스턴스들을 계산하기 위해 지속적인 볼륨들의 창조, 결합, 분리를 관리
- Nova-volume은 다양한 디스크 유형의 볼륨들을 사용할 수 있음
![](http://postfiles6.naver.net/20150805_165/junhyung17_1438753842849gnDAN_JPEG/nova-volume.jpg?type=w2)


### nova-network란?
- Nova-network는 대기열로 부터 네트워킹 업무들을 수행
- 네트워킹 업무를 수행하면서 브리지 인터페이스를 셋팅하거나 방화벽 정책을 변경하는 등의 네트워크를 다루기 위한 작업을 수행함 


### nova-dhcpbridge란?
- Nova-dhcpbridge는 데이터베이스 안에 있는 dnsmasq dhcp-script 기능을 사용함으로써 IP 주소를 임대하고 기록하는 역할을 수행


### console 관련 구성 요소들
- Nova-consoleauth
- Nova-novncproxy
- Nova-xvpnvncproxy
- Nova-cert
![](http://postfiles1.naver.net/20150805_256/junhyung17_1438753853645CV4I0_JPEG/console.jpg?type=w2)


출처
---
[openstack 구성 요소 알아보기 - Nova에 대하여](http://blog.naver.com/junhyung17/220258477631)

[openstack](http://www.openstack.org/)

[Nalee의 IT이야기](http://naleejang.tistory.com/101)

[wiki: HypervisorSupportMatrix](https://wiki.openstack.org/wiki/HypervisorSupportMatrix)
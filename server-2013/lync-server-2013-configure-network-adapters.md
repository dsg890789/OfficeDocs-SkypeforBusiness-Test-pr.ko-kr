﻿---
title: 'Lync Server 2013: 네트워크 어댑터 구성'
TOCTitle: 네트워크 어댑터 구성
ms:assetid: 6519ed80-020f-47a3-851c-03dea5eac5d9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg429707(v=OCS.15)
ms:contentKeyID: 49303851
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013에서 네트워크 어댑터 구성

 

_**마지막으로 수정된 항목:** 2013-11-07_

외부 네트워크 어댑터에는 한 개 또는 그 이상의 IP 주소를 지정해야 하며 내부 네트워크 어댑터에는 최소 한 개의 IP 주소를 지정해야 합니다.

다음 절차에서 Forefront Threat Management Gateway(TMG) 2010 또는 Internet Information Server Application Request Routing을 실행하는 서버에는 두 개의 네트워크 어댑터가 있습니다.

  - 일반적으로 인터넷을 통해 웹 사이트에 연결을 시도하는 클라이언트에 대한 공용 또는 외부 네트워크 어댑터

  - 웹 서비스를 호스트하며 Lync Server을 실행하는 내부 서버에 대한 개인 또는 내부 네트워크 인터페이스


> [!IMPORTANT]
> 에지 서버와 비슷하게 외부 네트워크 어댑터에서만 기본 게이트웨이를 설정합니다. 기본 게이트웨이는 트래픽을 인터넷으로 전송하는 라우터 또는 외부 연결 방화벽의 IP 주소입니다. 역방향 프록시에서 내부 연결 네트워크 어댑터로 이동하는 트래픽의 경우 웹 게시 규칙으로 참조되는 서버가 포함된 모든 서브넷에 대해 영구적인 정적 경로(예: Windows 서버의 Route 명령)를 사용해야 합니다. 영구적인 경로를 설정해도 컴퓨터가 라우터가 되지는 않습니다. IP 전달이 설정되지 않으면 컴퓨터는 다른 네트워크를 대상으로 지정된 특정 트래픽을 해당 인터페이스로 연결하는 역할만 합니다. 이 과정에서 기본적으로 두 개의 게이트웨이가 설정되는데, 하나는 외부 네트워크를 가리키는 기본 게이트웨이이고 다른 하나는 내부 인터페이스를 대상으로 지정된 트래픽과 라우터 또는 다른 네트워크의 트래픽을 위한 게이트웨이입니다.<BR>하지만 네트워크 라우터가 경로를 요약하도록 구성된 경우 모든 서브넷에 대해 반드시 영구 경로를 만들 필요는 없습니다. 라우터가 정의된 네트워크에 대한 영구 경로를 만들고 라우터를 기본 게이트웨이로 사용합니다. 네트워크 구성 방법이 확실하지 않고 어떤 영구 경로를 만들어야 하는지에 대한 지침이 필요하면 회사의 네트워크 엔지니어에게 문의하세요.<BR>역방향 프록시는 웹 게시 규칙에 사용되는 내부 디렉터 또는 프런트 엔드 서버 및 다음 홉 풀 FQDN에 대한 DNS 호스트(A) 레코드를 확인할 수 있어야 합니다. 에지 서버와 마찬가지로 보안상의 이유로 역방향 프록시 서버가 내부 네트워크에 있는 DNS 서버를 사용하도록 구성하지 않는 것이 좋습니다. 즉, DNS 서버를 경계에 배치해야 하거나 역방향 프록시에 이러한 각 FQDN을 서버의 내부 IP 주소로 확인하는 HOST 파일 항목이 있어야 합니다.



## 역방향 프록시 컴퓨터에 네트워크 어댑터 카드를 구성하려면

1.  역방향 프록시로 실행되는 Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2 서버에서 **시작** 을 클릭하고 **제어판** 을 가리킨 다음 **네트워크 및 공유 센터** 를 클릭한 후 **어댑터 설정 변경** 을 클릭하여 **어댑터 설정 변경** 을 엽니다.

2.  외부 인터페이스에 사용할 외부 네트워크 연결을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.

3.  **속성** 페이지에서 **네트워킹** 탭을 클릭하고 **이 연결에 다음 항목 사용** 목록에서 **인터넷 프로토콜 버전 4(TCP/IPv4)** 를 클릭한 다음 **속성** 을 클릭합니다.

4.  **인터넷 프로토콜(TCP/IP) 속성** 페이지에서 네트워크 어댑터를 연결할 네트워크 서브넷에 맞게 IP 주소를 구성합니다.
    

    > [!NOTE]
    > HTTPS/TCP/443을 사용하는 다른 응용 프로그램에서 Outlook Web Access 게시 등의 용도로 역방향 프록시를 이미 사용하고 있으면 기존 규칙 및 웹 수신기를 간섭하지 않고 HTTPS/TCP/443에서 Lync Server 2013 웹 서비스를 게시할 수 있도록 다른 IP 주소를 추가하거나, 기존 인증서를 주체 대체 이름에 새 외부 FQDN 이름을 추가하는 인증서로 바꿔야 합니다.



5.  **확인** 을 클릭한 다음 **확인** 을 클릭합니다.

6.  **네트워크 연결** 에서 내부 인터페이스에 사용할 내부 네트워크 연결을 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.

7.  3-5단계를 반복하여 내부 네트워크 연결을 구성합니다.


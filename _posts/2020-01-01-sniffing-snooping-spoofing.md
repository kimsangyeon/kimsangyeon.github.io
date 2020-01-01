---
layout: post
title: 'Sniffing Snooping spoofing'
categories: [network]
image: assets/images/banner/web.png
author: yeon
---

# Sniffing Snooping Spooping

네트워크 보안 공격중 이름이 비슷한 `sniffing` `snooping` `spoofing`에 대한 용어 정리를 해볼까합니다. 한번씩 읽고 항상 뭐가 뭐였지..? 하는 습관이 고쳐지길 바라며 :) <br>

<br><br>

## Sniffing

도청(Eavesdropping), 엿듣기(Wiretapping)라고 불리는 `sniffing`은 통신상에서 몰래 데이터를 획득하는 행위를 지칭합니다. 그리고 sniff는 '코를 킁킁거리다' '냄새를 맡다'로 네트워크상에서 패킷 교환을 엿듣고 훔쳐보는 행위라고도 합니다. <br>

<br>

원래의 `sniffing`은 네트워크를 분석하기 위한 합법적인 패킷 캡쳐도구를 지칭하기도 하였다고 합니다. 예로는 [WireShark](https://www.wireshark.org/)가 있으며 네트워크 트레픽 도청으로 패킷을 변경하지 않고 캡쳐하고 표시할 수 있습니다. <br>

<br><br>

## Snooping

`snooping`의 snoop은 '기웃거리다' '염탐하다'로 네트워크상의 떠도는 정보를 획득하는 행위를 말합니다. <br>
네트워크 상에서 `sniffing` `snooping` 두가지의 차이점은 `sniffing`은 몰래 데이터를 획득 할 때 사용되고 `snooping`은 합법적으로 청취하는 경우에 사용된다고 합니다. <br>

<br>

`snooping`의 예로는 `IGMP snooping`이 있으며 IGMP는 Internet Group Management Protocol의 약자로 Internet Protocol Multicast Group들의 멤버십을 관리하는 통신 규약입니다. `IGMP snooping`은 IGMP 트래픽을 감지하기 위한 것으로 스위치가 호스트와 라우터 간 IGMP 대화를 '청취'할 수 있도록 합니다. <br>

<br>

또 다른 예로 `DHCP snooping`이 있습니다. DHCP란 Dynamic Host Configuration Protocol의 약자로서, 호스트의 IP주소와 각종 TCP/IP 프로토콜의 기본 설정을 클라이언트에게 자동으로 제공해주는 프로토콜입니다. DHCP 지원 클라이언트는 네트워크 부팅과정에서 DHCP서버에 IP주소를 요청하고 얻을 수 있습니다. 여기서 `DHCP Snooping`이란 DHCP 서버를 보호하기 위해 사용하는 기능입니다. 이는 `DHCP spoofing`을 방어하기 위해 사용되며 DHCP 메시지의 내부까지 확인합니다.

<br><br>

## Spoofing

마지막으로 `spoofing`은 spoof '속이다'라는 뜻으로 승인받은 사용자인 것처럼 속여 시스템에 접근하는 것을 말합니다. <br>

<br>

`IP spoofing`은 IP 패킷의 송신측 주소를 위조사칭하거나 Mac address changer 등이 있습니다.

<br><br><br>

# IP 주소

## ARP 
컴퓨터와 컴퓨터 간의 통신은 흔히 IP 주소 기반으로 통신한다 알고 있지만
정확하게 얘기하면 IP 주소에서 ARP를 통해 MAC 주소를 찾아 MAC 주소를 기반으로 통신한다.

ARP란 IP 주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜이다.

ARP 를 통해 가상 주소인 IP 주소를 실제 주소인 MAC 주소로 변환한다. 이와 반대로 RARP를 통해
실제 주소인 MAC 주소를 가상 주소인 IP 주소로 변환하기도 한다.

![image](https://github.com/user-attachments/assets/9c54d1bc-42ae-4923-99cf-393ce5adc822)

장치 A가 ARP Request 브로드캐스트를 보내서 IP 주소인 141.23.56.3 에 해당하는 MAC 주소를 찾는다.
그러고 나서 해당 주소에 맞는 장치 B가 ARP Reply 유니캐스트를 통해 MAC 주소를 반환하는 과정을 거쳐
IP 주소에 마자는 MAC 주소를 찾게 된다.

- 브로드캐스트: 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전송되는 방식
- 유니캐스트: 고유주소로 식별된 하나의 네트워크 목적지에 1:1로 데이터를 전송하는 방식

### 홉바이홉 통신
IP 주소를 통해 통신하는 과정을 홉바이홉 통신이라 한다.
여기서 홉은 영어 뜻 자체로 건너뛰는 모습을 의미.
이는 통신망에서 각 패킷이 여러 개의 라우터를 건너가는 모습을 비유적으로 표현한 것으로, 수많은 서브네트워크 안에 있는
라우터의 라우팅 테이블 IP를 기반으로 패킷을 전달하고 전달해가면서 라우팅을 수행해서 최종 목적지까지 패킷을 전달한다.

![image](https://github.com/user-attachments/assets/b2c83e5f-cd02-4a8c-91c9-edb92f3ec13a)

즉 통신 장치에 있는 '라우팅 테이블'의 IP 를 통해 시작주소부터 시작해 다음 IP로 계속 이동하는 라우팅 과정을 거쳐 패킷이 최종 목적지까지 도달하는 통신을 말한다.

### 라우팅 테이블
라우팅 테이블은 송신지에서 수신지까지 도달하기 위해 사용되며 라우팅에 들어가 있는 목적지 정보들과 그 목적지로 가기 위한 방법이 들어있는 리스트를 뜻한다.
라우팅 테이블에는 게이트웨이와 모든 목적지에 대해 해당 목적지에 도달하기 위해 거쳐야 할 다음 라우터의 정보를 갖고 있다.

### 게이트웨이
게이트웨이는 서로 다른 통신망, 프로토콜을 사용해 네트워크 간의 통신을 가능하게 하는 관문 역할을 하는 컴퓨터와 소프트웨어를 두루 일컫는 용어다.
사용자는 인터넷에 접속하기 위해 수많은 톨게이트인 게이트웨이를 거쳐야 하며 게이트웨이는 서로 다른 네트워크 상 통신 프로토콜을 변환해주는 역할을 하기도 한다.

![image](https://github.com/user-attachments/assets/7782df8c-a5a3-47cd-a1c7-f2569366ffd2)

게이트웨이를 확인하는 방법은 라우팅 테이블을 통해 볼 수 있으며 라우팅 테이블은 윈도우 명령 프롬프트에서 netstat -r 명령어를 실행해 확인할 수 있다.
명령어를 실행하면 IPv4 경로 테이블, IPv6 경로 테이블이 있는데 이게 바로 라우팅 테이블이며 게이트웨이, 인터페이스 등이 나오는 걸 확인할 수 있다.

## IP 주소 체계
IP 주소는 IPv4 와 IPv6 으로 나뉜다. IPv4는 32비트를 8비트 단위로 점을 찍어 표기하고 123.45.67.89 같은 방식으로 IP 주소를 나타낸다.
IPv6은 64비트를 16비트 단위로 점 찍어 표기하며 2001:db8::ff00:42:9329 같은 방식으로 IP 주소를 나타낸다.

추세는 IPv6로 가고 있지만 현재 가장 많이 쓰이는 주소 체계는 IPv4이며 이후에 설명할 때도 IPv4를 기준으로 설명한다.

### 클래스 기반 할당 방식
IP 주소 체계는 과거를 거쳐 발전해오고 있으며 처음에는 A,B,C,D,E 다섯개의 클래스로 구분하는 클래스 할당 방식을 썼가.
앞에 있는 부분을 네트워크 주소, 뒤에 있는 부분을 컴퓨터에 부여하는 주소인 호스트 주소로 놓고 사용한다.

![image](https://github.com/user-attachments/assets/8eaf98a0-bbf4-4d78-9526-c6d55e29f621)

클래스 A,B,C는 일대일 통신으로 사용되고 클래스 D는 멀티캐스트 통신, 클래스 E는 앞으로 사용힐 예비용으로 쓰는 방식이다.
예를 들어 클래스 A는 0.0.0.0부터 127.255.255.255까지 범위를 갖는다

![image](https://github.com/user-attachments/assets/fedc49c3-12b6-4b11-ba6e-8ca94b191c45)

맨 앞쪽에 있는 비트를 구분비트라 하고, 클래스 A의 경우 맨 왼쪽에 있는 비트가 0이고 클래스 B는 10, 클래스 C는 110이다.
이를 통해 클래스 간 IP가 나눠진다. 
또한 네트워크의 첫 번째 주소는 네트워크 주소로 사용되고 가장 마지막 주소는 브로드캐스트용 주소로 네트워크에 속해있는 모든 컴퓨터에 데이터를 보낼 때 사용된다.

예를 들어 클래스 A로 12.0.0.0 이란 네트워크를 부여받았다 할 때 12.0.0.1 ~ 12.255.255.254의 호스트 주소를 부여받은 것.
이때 첫번째 주소인 12.0.0.0 은 네트워크 구별 주소로 사용하면 안되고 맨 마지막 주소인 12.255.255.255의 경우는 브로드캐스트용으로 남겨놔야하니 사용을 못한다.
그래서 그 사이에 있는 12.0.0.1 ~ 12.255.255.254를 컴퓨터에 부여할 수 있는 호스트 주소로 사용 가능.

하지만 이 방식은 사용하는 주소보다 버리는 주소가 많은 단점이 있었고 이를 해소하기 위해 DHCP와 IPv6, NAT 이 나온다.

### DHCP 
DHCP 는 IP 주소 및 기타 통신 매개변수를 자동으로 할당하기 위한 네트워크 관리 프로토콜이다.
이 기술을 통해 네트워크 장치의 IP주소를 수동으로 설정할 필요 없이 인터넷에 접속할 때마다 자동으로 IP주소를 할당할 수 있다.

많은 라우터와 게이트웨이 장비에 DHCP 기능이 있으며 이를 통해 대부분의 가정용 네트워크에서 IP 주소를 할당한다.

### NAT

NAT는 패킷이 라우팅 장치를 통해 전송되는 동안 패킷의 IP주소를 수정해 IP 주소를 다른 주소로 매핑하는 방법.
IPv4 주소체계만으로는 많은 주소를 모두 감당 못해서 이를 해결하기 위해 NAT으로 공인 IP와 사설 IP로 나눠서 많은 주소를 처리한다.
NAT을 가능하게 하는 소프트웨어는 ICS, RRAS, Netfilter 등이 있다.

![image](https://github.com/user-attachments/assets/9ee538ce-a4a0-4283-827b-5bf8b33c7153)
세개의 PC는 모두 192.168.1.xx 기반으로 각가의 다른 IP를 가지고 있고, 이를 사설 IP 라고한다.
그리고 NAT 장치를 통해 하나의 공인 IP인 67.210.97.1으로 외부 인터넷에 요청할 수 있다.

이를 통해 안쪽에 있는 PC는 하나의 IP인 67.210.97.1울 가번욿 각각 다른 IP를 가진 것처럼 인터넷을 사용할 수 있다.
이처럼 NAT 장치를 통해 사설 IP나 공인 IP로 변환하거나 공인 IP를 사설 IP로 변환하는데 쓰인다.

#### 공유기와 NAT

NAT을 쓰는 이유는 주로 여러 대의 호스트가 하나의 공인 IP 주소를 사용해 인터넷에 접속하기 위함이다. 
예를 들어 인터넷 회신 하나를 개통하고 인터넷 공유기를 달아서 여러 PC를 연결해 사용할 수 있는데 이게 가능한 이유는 인터넷 공유기에
NAT 기능이 탑재되어 있기 때문.

#### NAT을 이용한 보안
NAT을 이용하면 내부 네트워크에서 사용하는 IP 주소와 외부에 들어가는 IP 주소를 다르게 유지할 수 있기 때문에
내부 네트워크에 대한 어느 정도 보안이 가능

#### NAT의 단점
NAT는 여러명이 동시에 인터넷에 접속하게 되므로 실제 접속하는 호스트 숫자에 따라서 
접속 속도가 느려질 수 있다는 단점

### IP 주소를 이용한 위치 정보
IP 주소는 인터넷에서 사용하는 네트워크 주소이기 때문에 이를 통해 동 또는 구까지는 위치 추적이 가능하다.


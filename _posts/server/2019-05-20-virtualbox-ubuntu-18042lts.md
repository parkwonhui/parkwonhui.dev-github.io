---
layout: post
title: VirtualBox Ubuntu 18.04.2 LTS
categories: [server]
tags: [server,virtualbox]
comments: true
---

# VirtualBox Ubuntu 18.04.2 LTS

### Download
- [VirtualBox Download](https://www.virtualbox.org/)
- Ubuntu Server
- 리눅스 서버가 필요하므로 Ubuntu 가 아닌 Ubuntu Server를 다운받는다. 그냥 Ubuntu는 GUI 운영체제이다
- Ubuntu는 LTS(안정적이고 오랫동안 사용가능한 버전)을 Download 한다
- Putty 설치
- WinSCP 설치

### Ubuntu 설정
- 추가 버튼 클릭
- 종류는 Linux, 버전은 Ubuntu (64-bit)로 설치
- 메모리 2048MB(2GB) 설정
- 지금 가상 드라이브 만들기
- VDI(VirtualBox 디스크 이미지) 선택
- 100GB 설정(사용드라이브가 1TB라서)
- 설치 완료 후 '저장소' 클릭. 컨트롤러:IDE 아래 비어있음을 클릭하고 CD 버튼을 누른다. 그리고 Ubuntu ISO 선택

### Ubuntu 설치
- 언어 선택(English)
- Install Ubuntu
- 파티션 설정 Done, Done, Use An Entire Disk, 계속 Done 하고 마지막에 Continue
- ubuntu  로그인 id, pass 입력
- 추가 패키지 설치는 넘어감

### host 컴퓨터 정보 확인
- 네트워크는 '어댑터에 브리지' 하나만 사용

~~~
이더넷 어댑터 이더넷:

   연결별 DNS 접미사. . . . :
   링크-로컬 IPv6 주소 . . . . : fe80::881b:e340:c3c6:cae2%6
   IPv4 주소 . . . . . . . . . : 192.168.38.1
   서브넷 마스크 . . . . . . . : 255.255.192.0
   기본 게이트웨이 . . . . . . : 192.168.1.1
~~~

### 네트워크 설정
- ssh 설치 및 ssh 시작

~~~
sudo apt-get install openssh-server
service ssh restart
~~~
- 22번 포트 번호 열렸는지 확인

~~~
 netstat -tnlp
~~~

- 만약 20번 포트가 없다면 등록한다. 
- 포트 등록하면서 재시작 해도 설정이 남는 iptables-persistent을 설치한다

~~~
sudo apt-get update
sudo apt-get install iptables-persistent
~~~

- iptables 설정을 초기화한다(이 부분이 반드시 필요한지는 모르겠다)
- localhost 접속 허용 규칙이나 22번 포트 열기 등... 의 처리를 한다
- [출처]( http://bombee6.dothome.co.kr/2018/10/22/03-%EC%9A%B0%EB%B6%84%ED%88%AC-%EC%84%9C%EB%B2%84-18-04-1-lts-%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95/)

~~~
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -Z
sudo iptables -F
sudo iptables -X
~~~

### 고정 네트워크 IP 설정
- UbuntuNetplan 설명
- Ubuntu 17.10 부터 바뀐 네트워크 설정방법
- Ubuntu 17.10 버전 이상이라면 interfaces을 설정해도 Netplan 설정에 덮어져 ip설정이 제대로 되지 않을 수 있다

### Netplan 설정 방법
- vi Netplan 수정
- 50-cloud-init는 기본 인터페이스 설정

~~~
vi /etc/netplan/50-cloud-init.yaml
~~~
- ethernets 아래에 설정할 네트워크 디바이스 이름을 추가한다.
- addresses는 ip주소를 설정한다 /24는 서브넷마스크 대신 사용한다
- /24의 의미는 왼쪽부터 채워진 1bit의 수. 즉 /24는 11111111.11111111. 11111111.0000 = 255.255.255.0 이다
- enp0s3는 ifconfig로 네트워크 장비의 이름이다
- netmask와 gateway는 host 컴퓨터 설정과 맞춰준다

~~~
network:
    ethernets:
        enp0s3:
            dhcp4: no
            dhcp6: no
            addresses: [192.168.38.3/24]
            gateway4: 192.168.1.1
            nameservers:
              addresses: [8.8.8.8,8.8.4.4]
    version: 2
~~~ 

### 설정 적용

~~~
sudo netplan apply
~~~

### 확인
~~~
ifconfig -a
~~~


<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIA*BLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://parkwonhui.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            
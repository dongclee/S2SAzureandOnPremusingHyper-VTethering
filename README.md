안녕하세요…

부족하지만 또 하나의 그림책을 공유하고자 합니다.
제가 Azure 를 2013년도경 처음 접했을 때, 만들어 놓은 문서인데, Azure 를 포함한 Public 클라우드를 입문하는 분들에게 유용할 것 같아서 공유해 봅니다.

Azure를 처음 접했을 때, 모든 부분이 생소했지만, 가장 테스트 해 보기가 쉽지 않았던 부분이 On Premise 와 Azure 간의 Site-To-Site Tunneling (이하, S2S) 이었습니다. Azure 클라우드의 활용도를 높이기 위해서는 On Premise 쪽의 각종 컴퓨팅 자원을 Azure 로 마이그레이션하거나, Hybrid 형태로 사용해야 합니다.
이러한 Azure로의 마이그레이션 및 Hybrid 형태의 사용을 위해서는 반드시 필요한 부분이 바로 On Premise 와 Azure 간의 네트워크 연결성입니다.

On Premise 와 Azure 간의 네트워크 연결을 위해 사용하는 방법 중의 하나가 바로 S2S 입니다.
S2S 를 위해서는 아래와 같은 요소가 필요합니다.

1. On Premise : VPN 서버 (IKE 프로토콜 지원)
2. Azure : Virtual Network Gateway 

S2S 를 직접 구현하기 전에, S2S를 경험하기 위해서는 실물 VPN 서버가 필요합니다. 그러나, 보통의 실습 환경에서는 실물 VPN 서버를 접하기가 쉽지 않습니다. 또한, VPN 서버를 구비하고 난 후에는, VPN 서버의 외부 네트워크 인터페이스에 외부 공인 IP 또한 할당해야 합니다. 공인 IP 부분도 실습 초보자들이 구비하기에는 어려움이 많습니다.

이러한 부분을 고려해서, 저는 몇 가지 제 On Premise 지식 및 인터넷 자료를 참조하여, S2S 환경을 테스트 할 수 있는 데모 환경을 만들어 보았습니다.

먼저, 최소로 구비해야 할 장비는 아래와 같습니다.

1. Physical Machine : Hyper-V 가 설치된 Windows Server OS 또는 Window Client OS
2. 외부 네트워크 연결 : 가정용 인터넷 (ex, KT GigaWiFi 또는 LGU 핸드폰 테더링)

저는 위 최소 장비를 바탕으로 아래와 같은 데모 환경을 만들었습니다.

 ![제목 없음](https://user-images.githubusercontent.com/42400574/219842697-16b85f8e-0983-4889-b112-092ed89b3c81.jpg)

위 데모 환경을 보면 알겠지만, 제 노트북에 Windows Server 2012 R2 DataCenter 를 설치하고, Hyper-V 가상화 환경을 활성화 했습니다. Hyper-V 호스트에 총 2개의 VM을 생성하고, 하나의 VM에 네트워크 카드 2개를 장착하여, 하나의 네트워크 카드에는 GiGa Wifi 를 연결하고, 나머지 네트워크 카드에는 Hyper-V 내부 가상 스위치에 연결하였습니다.

여러분들은 Windows Server 2016 2019 2022 를 사용하셔도 괜찮습니다. 제가 이 문서를 만들 당시에 최신 OS가 Windows Server 2012 R2 였습니다. 또한, 나머지 VM은 테스트 클라이언트로써 Windows 8.1 을 사용했는데, 지금은 Windows 10 또는 11을 사용하셔도 무방합니다.

핵심은, Hyper-V 호스트에 설치된 Windows Server 2012 R2 DataCenter OS 내의 VPN 서버를 구현하는 것 입니다. 다행히도, Windows Server 에는 RRAS 라는 기능이 VPN 서버 역할을 할 수 있습니다. 본 문서의 가장 핵심적인 부분은 Windows Server 내에 VPN 서버를 구현하고 Azure 와의 연결성을 위해 필요한 구성을 하는 것 입니다. 또한, Window Server 내의 VPN 서버의 외부 공인 IP 를 우리가 손 쉽게 접할 수 있는 홈네트워크 및 핸드폰 테더링으로 구현할 수 있다는 점입니다.

제가 첨부한 문서를 참조하여, 여러분들도 이제 S2S 환경을 손 쉽게 구현할 수 있습니다.


여러분들 이제 더 이상 환경 탓 하지 마시고, S2S 를 구성하고 연습해 보세요

[Creating a hybrid Active Directory & a site to site (S2S) VPN to Azure.pdf](https://github.com/dongclee/S2SAzureandOnPremusingHyper-VTethering/files/10773412/Creating.a.hybrid.Active.Directory.a.site.to.site.S2S.VPN.to.Azure.pdf)

## *4-1 Network layer: overview*

지금까지 배운 5계층의 application layer와 4계층의 transport layer에서는 end-system, network의 edge부분에서의 동작을 다뤘다. 즉 내 컴퓨터에 데이터가 배달된 이후에 이 데이터를 어떻게 처리할 것인지에 대해서 생각했다. 이제부터 배울 3계층의 network layer에서는 내 컴퓨터까지 데이터가 어떻게 오는지에 대해 다룰 것이다. 이는 network edge 부분이 아닌 network core 부분의 동작을 다루는 것이다.

Internet은 network of networks, 즉 수많은 네트워크를 연결해주는 네트워크이다. 네트워크와 네트워크 사이에는 라우터가 있다. 라우터를 통해 한 네트워크에서 다른 네트워크로 넘어갈 수 있다. 

앞 장에서 반복해서 다뤘듯이 N layer는 N - 1 layer의 서비스를 이용해 작동한다. 마찬가지로 3계층인 network layer는 2계층인 data link layer의 서비스를 이용한다. data link layer가 제공하는 것은 라우터와 라우터 사이의 데이터 전달이다. 대표적으로 ethernet이 있고, 요즘은 거의 ethernet을 이용하는 추세이며 앞으로도 그럴 것 같다. 이 하위 레이어의 서비스를 이용하여 network layer가 제공하는 것은 host와 host 사이의 데이터 전달이다. 

# Network-layer services and protocols

- 3L의 전송 단위는 패킷 packet 이다.  datagram이라고도 한다.
  - sender: transport layer에서 전달받은 segment를 IP 헤더를 붙여 datagram으로 만들어  link layer에 전달한다. encapsulation.
  - receiver: datagram의 IP 헤더를 확인하고 떼어내어 segment로 만들고 transport layer로 전달한다. decalsulation.
- network layer protocol (IP) 는 인터넷에 접속하는 모든 장치에 있다. 네트워크 edge 장치에는 IP를 포함해 5계층까지 구현되어 있고, 라우터 등 네트워크 core 장치에는 IP, 3계층까지 구현되어 있다.
- router: 라우터는 자신의 input port로 들어온 모든 IP datagram들의 헤더를 확인하여 적절한 output으로 내보내 준다. 즉 목적지 주소 IP를 확인해 적절한 다음 라우터로 보내는 것이다.



# Two key network-layer functions

network-layer의 기능은 크게 두 가지로 나뉜다. network core에서의 패킷의 이동은 자동차를 타고 여행을 가는 것에 비유할 수 있다.

- **forwarding**: 라우터의 input link로 들어온 패킷을 적절한 output link로 내보내준다.  자동차가 톨게이트를 지나서 목적지로 이어지는 갈림길로 빠지는것에 비유할 수 있다.
- **routing**: 패킷이 출발지에서 목적지까지 이동할 때 어떤 경로를 거쳐서 가야하는지 결정한다. 이를 라우팅 알고리즘을 돌린다고 한다. 여행 계획을 세울 때 자동차를 어떤 경로를 통해 이동시킬지 결정하는 것에 비유할 수 있다.

routing을 통해 정해진 경로를 따라 각각의 갈림길 router에서 적절한 길목으로 빠지는 동작 forwarding을 반복하다 보면 목적지에 도착하게 된다.



# Network layer: data plane, control plane

forwarding과 routing은 각각 다른 영역의 동작으로 구분한다.

**Data plane:** 직역하면 데이터 정보를 날려보내기. 라우터가 자신의 input port로 들어온 패킷을 테이블의 정보를 확인해 적절한 output port로 내보내는 것을 의미한다. 즉 forwarding하는 것이다. 4장에서 다룬다.

- 각 라우터에서 로컬하게 발생하는 기능이다.

**Control plane:** 직역하면 컨트롤 정보를 날려보내기. 패킷이  출발지에서 도착지까지 가기 위해 지나야 할 라우터의 경로를 지정하는 것을 의미한다. 즉 routing하는 것이다. 5장에서 다룬다.

- 모든 라우터가 정보를 주고받아서 작동하는 network-wide logic이다.
- control-plane을 구현하는 방법은 두 가지가 있다.
  - traditional routing algorithms: 라우터가 서로 정보를 교환하면서 라우터 내부에서 알고리즘을 돌려 테이블을 작성하는 방법이다. 아직까지 제일 많이 사용되고 있다.
  - software-defined networking (SDN): 원격 서버가 라우터들에게서 정보를 받아 알고리즘을 돌려 테이블을 작성하고, 그것을 다시 라우터들에게 뿌려준다. 



# Network service model: best-effort service

Internet은 "best effort" 모델로 설계되었다. 패킷을 전송하는데 최선을 다하겠지만 어떤 것도 보장하지 못한다는 의미이다. 패킷이 목적지까지 확실히 전달되는 보장을 못하고, 도착하는 시간과 순서도 보장 못하고, 최소 대역폭의 제공을 보장하지도 못한다. 그럼에도 다른 모델들을 제치고 Internet이 사용되는 이유는 무엇일까?

가장 큰 이유는 충분한 대역폭 bandwidth가 제공되고 있기 때문이다. 또한 application-layer에 구현된 분산 서비스들 (데이터 센터, CDN 등)이 있어서 실시간성과 대역폭 개런티 등이 충분히 해결된다. 때문에 3계층에 굳이 다른 서비스를 구현할 필요성이 없어졌고, 제일 단순한 IP가 채택되었다.






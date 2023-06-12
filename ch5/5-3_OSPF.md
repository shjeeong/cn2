## *5-3 intra-ISP routing: OSPF*

지금까지 공부한 라우팅에 대한 내용은 현실적이지 않다. Internet이 하나의 작은 네트워크인 상황에서나 적용이 가능하다. 실제의 네트워크 상황에서는 아래의 두 가지를 고려해야 한다.

- scale: Internet에는 수십억 개의 노드가 존재한다. billions of destinations. 수많은 목적지들에 대해  알고리즘을 돌려서 라우팅 테이블을 만드는 것은 불가능하다.

- administrative autonomy: Internet은 a network of networks, 네트워크들의 네트워크이다. 각 네트워크의 네트워크 관리자는 자신들만의 라우팅 방법을 사용한다.



# Interconnected ASes

**autonomous systems (AS) (a.k.a. domains):** AS는 관리자가 제어하는 네트워크의 단위이다. 인터넷은 이러한 AS들이 서로 연결되어있는 형태로 구성되어 있다.

- **intra-AS (aka "intra-domain"):** 같은 AS (network) 안에서의 라우팅
  - 같은 AS 내에서는 동일한 라우팅 프로토콜을 실행한다. 다시말하면 서로 다른 AS에 있는 라우터들은 각각 다른 라우팅 프로토콜을 돌리고 있을 수 있다.
  - **gateway router**: 한 AS의 안에는 외부의 AS와 링크가 연결되어있는 라우터가 하나 이상 존재한다. 이 라우터를 gateway router라고 한다.
- **inter-AS (aka "inter-domain"):** AS 끼리의 라우팅
  - gateway router가 inter-domain 라우팅을 한다. gateway router는 외부의 AS와 연결되어 있으면서 특정 AS에 소속된 라우터이기도 때문에 AS 내부의 intra-domain 라우팅도 한다. AS끼리의 라우팅은 BGP 라우팅 프로토콜을 사용한다. 

이 구조에 따라 forwarding table은 

- AS 내부의 목적지는 intra-AS가 라우팅해서 경로를 설정해주고
- AS 외부의 목적지는 inter-AS와 intra-AS 둘 다 이용해서 경로를 설정해준다. 

# Inter-AS routing: a role in intra domain forwarding



# Intra-AS routing: routing within an AS



# OSPF (Open Shortest Path First) routing


# 쿠버네티스 이해하기
## 소개
쿠버네티스(Kubernetes)는 도커와 같은 컨테이너 관리를 자동화하는 오픈소스로 간단하게 말하면, "컨테이너 오케스트레이션" 엔진이다.
Cloud Native Computing Foundation(CNCF)에서 주관하고 있으며, K와 s 사이에 글자가 8개가 있어서 주로 K8s로 줄여 부르기도 한다.

## 배경
![container_evolution](https://github.com/Meet-Coder-Study/posting-review/assets/35288895/c7b3013d-7866-4002-b865-a0739c9021b8)

### 전통적인 배포 시기
예전에는 서버가 물리적으로 구성되어 애플리케이션을 실행했다. 하나의 서버에서 여러 애플리케이션을 실행할 때 다른 애플리케이션 성능이 저하되거나 리소스를 전부 특정 애플리케이션이 차지할 가능성이 있었다. 이러한 문제를 방지하려면 물리적인 서버를 여러 개 구축하여 각각의 애플리케이션을 실행해야 했는데, 이 방법은 확장성이 낮았고 물리적인 서버를 많이 유지하는 비용이 만만찮았다.

### 가상화된 배포 시기
위의 문제에 대한 해결책으로 하나의 물리 서버 CPU 에 여러 가상 머신(VM)을 실행하는 가상화가 도입되었다. 가상 머신은 가상화된 하드웨어로 자체 운영체제를 포함한 구성 요소를 실행할 수 있다. 각 VM마다 애플리케이션이 분리되어 애플리케이션마다 서로의 리소스에 접근할 수 없어 효율적으로 활용이 가능해진다. 애플리케이션을 쉽게 추가하거나 업데이트할 수 있고 하드웨어 비용을 절약하여 높은 확장성을 가진다. 

### 컨테이너 개발 시기
컨테이너는 VM과 유사하지만 애플리케이션 간의 OS를 공유하여 보다 가벼워 이미지 생성이 쉽다. 자체 파일 시스템, CPU 점유율, 메모리, 프로세스 공간 등이 있지만 기본 인프라의 종속성이 없기 때문에 다른 클라우드나 OS에도 이식할 수 있다. 
컨테이너 이미지를 빌드하고 배포하면서 빠르고 효율적인 CI/CD가 가능해진다. 
모놀리식이 아닌 마이크로서비스 단위로 애플리케이션을 쪼개어 동적으로 배포하고 관리할 수 있다.


## 특징 
쿠버네티스는 분산 시스템을 탄력적으로 실행하기 위한 프레임 워크를 제공하여 아래와 같은 기능을 제공한다.
한 컨테이너가 다운되면 다른 컨테이너를 확장하고 장애 조치를 하는 과정을 자동화할 수 있다.
뿐만 아니라, 하드웨어가 아닌 컨테이너 수준에서 Platform as a Service(PaaS)처럼 운영되어 배포, 스케일링, 로드 밸런싱 등의 기능을 제공하고 로깅, 모니터링, 알림 등의 솔루션을 선택적으로 통합할 수 있다.

#### 서비스 디스커버리와 로드 밸런싱 
쿠버네티스에서는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다.
또한, 컨테이너에 네트워크 트래픽이 많으면 로드밸런싱하여 배포가 안정적으로 이루어질 수 있다.

#### 스토리지 오케스트레이션 
로컬 저장소, 클라우드에서 제공하는 저장소 등의 어떤 스토리지 시스템이든 자동으로 탑재할 수 있다.

#### 자동화된 롤아웃과 롤백 
컨테이너의 원하는 상태를 미리 정의하여 원하는 설정 속도로 변경할 수 있다. 예를 들어, 배포용 새 컨테이너를 만들어 기존 것을 제거하고 모든 리소스를 새 컨테이너에서 그대로 적용하는 과정을 자동화 할 수 있다.

#### 자동화된 빈 패킹(bin packing) 
각 컨테이너가 필요하는 CPU와 메모리 사용량을 쿠버네티스에 지시하면 클러스터 노드에 맞추어 리소스를 실행시킨다.

#### 자동화된 복구(self-healing) 
실행에 실패한 컨테이너를 자동 재시작하고 교체하는 등의 일련의 작업을 클라이언트에게 노출시키지 않고 작업한다.

#### 시크릿과 구성 관리 
암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 환경변수를 노출하지 않고도 시크릿 및 애플리케이션 구성을 배포 및 업데이트할 수 있다.

#### 다양한 워크로드 지원
상태 유지가 필요 없는(stateless) 워크로드, 상태 유지가 필요한(stateful) 워크로드 등 다양한 워크로드를 지원한다.


### 참고자료
[쿠버네티스란 무엇인가? | kubernetes.io](https://kubernetes.io/ko/docs/concepts/overview/)
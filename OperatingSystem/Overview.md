### What Operating Systems Do
- 컴퓨터의 하드웨어를 관리하고 하드웨어와 소프트웨어, 사용자를 매개하는 프로그램
- kernel + kernel modules 로 구성

### User View
- 컴퓨터 자원 사용(Resource Utilization)을 신경쓰지 않도록 도우며, 사용자가 컴퓨터를 쉽게 이용할 수 있도록 함

### System View 
- 자원 할당자(Resource Allocator)로서 컴퓨터 자원들을 관리하는 제어프로그램으로서 동작

### Computer-System Organization & Operation
- 여러개의 CPU와 장치 컨트롤러 로 구성되며 공통버스로 이어져 메모리를 공유한다.
- Bootstrap program이 시스템을 초기화 하고 운영체제를 실행하며 시스템이 완전히 부팅되면 운영체제는 이벤트 발생을 기다림
- 입출력 장치외 CPU는 동시에 실행될 수 있음
- 장치 컨트롤러는 Interrupt를 발생시켜 이벤트 발생을 CPU에게 알림

### Interrupt
- 인터럽트란 : 어떤 장치가 다른 장치의 일을 잠시 중단시키고 자신의 상태변화를 알려 주는 것, 인터럽트가 걸리면 인터럽트를 받은 장치는 현재 자신의 상태를 기억시켜두고 인터럽트 처리를 진행한다.
- 인터럽트 종류 :     
  - 예외상황 인터럽트 : 시스템에 심각한 에러가 생겼을 때 발생된다.  
    ex) 0 / ?, page fault 등
  - 하드웨어 인터럽트 : 주변 장치에 무슨 일이 생겼을 때 발생된다.
    ex) keyboard event 등
  - 시스템 콜 : 프로그래머가 운영체제의 서비스를 요청하기 위해 프로그램 내에서 int 명령으로 발생시킨다. 사용 규칙은 운영체제 마다 다름
- 인터럽트 처리 과정
  - INT 발생 -> 현 상태(current context)에 대한 정보 저장 -> INT 처리 -> 현 상태로 리턴 혹은 next context 로 리턴
- Handling 방식 : 
  - Interrupt driven : 인터럽트가 발생하기 전까지 CPU는 대기상태에 머뭄 --> 입출력 장치에서 필요시마다 인터럽트 전송해 순간순간 사용. 폴링에 비해 성능 좋음
  - Polling : 주기적으로 이벤트를 감시해 처리 루틴 실행 --> 입출력 장치가 증가할 수록 CPU 점유 시간이 증가하여 성능이 하락함.

### I/O
- 컴퓨터는 다양한 입출력 장치를 가지고 있으며, 입출력 컨트롤러는 각각의 다른 장치들을 담당한다. 컴퓨터는 이 컨트롤러 덕분에 다양한 장치를 이용할 수 있다. 또한 운영체제는 각 장치 컨트롤러를 제어하기 위한 장치 드라이버를 가지고 있다.
- 사용자 프로그램은 커널과 사용자 프로그램을 매개하는 인터페이스인 시스템 콜을 통해 입출력을 요청할 수 있다.

### Direct Memory Access
- 과거에는 장치 데이터를 처리하기 위해서 CPU를 거쳐 메모리에 로드하는 방식 사용 --> CPU 자원이 너무 많이 소모됨
- 장치와 메모리를 직접 연결하는 방식으로 버스가 지원하는 기능 --> 입출력 장치간 데이터를 주고 받는 과정이 끝났을 때에만 인터럽트 발생 --> CPU 가용시간 증가

### Storage 
![image](https://t1.daumcdn.net/cfile/tistory/992DB8435AEF240E25)
- 보조기억장치는 용량이 크고 저렴한 반면 캐시나 레지스터는 용량이 작고 비싸다.

### Operating System Structure
- Multiprogram : 여러 프로그램을 메모리에 로드해 두고 한 프로세스가 대기 상태가 되면 다른 프로세스의 작업을 수행하는 시스템
- Time Sharing == Multitasking : 프로세스마다 작업 시간을 정해두고 번갈아가면서 작업하는 방식

### Process
- 구성 : Stack, Heap, Data, Code
- State : new, ready, running, terminated, wating
- Process Control Block : 프로세스 상태, 프로그램 카운터, 메모리 한계, 레지스터 정보 등 담겨있음

### 프로세스간 통신; IPC(Inter Process Communication) 종류  
- PIPE : 부모 자식간의 단방향 통신, 양방향일 경우 두개의 파이프(파일) 필요, FIFO 구조
- Message Queue : 프로세스간 단방향 통신, 메모리를 사용한 PIPE, FIFO
- Shared Memory : 시스템 상의 공유 메모리를 통해 양방향 통신, 일정한 크기의 프로세스간에 공유하는 구조, 공유 메모리는 커널에서 관리됨
- Socket : 다른 시스템간 양방향 통신, IP주소와 포트 정보가 있으면 클라이언트는 네트워크를 통해 서버 프로세스에 접근, 데이터 세그먼트 처리를 잘해야 함, 원격에서 프로세스간 데이터 공유시 사용    

### References 
- https://ferrumdev.tistory.com/18
- https://doitnow-man.tistory.com/110

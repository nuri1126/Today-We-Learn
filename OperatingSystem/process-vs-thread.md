### 프로세스란
![image](https://gmlwjd9405.github.io/images/os-process-and-thread/process.png)
- 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램
- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스
- 운영체제로부터 시스템 자원을 할당받는 작업의 단위

### 스레드란 
![image](https://gmlwjd9405.github.io/images/os-process-and-thread/thread.png)
- 프로세스 내에서 실행되는 여러 흐름의 단위
- 프로세스의 특정한 수행 경로
- 프로세스가 할당 받은 자원을 이용하는 실행의 단위
- 스레드는 프로세스 내에서 각각 stack만 따로 할당 받고 code, data, heap 영역은 공유한다. 
- 반면에 프로세스는 다른 프로세스의 메모리에 직접 접근할 수 없다.

## ps 명령어 
리눅스는 다중 사용자, 사용 작업 시스템이기 때문에 여러 개의 프로세스를 동시에 수행하기에 어떤 프로세스들이 실행되고 있는지 알아야 합니다.
따라서 현재 시스템에서 실행 중인 프로세스에 관한 정보를 출력하여 사용자에게 정보를 제공하는 명령어가 필요한데 이게 ps 명령어입니다.

ps 명령어는 Process State의 약자로 현재 실행 중인 프로세스와 상태를 출력하는 명령어입니다. 
ps명령어의 옵션은 시스템 계열마다 다른 표기법 및 출력을 가지고 있습니다. 
따라서 help 명령어를 통해 옵션을 확인하는 것이 더 정확합니다.

명령어와 함께 사용하는 주요 옵션은 아래와 같습니다.
-e: 현재 사용자뿐만 아니라 다른 사용자들의 구동시킨 모든 프로세스를 보여줍니다. 
-f: 보다 상세한 정보를 보여줍니다. (Full format)
-l: -f보다 상세한 정보를 보여줍니다.(Long format)

위의 사진에서 출력되는 결과의 각 필드의 의미는 아래와 같습니다.
+ F: 프로세스 플래그+ S: 프로세스의 현재 상태
+ UID: 프로세스를 실행시킨 사용자 ID
+ PID: PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.
+ PPID: 프로세스의 부모 프로세스 ID
+ C: 프로세스가 사용하는 CPU 사용량
+ PRI: 커널에 의해 나타나는 프로세스의 실행 우선순위를 나타냅니다. 값이 낮을수록 더 높은 우선 순위를 가집니다.
+ NI: 사용자에 의해 변경된 프로세스의 우선 순위를 나타냅니다.
+ ADDR: 프로세스의 메모리 주소를 나타냅니다.
+ SZ: 가상 메모리 사용량
+ STIME: 프로세스 시작 시간
+ TTY: 프로세스가 실행된 터미너르이 종류와 번호
+ TIME: 프로세스에 의해 사용된 CPU 시간
+ CMD: 실행된 프로세스의 이름 또는 실행된 명령


## jobs 명령
ps 명령어와 달리 백그라운드에서 실행중인 프로세스를 확인할 수 있다. 현재 쉘에서 실행시킨 백그라운드 작업의 목록이 출력되며, 각 작업에는 번호가 붙어 있어 kill 명령어 등으로 사용할 수 있다. job를 사용할 경우 보통 아무 옵션을 주지 않고 사용한다.

`job [옵션] [작업번호]

jobs에서 출력되는 백그라운드 작업의 상태값은 다음과 같습니다.
Running: 작업이 계속 진행중
Done: 작업이 완료되어 0을 반환
Done(code): 작업이 종료되었으며 0이 아닌 코드를 반환
Stopped: 작업이 일시 중단
Stopped(SIGTSTP): SIGTSTP 시그널이 작업을 일시 중단
Stopped(SIGSTOP): SIGSTOP 시그널이 작업을 일시 중단
Stopped(SIGTTIN): SIGTTIN 시그널이 작업을 일시 중단
Stopped(SIGTTOU): SIGTTOU 시그널이 작업을 일시 중단

** ps 명령어와 jobs 명령어의 차이점 **

ps 명령어는 모든 프로세스의 목록을 보여주며, 사용자가 실행한 프로세스 또는 시스템 프로세스를 모두 포함합니다. 반면에 jobs 명령어는 현재 쉘 세션에서 실행 중인 프로세스 목록만을 보여줍니다. 따라서 백그라운드에서 실행 중인 프로세스를 확인하려면 jobs 명령어를 사용해야 합니다.
또한, ps 명령어는 더 자세한 정보를 제공하며, 필요한 옵션을 사용하여 원하는 결과를 얻을 수 있습니다. 반면에 jobs 명령어는 현재 프로세스의 상태만을 간단하게 보여주는 목적으로 사용됩니다.


## kill 명령어
리눅스 환경에서 프로세스를 종료하기 위해 kill 명령어를 사용합니다. kill이라는 명령어를 이용해서 특정 프로세스에 작업 중지, 실행 종료, 대기, 재시작, 강제 종료 등의 시그널을 전달할 수 있다.

주로 사용하는 시그널
+ SIGHUP : 재시작할 때 사용
+ SIGINT : 실행 중지 시그널, Ctrl + c
+ SIGKILL : 프로세스 강제 종료
+ SIGTERM : 프로세스 정상종료 (기본 명령)
+ SIGCONT : 정지된 프로세스 실행
+ SIGSTOP : 터미널에서 입력되는 정지 시그널
+ SIGTSTP : 실행 정지 후 재실행 대기, Ctrl+ z

kill 명령어를 통해 프로세스를 종료하기 위해 먼저 PID나 작업번호를 확인해야 합니다.
ps 명령어를 통해 PID 찾을 수 있고, jobs를 통해 작업번호를 찾을 수 있습니다.

` kill -시그널번호(시그널명) %작업번호
` kill -시그널번호(시그널명) PID

kill 옵션
ps 로 PID 를 kill 명령어로 종료 시키는 옵션 중 -9 와 -15 가 있습니다.이중 -9 옵션은 프로세스를 강제로 종료 시키는 옵션으로 프로세스가 정상 종료가 안될 경우 사용하게 됩니다. 

-15 : 정상 종료 
-9 : 강제 종료

kill -15 <PID>
TERM 시그널 (default Option 으로 기본 적용)자신이 하던 작업을 모두 안전하게 종료하는 절차를 밟으며 프로세스를 종료메모리상에 있는 데이터와 각종 설정/환경 파일을 안전하게 저장한 후 프로세스를 종료합니다.
 
kill -9 <PID>
리눅스 커널이 프로세스를 강제 종료프로세스를 강제 종료하기 때문에 저장되지 않은 데이터가 날아가는 경우 발생합니다.


## top 명령어
top 명령어는 리눅스 시스템의 CPU 사용량, 메모리 사용량 등 전반적인 상황을 실시간으로 모니터링할 수 있는 명령어입니다.
터미널에서 top 명령어를 입력하면 아래 그림과 같이 출력됩니다.
![top]https://github.com/bakyunjae/-SW/blob/main/top.png

top 명령어를 사용했을 때 나오는 결과에 대해 설명하자면 다음과 같습니다.

첫번째 줄부터 설명하면 시스템 시간, 업타임, 유저 세션 수, 로드 에버리지를 나타냅니다.
1. 시스템 시간: 시스템의 현재 시간, 이 시간은 GMT(그리니치 평균 시)기준으로 표시합니다.
2. 업타임: OS가 얼마나 살아 있는지 표시합니다.
3. 유저 세션 수: 현재 시스템에 연결된 사용자의 수입니다.
4. 로드 에버리지: 이 부분에는 3개의 숫자가 출력되는데, 왼쪽부터 각각 1분, 5분, 15분 동안의 평균 시스템 부하를 의미합니다.
리눅스에서 실행된거나 대기중인 프로세스의 평균이다. 싱글 코엉일 경우 1.0의 값이 CPU를 100%를 사용하고 있다는 의미입니다.
멀티코어라면 코어만큼 곱한 값이 CPU 100%를 사용하고 있다는 의미이다.만약 100%를 넘어간다면 CPU에서 처리하지 못하고 대기하고 중인 프로세스가 있다는 뜻입니다.

2번째 줄에는 Tasks에 관한 내용이 출력됩니다. Tasks는 현재 프로세스들의 상태를 나태내주는 영역입니다. 
total : 모든 상태의 프로세스 합계를 보여 줍니다.
running : 요청을 처리하고 정상적으로 실행하며 CPU 액세스 권한을 가진 프로세스 수를 보여 줍니다.
sleeping : 리소스를 대기 중인 프로세스를 나타냅니다. 이는 정상 상태입니다.
stopped : 리소스를 종료하거나 해제하는 프로세스를 보고합니다. 이러한 프로세스는 상위 프로세스에 종료 메시지를 보냅니다.
zombie : 부모 프로세스가 릴리스하기를 기다리는 프로세스를 말합니다.

3번째 줄에는 CPU가 어떻게 사용되고 있는지 그 사용율을 보여주는 영역입니다. 모든 값의 총합은 100%입니다.
1. us : 유저 영역에서의 CPU 사용율 
2. sy : 커널 영역에서의 CPU 사용율 
3. ni : 프로세스 우선순위 설정에 사용되는 CPU 사용율
4. id : 사용하지 않는 CPU 비율
5. wa : I/O 대기 상태의 CPU 사용율
6. hi : 하드웨어 인터럽트에 사용되는 CPU 사용율
7. si : 소프트웨어 인터럽트에 사용되는 CPU  사용율
8. st :Hypervisor VM에서 사용하여 대기하는 CPU 비율

나머지 4, 5번째 줄에는 메모리 사용량에 관련된 영역입니다. 4번째 줄은 RAM 메모리 영역, 5번쨰 줄은 Swap 메모리 영역입니다.
Swap 메모리 영역은 RAM의 사용량이 거의 가득 찼을 때 사용하는 메모리영역입니다. 이 영역은 디스크를 사용하기에 RAM 메모리보다 속도가 많이 느린 단점을 지닙니다.
1. PID: PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.
2. USER: 프로세스를 실행한 사용자 계정을 나타냅니다.
3. PR : 커널에 의해 나타나는 프로세스의 실행 우선순위를 나타냅니다. 값이 낮을수록 더 높은 우선 순위를 가집니다.
4. NI : 사용자에 의해 변경된 프로세스의 우선 순위를 나타냅니다.
5. VIRT : 프로세스가 소비하고 있는 총 메모리입니다. 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함합니다.
6. RES : RAM에서 사용중인 메모리의 크기를 나타냅니다.
7. SHR : 다른 프로세스와 공유하고 있는 메모리의 크기를 KB 단위로 나타냅니다.
8. S : 포로세스의 현재 상태를 나타내며, R은 실행 중, S는 슬립 중, Z는 좀비상태를 의미합니다.
9. %CPU : 프로세스가 CPU를 사용하는 비율을 백분율로 나타냅니다. 
10. %MEM : 프로세스가 메모리를 사용하는 비율을 백분율로 나타냅니다.
11. TIME+ : 프로세스가 실행되며 사용한 누적 CPU 시간을 나타냅니다.
12. COMMAND : 해당 프로세스를 실행한 명령어 또는 프로그램을 나타냅니다.

top 명령어 실행 중 다음의 키를 사용하여 인터페이스를 제어할 수 있습니다. 
k키를 입력하고 종료하고 싶은 프로세스의 PID를 입력하면 프로세스를 종료할 수 있다.
1키를 입력하면 CPU를 코어별로 모니터링이 가능하다.

m키를 입력하면 메모리영역에서 메모리 사용률을 시각화 할 수 있다.

이외에도 여러 옵션이 존재한다. 알고 싶다면 h키를 입력하면 도움말이 표시됩니다.






**Volatility?** <br>
**- 메모리 포렌식 도구. 오픈소스. CLI 인터페이스**<br>
**- Volatilility에서 증거를 획득할 수 있는 이유**<br><br>

메모리 = 프로세스들이 뛰어놀고 있는 운동장, 마음대로 쓰는 공간이며 프로세스한테 부여된 주소들이 메모리이다.<br>
Volatility는 어떤 규칙적인 구조체가 메모리 안에 존재할 경우에 그것을 잘라내서 가져오는 역할을 한다.<br>
모든 내용들을 규칙적으로 가져올 순 없으며 한정적이고 사실 프로세스가 사용하고 있는 모든 데이터를 볼라틸리티의 기본적인 기능만으로 가져오는 것에는 한계가 존재한다.<br><br>

분석가가 증거를 어떻게 추출하냐의 방법에 따라서 획득할 수 있는 증거의 양이 천차만별이다.<br>

**Volatility 명령어 정리**<br>
운영체제 식별<br>
- imageinfo : 메모리 덤프의 운영체제를 식별<br><br>

프로세스 검색<br>
- pslist : 시간 순서대로 보여줌<br>
- psscan : 숨겨진 프로세스 출력 가능<br>
- pstree : PID, PPID 기준으로 구조화하여 보여줌<br>
- psxview : pslist, psscan을 포함한 도구들의 결과를 한 눈에 볼 수 있음<br>

네트워크 분석<br>
- netscan<br>
  - Windows 7 이상<br>
  - TCP, UDP / IPv4, IPv6<br>
  - Listening(소켓을 열고 있는 상태), Established(소켓이 열려서 송신 중인 상태), Closed(소켓이 닫힌 상태)<br><br>

- Connections<br>
  - Windows 7 미만<br>
  - 현재 연결된 TCP 통신에 대한 정보, Established 상태만 출력<br><br>

- Sockets<br>
  - Windows 7 미만
  - TCP, UDP를 포함한 모든 프로토콜<br>
  - 현재 Listening 상태에 있는 소켓을 출력<br><br>

- CMD 분석<br>
  - cmdscan, consoles : 콘솔에 입력한 값들을 볼 수 있음(출력 값도 볼 수 있다.)<br>
  - cmdline : 프로세스가 실행될 때의 인자값을 확인할 수 있음(실행을 할 때 초기 값들을 줄 수가 있는데 그것을 확인 할 수 있다.)<br><br>

- 파일 분석 및 덤프<br>
  - filescan : 메모리 내에 존재하는 모든 파일들의 리스트 출력<br>
  - dumpfiles : 파일을 덤프. 옵션으로 메모리 주소, 프로세스 줄 수 있다,-Q 옵션을 통해 Offset을 주는 옵션과 -p 옵션을 주어서 프로세스를 넣어주면 해당하는 프로세스가 사용하는 모든 파일을 뽑아준다.<br><br>

- 프로세스 세부 분석<br>
  - memdump : 특정 프로세스의 메모리 영역을 덤프 -> strings 사용<br>
  - procdump : 프로세스의 실행 파일을 추출<br><br>

- 악성 프로그램 식별<br>
  - virustotal 주로 사용<br>
  - Windows Defender도 정확한 편임<br><br><br><br><br><br><br>



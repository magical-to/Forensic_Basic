![image](https://github.com/user-attachments/assets/1caa22eb-46d3-4f13-920d-e42636c628a0)If need english translation, contact me, thx.<br><br> 
  Volatility - 메모리 관련 데이터를 수집해주는 도구<br><br>

  <br>
command in Windows PowerShell<br>
메모리 덤프를 보고 Volatility가 어떤 운영체제의 메모리 덤프인지 판단 -> 어떤 운영체제인지?에 대한 값이 앞으로의 모든 분석에 사용될 예정<br><br><br>


![2](https://github.com/user-attachments/assets/b71f08b4-23fb-4b59-a73e-23642df69765)<br>
우선, 이전과 같이 imageinfo 명령어를 통해 운영체제를 식별할 예정이다.<br><br>

(Windows XP 기준)<br>
connections : '현재' 연결된 TCP 통신에 대한 정보<br>
sockets : 응답 받기를 기다리고 있는 모든 프로토콜에 대한 socket 정보<br><br>

(Windows 7 up 기준)<br>
netscan<br><br>

cmdline : 프로세스가 실행될 때 인자값<br>
cmdscan : 콘솔에 입력한 값들을 실제로 볼 수 있다.<br>
consoles : 콘솔에서 입력 & 출력한 값들을 실제로 볼 수 있다.<br><br><br><br>



TeamViewer -> TeamViewer 관련 악성코드가 존재하기 때문에 하위 3개까지 의심<br>
mstsc -> 내 컴퓨터를 원격에서 수리를 할 때 사용하기 때문에 의심<br>
explorer -> 윈도우 탐색기에서 cmd를 오픈하였기 때문에 의심<br>
outlook -> 메일 관련 악성 코드가 매우 많이 유포되기 때문에 의심<br>
iexplorer -> iexplorer 하위 프로세스에서 cmd가 실행이 되었기에 의심<br>


8,9 cmdscan 살펴봄, wce.exe를 사용해 무언가를 Temp로 빼낸거 같다.
+ 관리자로서 cmd 실행해서 다시 해보는 모습도 보인다.

outlook.exe를 살펴봐야하고
tv_w32.exe도

C:\Windows\Temp\wce.exe, w.tmp


filescan.log에서의 605번째 줄 wce.exe를 dumpfiles을 이용해 추출
같은 방식으로 w.tmp도 추출

w.tmp는 어디서 나왔느냐? cmdscan.log 11번째 줄에서 wce.exe -w > w.tmp를 실행하였다.





If need english translation, contact me, thx.<br><br> 


  Volatility - 메모리 관련 데이터를 수집해주는 도구<br><br>
![1](https://github.com/user-attachments/assets/28f69dbf-46ca-4d68-a9f3-8b42185baa13)<br>
command in Windows PowerShell<br>
메모리 덤프를 보고 Volatility가 어떤 운영체제의 메모리 덤프인지 판단 -> 어떤 운영체제인지?에 대한 값이 앞으로의 모든 분석에 사용될 예정<br><br><br>

<br>
![2](https://github.com/user-attachments/assets/a134f40c-3e20-46a2-ae70-dd0c2c58bb6c)<br>
우선, 이전과 같이 imageinfo 명령어를 통해 운영체제를 식별할 예정이다.<br>
![4](https://github.com/user-attachments/assets/2bc2f774-933f-4a1f-b8ee-f999a8a0be16)
<br><br>


![5](https://github.com/user-attachments/assets/02abcbc0-4202-4d78-9991-6cfc3640c096)<br>
일단 각 로그들을 전부 출력하여 준다.<br>

(Windows XP 기준)<br>
connections : '현재' 연결된 TCP 통신에 대한 정보<br>
sockets : 응답 받기를 기다리고 있는 모든 프로토콜에 대한 socket 정보<br><br>

(Windows 7 up 기준)<br>
netscan<br><br>

cmdline : 프로세스가 실행될 때 인자값<br>
cmdscan : 콘솔에 입력한 값들을 실제로 볼 수 있다.<br>
consoles : 콘솔에서 입력 & 출력한 값들을 실제로 볼 수 있다.<br><br><br><br>

의심이 가는 프로세스들을 먼저 나열을 해 볼 건데<br>
![6](https://github.com/user-attachments/assets/4da0ffed-91e1-41a7-a78e-baf10ac8a46b)<br>
TeamViewer -> TeamViewer 관련 악성코드가 존재하기 때문에 하위 3개까지 의심<br>
mstsc -> 내 컴퓨터를 원격에서 수리를 할 때 사용하기 때문에 의심<br>
explorer -> 윈도우 탐색기에서 cmd를 오픈하였기 때문에 의심<br>
outlook -> 메일 관련 악성 코드가 매우 많이 유포되기 때문에 의심<br>
iexplorer -> iexplorer 하위 프로세스에서 cmd가 실행이 되었기에 의심<br>
이 정도가 의심이 된다고 볼 수 있다.<br><br><br>

![8](https://github.com/user-attachments/assets/c79cc436-7b40-4fd8-b7d7-f4cbbaa32b91)<br>
cmdscan 살펴본 결과, wce.exe를 사용해 무언가를 Temp로 빼낸거 같다.<br><br>

![9](https://github.com/user-attachments/assets/45f0bf93-22b5-4c50-8bc3-0b797bd8409e)<br>
+ 관리자로서 cmd 실행해서 다시 해보는 모습도 보인다.<br><br>

추가적으로 살펴봐야 할 내용은<br>
outlook.exe를 살펴봐야하고<br>
tv_w32.exe도 살펴봐야한다.<br><br>

C:\Windows\Temp\wce.exe, w.tmp<br><br><br>

![10](https://github.com/user-attachments/assets/0007722d-f5e2-47c8-b8ba-b7b11a7620a6)
filescan.log에서의 605번째 줄 wce.exe를 dumpfiles을 이용해 추출<br>
같은 방식으로 w.tmp도 추출<br><br>

w.tmp는 어디서 나왔느냐? cmdscan.log 11번째 줄에서 wce.exe -w > w.tmp를 실행하였다.<br><br>

![13](https://github.com/user-attachments/assets/5c88dfc9-515e-474e-a285-3656123a0aca)<br>
위 사진에서 계정 정보와 비밀번호로 보이는 글자를 확인할 수 있었다. wce라는 프로그램이 컴퓨터에 들어와서 관리자 PC의 계정과 사용자 계정의 비밀번호를 추출하였고 w.tmp로 남겨둔 것으로 확인된다.<br><br>

![14](https://github.com/user-attachments/assets/5013b53c-625a-43e6-9919-d037d7401b2c)<br>
이를 바탕으로 VirusTotal(www.virustotal.com)에 wce.exe.dat 파일을 업로드 해 본 결과,
위 사진과 같은 결과가 나왔다.<br><br>


![15](https://github.com/user-attachments/assets/12af3b20-684b-4eda-93a9-1e9466dddde2)<br>
netscan.log를 살펴보는데, mstsc.exe 부분에서 같은 IP를 사용하고 있는데 해당 주소는 공격자의 주소이거나, 컴퓨터에 해커가 이 ip를 거점으로 다른 곳으로 가는 것일 수도 있으니, 해당 IP를 눈여겨보아야 한다.<br><br>

수상한 list들을 정리해보자면,<br>
하위에서 cmd가 실행된 iexplorer.exe와 TeamViewer, outlook.exe가 있겠다.<br><br><br>


![17](https://github.com/user-attachments/assets/8389db98-2fe3-47d1-928c-e5a6e3a21b6a)<br>
filescan.log에서 tv_w32를 검색해 tv_w32.exe의 주소(0x000000003fa4f5d0)를 얻어 -n 옵션을 주어 추출해본다.<br><br>


![18](https://github.com/user-attachments/assets/9d1ea631-5e79-4d28-ac2d-72fd07604e30)<br>
해당 파일을 다시 VirusTotal(www.virustotal.com)에 업로드해보았더니 No security vendors flagged this file as malicious라고 한다. 또한, teamviewer.exe 외 여러가지를 돌려도 전부 같은 문구가 나온다. 그러므로 깨끗했다고 생각하고 넘어가도록 한다.<br><br>

![19](https://github.com/user-attachments/assets/a5fe2387-d8b3-4f49-a5ca-8315b663c45c)<br>
iexplorer도 같은 방식으로 해보면 180.76.254.120이라는 IP 주소를 얻을 수 있고, 이를 통해 AnyConnectInstaller를 다운 받은 흔적을 확인할 수 있지만 그 다음으로 나아가기는 어려워 보인다. <br><br><br><br>


outlook.exe을 다음으로 살펴보자.<br>
outlook.exe를 통해서 메일 -> 메모리 덤프 -> 메일 원본이 있는 지 보고 싶기 때문이다.<br>
메일 원본을 찾기 위해선, url을 위주로 찾아보면 된다.<br><br>

![20](https://github.com/user-attachments/assets/ede6246e-9ae2-4111-9f30-7c495030bfbf)<br>
우선, string.log에 http를 검색해보았더니 1111개의 검색 결과가 나오게 되었다.<br>
1111개의 결과를 전부 다 살펴볼 수는 없으니 URL 주소의 끝에 .exe가 있는 것을 확인해 볼 것이다.<br><br><br>


![21](https://github.com/user-attachments/assets/a60b96af-81fd-404f-969d-2cd5ef9b1e45)<br>
그렇게 해서 찾아낸 결과이다. 사진에서 볼 수 있는 내용은 메일의 html 코드버전인데, 여기서의 ip주소는 이전에 netscan.log에서 단서로 얻어낸 ip 주소와 일치하는 것을 확인할 수 있는 매우 귀중한 단서가 되겠다.<br>


![22](https://github.com/user-attachments/assets/c399c856-71cf-408f-bcd2-4595a4155cae)<br>
http://180.76.254.120/AnyConnectInstaller.exe<br><br><br>


![23](https://github.com/user-attachments/assets/2ef26736-ba0a-490c-9535-e87fe7fe2694)<br>
위 내용을 바탕으로 filescan.log로 가서 AnyConnectInstaller가 다운로드 된 경로를 찾아서 추출을 해본다.<br><br><br>


![24](https://github.com/user-attachments/assets/3fa948e3-28be-49e5-a23f-30214f40bb12)<br>
추출한 결과를 업로드해보니 악성 코드가 맞았다.<br>
해커가 outlook 메일을 통해서 AnyConnectInstaller.exe를 설치하게 하여 wce.exe, w.tmp(관리자 패스워드)가 생겨났고, mstsc.exe가 실행되었을 것이다. 라는 로드맵을 그려볼 수 있다.<br><br><br>

이 과정에서 AnyConnectInstaller.exe에서 wce.exe, w.tmp로 넘어가는 과정과 mstsc.exe로 넘어가는 과정은 리버싱을 통해서 볼 수 있겠지만 이번은 메모리 포렌식이 주이기 때문에 넘기겠다.<br>








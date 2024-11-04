If need english translation, contact me.<br><br> 
  Volatility - 메모리 관련 데이터를 수집해주는 도구<br><br>
  
![8](https://github.com/user-attachments/assets/bb1d2aa7-b74f-4ae9-a7a0-a6d03788940d)<br>
command in Windows PowerShell<br>
메모리 덤프를 보고 Volatility가 어떤 운영체제의 메모리 덤프인지 판단 -> 어떤 운영체제인지?에 대한 값이 앞으로의 모든 분석에 사용될 예정<br><br><br>


![9](https://github.com/user-attachments/assets/c22f94c7-5e3e-404a-b816-fe62f02e9c8f)<br>
WinXPSP2x86


![10](https://github.com/user-attachments/assets/6c62d416-6502-4313-8c5e-9029832c08ab)<br>
volatility -f .\cridex.vmem --profile=WinXPSP2x86 pslist 명령어를 사용한다.<br>
pslist 명령어는 프로세스들의 리스트를 출력하는 역할을 한다.<br>

![11](https://github.com/user-attachments/assets/8c30e806-9904-4380-8f2f-68166c95eaf2)<br>
출력 화면<br><br><br>

![12](https://github.com/user-attachments/assets/bf3d32a9-46ef-47de-9543-3cb52762dd83)<br>
pslist를 pslist.log 파일로 출력하여 Notepad++ 프로그램을 통해서 확인하는 화면<br>
사진에서 보이는 각 .exe 파일들은 프로세스들을 나타내고 있다.<br><br><br>

![13](https://github.com/user-attachments/assets/65baed9a-bfdc-4523-975b-1d668a0b718a)<br>
pslist, psscan, pstree, psxview 모두 log로 출력한 상태이다.<br>
pslist는 현재 작동중인 모든 프로세스들을 출력해준다. Offset 주소와 PID, PPID 등과 같은 정보도 함께 출력된다.<br>
psscan은 풀 스캐너를 통하여 프로세스를 출력해준다. 따라서 종료된 프로세스나 비활성화된 프로세스, 루트 킷에 의해 숨겨지거나 연결이 끊긴 프로세스를 찾을 수 있다.<br>
pstree는 각 줄의 offset 주소 왼쪽에 .을 통하여 프로세스를 트리 형식(PID, PPID 기반으로 구조화)으로 나타내준다. 상위, 하위 프로세스를 한 눈에 확인할 수 있으며 상위 프로세스가 없는 프로세스 위주로 분석하면 악성 프로세스를 쉽게 찾아낼 수 있다.<br>
psxview는 다양한 프로세스 리스트로 숨겨진 프로세스를 찾아준다. pslist는 Ture이지만 psscan은 False인 프로세스를 찾으면 해당 프로세스가 숨겨진 프로세스인 걸 확인할 수 있다.<br><br><br>


![14](https://github.com/user-attachments/assets/d019d9ff-75c4-44f7-bd7b-4ad70276c5c8)<br>
각 프로세스는 구글링을 통해서 어떠한 역할을 하고 있는 프로세스들인 지 확인해 볼 필요가 있다. 다만 악성 프로세스도 이름을 변조하는 경우도 있으니 주의해야 한다.(이 경우는 뒤에서 또 다른 단서를 찾는 과정을 보여줄 예정)<br><br>

사진에서 마지막 줄의 reader_sl.exe 프로세스는 Adobe Acrobat 소프트웨어 구성 요소라고 구글링을 통해 알아봤다. Adobe -> PDF 문서를 읽는 데 주로 사용되는데 PDF는 관련 악성 코드가 많으니 의심해본다.<br><br>

pslist.log에 등장하는 reader_sl.exe 밑에 존재하는 alg.exe나 wuauclt.exe 프로세스도 reader_sl.exe 프로세스에서 파생되었을 수도 있으니 충분히 의심을 할 만 하다.<br><br><br>


![16](https://github.com/user-attachments/assets/f046543e-c607-41ff-8a20-0f7311cf9ec6)<br>
cmdline(프로세스가 실행될 때 인자 값을 확인할 수 있다.), cmdscan, consoles를 각각 출력을 해보았는데 cmdline을 제외한 cmdscan, consoles에서는 아무것도 찾아볼 수 없는 빈 상태였으며 cmdline에서도 의심을 했었던 reader_sl.exe 프로세스 항목에서 의심될만한 것을 찾지 못하였다.<br><br><br>

![17](https://github.com/user-attachments/assets/3a5b48a0-7774-4a49-8353-434e0cb154dd)<br>
그렇기에 다음 단계로, filescan을 출력해보기로 하였다. filescan은 메모리 내에 존재하는 모든 파일에 대한 정보를 보여준다.<br>
의심했던 reader_sl.exe 프로세스의 offset을 복사하여<br>

![18](https://github.com/user-attachments/assets/110ccbe6-ee1e-4d8a-b69c-7433148d05b1)<br>
files라는 폴더를 만들고 명령어를 입력하면 다음과 같은 파일 2개가 생성된 것을 확인할 수 있다. 의심이 됬던 프로세스를 따로 뽑아두는 작업이다.<br><br>
![19](https://github.com/user-attachments/assets/85dcea9c-cc63-4ecd-ae6d-3375e439bdd0)<br>
그렇게 얻어낸 파일을 virustotal이라는 사이트(https://www.virustotal.com/gui/home/upload)에 업로드를 해본다.<br><br>

![20](https://github.com/user-attachments/assets/466fd6a2-53ed-43c2-86e2-0613464e4e5f)<br>
바이러스를 식별해 낸 대부분의 백신 프로그램들이 트로이 목마라고 한다. ㅋㅋ<br><br>

혹여나 바이러스를 식별해 낸 프로그램들이 적을 경우를 대비해 connections.log를 뽑아내고자 한다. connections에서는 연결된 TCP 통신을 출력할 수 있다.<br>
![21](https://github.com/user-attachments/assets/7a7c2833-077a-4fef-9c3c-a42ba82b99e4)<br>
그럼 그렇지, 원래라면 조금 더 내용이 많았어야 하는데 달랑 하나가 이정표마냥 존재하고 있다. 안 따라갈 수가 없다.<br>
참고로 Local Address는 우리가 분석하고자 하는 PC의 주소이며 Remote Address는 원격지 주소이다. Local Address와 Remote Address가 서로 8080이라는 포트를 통해 통신을 하고 있고, 1484라는 프로세스에서 진행하고 있는 것이다.<br>
pstree.log에서 확인한 1484 프로세스는 explorer.exe이며 이는 reader_sl.exe 파일의 바로 위에 위치하고 있다.<br><br>

![22](https://github.com/user-attachments/assets/0c5079a8-5ea0-468f-89e8-a5373b7c814a)<br>
위 명령어를 입력함으로 인해 1640.dmp라는 파일의 이름으로 덤프 파일이 생성된 것을 확인할 수 있다.<br>
덤프 파일을 HxD를 이용해 확인해보면 쓸모 없는 값들이 매우 많은데 그러한 값들을 제거하기 위해<br>
![23](https://github.com/user-attachments/assets/65b92081-dd1f-4ea2-a553-f5fb022aa73d)<br>
다음과 같은 명령어를 입력해준다.(혹시라도 strings가 안되는 분들은 환경 변수에 Sysinternals Suite 추가해주세요.) <br><br>

메모리 dump 내에서 찾아볼 것은 바로 Remote Address인 41.168.5.140이다. 왜냐하면 의심을 하고 있는 reader_sl.exe 프로세스가 해당 주소와 통신을 하는 것으로 보이기 때문이다.<br>

![24](https://github.com/user-attachments/assets/255678d7-e1fc-474c-99c5-fde619f9196d)<br>
이상한 IP 주소들이 나오고 악성 프로그램 관련 주소인 것으로 추정이 된다.<br>
reader_sl.exe 프로세스를 통해서 악성 PDF 문서를 읽었고 그 취약점으로 인해서 해당 URL로 접속을 했을 것이다. 라고 추측할 수 있다.<br><br>

![25](https://github.com/user-attachments/assets/080ad6ec-af51-4bb3-b651-2858fe1df924)<br>
도중에는 인터넷을 접속한 흔적도 보인다.<br><br><br>

![26](https://github.com/user-attachments/assets/d4905627-79ce-464c-b8b8-246d84329f0e)<br>
반복적으로 보이는 문자를 통해 검색해 본 결과 많은 사이트 주소가 눈에 띄는데 전부 은행 관련 주소인 것으로 보아 은행 피싱 언저리 정도로 추정할 수 있다.<br><br>

![27](https://github.com/user-attachments/assets/077bf590-5830-4d0c-b1db-77a69db96e9f)<br>
다음으로는 procdump를 진행할건데, procdump는 프로세스 리스트에서 1640 PID를 갖는 reader_sl.exe 프로세스가 있는데 이것을 파일 offset에서 뽑아내는 것이 dumpfiles 방식이고 프로세스 내부에서 직접 뽑아내는 것이 procdump 방식이다. 즉 실제로 실행이 되었던 .exe 파일이다. 존재하는 .exe 파일을 뽑아내는 것인지, 실행되었던 .exe 파일을 뽑아내는 것에 차이가 있다.<br><br><br>

![28](https://github.com/user-attachments/assets/70dcc2da-75ce-444a-b237-2ac22c6e642f)<br>
virustotal 사이트에 procdump를 통해 뽑아내었던 executable.1640.exe 파일을 VirusTotal에 업로드 해보면 이전에 올렸던 과는 확연한 차이를 볼 수 있다.<br><br><br>

![29](https://github.com/user-attachments/assets/328f8aee-7d9b-4911-b806-e8cb832ec203)<br>
사진과 같이 6개의 exe parents가 존재하고, 9개의 연결된 도메인이 있는 등 다양한 정보를 볼 수 있다.<br><br>

nice



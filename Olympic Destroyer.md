**Brought a memoery analysis example about Olympic called 'Olympic Destroyer' cuz its 2024 Paris Olympics Season. Support Korea :V**<br><br>

Outline : On September 24, 2018, the day before the opening ceremony of the 2018 PyeongChang Olympics, An e-mail arrived to Mr OOO, the organizing committee & the ticket manager. E-mail saying that Olympic Games schedule has been updated. This is the content.<br><br>

Mr.OOO checked 'Olympic_Sesson_V10' in the e-mail and posted the schedule on the website after.<br>
The next day, the PyeongChang Olympics official website server was shut down, and PCs at the site were shut down one after another.<br>
An accident occured. The security team first dumped the momery of the PC that were presumed to be infected immediately after the incident.<br><br>

![image](https://github.com/user-attachments/assets/40021a4b-e70d-432d-85d3-d95d2c88f0a2)<br>
(If need translation, contact me.)<br><br>

**Mail Content**<br>
Hello, This is the Pyeongchang Olympic Oranizing Committee.<br>
The Olympic Games schedule Updated as of Ver. 10 on 9/23.<br>
Please check the contents of the attached file and notify everyone who has reserved tickets.<br>
Game date, start time, and end time of the ticket you purchased from the [Game/Price Information] menu on the ticket website.<br>
You can check the details of changes to the game schedule.<br>
The password for the attached file is pyeongchang2018.<br>
Thank you.<br>
-Pyeongchang Olympic Organizing Committee-<br><br><br>

**Clue from upside**<br>
Olympic_Session_V10이라는 첨부파일<br>
메일을 통한 감염<br><br><br>

What's we gonna do?<br>
imageinfo<br><br>

pslist<br>
psscan<br>
pstree<br>
psxview<br><br>

cmdline<br>
cmdscan<br>
consoles<br><br>

netscan<br><br>

dumpfiles<br>
procdump<br>
memdump<br><br>

Virustotal<br>
strings<br><br><br>

//This file requires only 2gb ram.<br>
![2](https://github.com/user-attachments/assets/84c1892f-f5e0-4f5f-b9d8-19f9d6734618)<br>
imageinfo 명령어를 통해서 확실한 윈도우 버전 알아내기.<br><br>


![3  pstree check](https://github.com/user-attachments/assets/9830633b-ddc7-44e4-a8cf-cd03a4a69431)<br>
pstree.log에서 OlympicDestroyer라는 프로세스가 대놓고 존재하기 때문에 바로 의심하고 시작하자.<br>
powershell을 통해서 OlympicDestroyer가 트리거 되었다고 하는데 위에서 차례대로 실행이 된 것으로 보인다.<br><br>

tree 관계를 보게 되면, OlympicDestroyer가 _xut.exe, teikv.exe, ocxip.exe를 모두 낳았기 때문에 전부 의심해야한다.<br>
즉, OlympicDestoyer라는 프로세스가 3개의 프로세스를 낳아서 각각의 프로세스가 악성 행위를 하는 것으로 보인다.<br><br>

모든 프로세스를 검색해보자<br>
msdtc.exe -> Distribute Transcation?이라고 나온다. 잘 모르겠다.<br>
svchost.exe -> 서비스 호스트는 넘긴다.<br>
dwm.exe -> 데스크톱 창 관리자. 넘긴다.<br>
OSPPSVC.exe -> 마이크로소프트 소프트웨어 프로덕션 플랫폼... 엑셀을 통한 침입이라고 했으니 마이크로소프트 오피스 관련이면 의심해야 한다.<br>
taskeng.exe -> 작업 스케줄러 서비스라고 한다. 악성 코드들이 컴퓨터에 들어온 다음에 본인 파일을 작업 스케줄러에 등록을 해놓고 지속적으로 컴퓨터에서 실행이 되기 위한 경우가 있기 때문에 의심한다.<br>
나머지는 크게 없어보인다.<br><br>

pslist.log에서는 WmIPrevSE.exe가 실행이 되고 poweshell.exe를 낳는데 9시간 정도 차이가 있어 보인다.<br>
![image](https://github.com/user-attachments/assets/a5ee6c7d-870a-4019-8b17-2f6e7e6a3d58)<br>
OSPPSVC.exe가 파워쉘과 굉장히 인접한 시간에 실행이 되고 있다. 즉, 문서 악성코드가 파워셸을 실행했다고도 볼 수 있겠다.<br><br>

powershell과 conhost가 똑같이 실행이 되는데 그 후에 한 19시간 이후에 OlympicDestroyer가 실행이 되고 ocxip.exe와 teikv.exe, _xut.exe 프로세스가 실행이 되고 있는 모습이다. <br><br>

그 후에 taskeng.exe, cmd.exe, conhost.exe가 실행되는 모습이다.<br>
시간 텀이 있는게 특이한 부분이다.<br>

psscan.log는 출력이 되지 않았으니 닫고 넘어가도록 한다.<br>
psxview도 마찬가지이다.<br><br>

netscan.log에서는 파워셸이 안 나와있고 외부 IP도 나와있지도 않다. 마지막에 powershell.exe가 나와있지만 얻을 수 있는건 많이 없다. 컴퓨터의 IP는 192.168.111.130으로 추정이 된다.<br><br>

192.168.111.128이라는 IP도 보이는데, 이것이 같은 서버의 컴퓨터에서 공격이 들어왔다는 것인지 아니면 해커가 들어와서 이 컴퓨터를 통해서 다른 컴퓨터로 침투를 했다는 것인지가 명확해 보이지 않는다.<br><br>

cmdline.log에서 의심스러워했던 프로세스 위주로 살펴보아야 한다.<br>
![5](https://github.com/user-attachments/assets/c7b61320-c5d3-45a3-9482-d2a911a87fbf)<br>

powershell도 실행될 때 커맨드가 비어있고, OlympicDestroyer3이라는 경로가 일단 확인할 수 있다.<br>
**C:\Windows\System32\OlympicDestroyer3.exe**<br><br>

_xut.exe도 경로를 확인 할 수가 있었다.<br>
**C:\Users\VM\AppData\Local\Temp\_xut.exe**<br><br>

consoles.log에서는 conhost.exe라는 프로세스가 cmd 라인으로 파워셀을 실행한 걸 볼 수 있다.<br>
pslist.log에서 conhost.ext는 powershell.exe와 동일하게 실행되었는데, conhost라는 프로세스는 crcsrss.exe 프로세스가 실행을 한 것을 확인할 수 있다.<br><br>

crcsrss.exe -> 클라이언트 서버 런타임 프로세스라고 윈도우에서 기본적으로 동작하는 프로세스라고 나와있다.<br><br>

콘솔호스트라는 친구가 위의 powershell 등 프로세스들을 트리거 하지 않았을까? 생각 할 수 있다.<br><br>

filescan.log에서는 OlympicDestryoer 경로를 다운해서 추출한다.<br>
![7](https://github.com/user-attachments/assets/c4d9b19e-1fd1-4210-8e10-07b90d8120d4)<br>
_xut도 마찬가지이다.<br><br>

추출해낸 두 exe 파일을 VirusTotal(www.virustotal.com)에 업로드해보자.<br>
![8](https://github.com/user-attachments/assets/e81fbc4d-3c4e-4b79-8ae1-b7f9738120db)<br>
![9](https://github.com/user-attachments/assets/19b478a3-3ca4-4779-94df-1938e527ec20)<br>
PC에서 자동으로 저 친구들을 삭제해서 올리느라 애먹었다...ㅋㅋㅋ<br><br><br>


즉, _xut.exe와 OlympicDestroyer.exe는 악성 프로세스로 체크하고 넘어가면 될 것 같다.<br><br>

다음 프로세스인 teikv.exe와 ocxip.exe도 procdump 명령어를 사용해본다.<br>
위 2개는 paging 오류가 뜨는데 filescan.log에 가서 검색을 해서 각각의 오프셋을 얻은 뒤, 이것을 dumpfiles를 통해 뽑아 볼 것이다.<br>
![10](https://github.com/user-attachments/assets/9e0faaf2-f7d0-4396-8397-ca1686303eba)<br><br>


다음으로 taskeng.exe와 conhost.exe도 시도해본다.<br><br>

전부 VirusTotal(www.virustotal.com)에 업로드를 해보자면,<br>
![620](https://github.com/user-attachments/assets/b7caa38e-9630-45f3-aa3d-728b1e46574d)<br>
620.exe이다.<br><br>

![1700](https://github.com/user-attachments/assets/67e20a98-7785-4bff-b0f8-0e3046c7d049)<br>
1700.exe이다.<br><br>

![2192](https://github.com/user-attachments/assets/61603591-bfe0-4a29-b3c1-61fc7e29f6e5)<br>
2192.exe이다.<br><br>

![ocxip](https://github.com/user-attachments/assets/86e2e15c-1e55-4953-ab56-bcb9a35f4183)<br>
ocxip.exe이다.<br><br>

![teikv](https://github.com/user-attachments/assets/40736c56-c82f-4a99-af3b-173b9b9935df)<br>
teikv.exe이다.<br><br>

620번, conhost는 6개의 프로그램에서 악성코드라고 나왔으며 1700번, OSPPSVC은 아니다. 2192번인 taskeng도 제외.<br>
ocxip.exe와 teikv.exe는 악성코드가 확실시되는 모습이다.<br><br>

**Virustotal 사용 시 주의사항**<br>

1. 압축하여 파일을 업로드 할 경우 가장 범용성있는 ZIP 확장자 파일을 권장한다..<br>
    하지만 특정한 경우를 제외하고는 압축을 하지 않고, 단일 파일로 검사를 하는 것이 가장 좋다.<br><br>
 
2. 압축을 할 경우 하나의 파일만을 압축해서 검사해야 한다.<br><br>
 
3. 한번 검사를 진행한 경우에도, 시간이 오래 지났다면 주기적으로 재검사를 해야한다.<br><br>
 
4. 바이러스 토탈의 검사 결과를 맹신하지 말아야 한다.<br><br>
 
5. 바이러스 토탈에 업로드된 파일은 커뮤니티에 공개가 되기 때문에 기밀 또는 민감한 정보는 절대 올리시면 안된다.<br><br>
 
Virustotal 을 통한 분석 방법<br><br>

악성 코드 분석에는 총 3가지 방법이 있다.<br>
- 기초 분석<br>
- 정적 분석<br>
- 동적 분석<br><br>

Virustotal 의 경우 기초 분석 영역에 사용된다.<br>
악성 코드에 대한 기초적인 정보를 모으는 단계이며, 해당 악성 코드의 특징적인 부분을 파악한 후 뒤에 정적 분석, 동적 분석에 방향성을 결정하는 역할을 한다.<br>
출처: https://maker5587.tistory.com/12 [Maker's security:티스토리]<br><br><br>


위 OlympicDestroyer에서 알 수 있는 건, 악성 프로세스들이 정상적인 프로세스들을 이용해서 동작을 하기도 한다.<br>
명령 프롬프트, cmd를 이용해서 악성 코드를 입력한다고 해서 cmd 자체가 악성 프로그램이 되는 것이 아니라 그 안에서 어떤 명령어를 입력을 했는 지를 확인하는 것이 중요하다.<br><br>


현재 진행상황을 보자면, 4개의 악성 프로세스들을 발견하였지만 어느 경로를 통해서 들어왔는가, 어떠한 공격행위를 하는가를 확인해 볼 필요가 있겠다.<br><br>

다시 처음으로 돌아가서 중요한 단서 중 하나가 뭐였냐면, 바로 'Olympic_Session_V10'이라는 엑셀 파일(.xls)이다.<br>
엑셀은 오피스 파일이므로 오피스 관련 프로세스인 OSPPSVC.EXE를 먼저 메모리 덤프를 해볼 것이다.<br>
![11](https://github.com/user-attachments/assets/0ee6d0fc-52bb-4b72-b181-9c61c7566912)<br><br><br>

추가적으로 기존에 발견했던 4개의 악성 프로세스들 또한 strings를 해볼 예정이다.<br>
OlympisDestroyer.log를 살펴보면 2784번째 줄에서 공격스크립트로 보이는 줄이 보인다.<br><br>

![12](https://github.com/user-attachments/assets/949166e1-4b5e-4b7d-afc2-f0e974e38332)<br>
Wsciprt = 윈도우 스크립트이며 DeleteFile = 무언가를 삭제하고 GetObject를 해서 뭐시기뭐시기...<br>
OlympicDestroyer는 공격 스크립트 구문을 포함하고 있다는 사실을 알 수 있었다.<br><br>

밑에 줄에 보면 %s\root\directory\LDAP 라는 경로가 존재하는데 LDAP가 컴퓨터가 어떤 네트워크 집단에 소속되어 있을 때, 그 집단을 관리하는 프로토콜 중 하나이기 때문에 공격자는 LDAP를 통해서 내부 네트워크를 사용하고 침입했다고 추정이 된다.<br>
SELECT ds_cn FROM ds_computer 구문은 SQL 구문인데 내부 네트워크에 대한 정보를 불러오는 구문이 아닐까 생각이 된다.<br><br>

쭉 내리다보면 계정과 어드민, 패스워드 등과 같은 정보들도 보인다.<br><br><br><br>

oxcip.exe.log 내부에서도 눈여겨볼만한 내용은 존재하지 않는다.<br>
teikv.exe.log도 마찬가지.<br><br>

![image](https://github.com/user-attachments/assets/0295b040-b110-4aeb-be0d-15a212e11297)<br>
다만, xut.exe.log를 살펴보게 되면 cmd를 실행을 해서 명령어들을 실행하고 있다.<br>
SeShutdownPrivilege는 종료 관련 api를 사용하기 위해서 권한을 지정해주는 것으로 구글에서 말해주고 있다.<br>
그 밑의 줄에서 vssadmin.exe가 보이는데, 현재 볼륨 섀도 복사본 백업 및 설치된 모든 섀도 복사본 기록기 및 공급자를 표시하는 역할을 한다.<br>
그런 vssadmin를 전부 delete shadows /all 하고 있다는 것이다.<br>
컴퓨터가 복구가 안되도록 모두 지워버리는 것이다.<br>
wbadmin은 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 응용 프로그램을 백업 및 복원할 수 있는 명령이다.<br>
wbadmin이라는 명령어 또한 delete catalog -quiet 명령어를 통해 카탈로그들을 다 지워버리고 있다.<br><br>

bcdedit은 부팅 로더 관련된 명령어인데 실패들은 다 무시해버리고 recovery를 no로 만들어버리고 있다.<br>
부팅 관련 복구 기능을 전부 no 설정으로 바꿔버리고 있는 것이다.<br><br>

밑에 줄에는 cl System과 cl Security라는 명령어가 있는데 event-log, 시스템 이벤트 로그와 시스템 보안 이벤트 로그를 전부 지워버리겠다라는 내용이다.<br><br>

위 사진이 즉 공격 코드이고 알 수 있었던 점은,<br>
s_xut.exe -> 공격코드 존재(복구 관련 기능을 삭제, 부팅 관련 기능을 불가하게 만들며 이벤트 로그를 삭제)<br>
OlympicDestroyer.exe -> LDAP, 계정, 패스워드를 통해서 네트워크 망에 있는 다른 컴퓨터들로부터 무언가 공격을 이어나감<br><br><br>


마지막으로 남은 분석은 이 악성코드가 어디에서 들어왔는 것인가에 대해서 분석을 해봐야 한다.<br><br><br>
OSPPSVC는 마이크로소프트 오피스 관련 관리하는 프로세스인데, memdump한 것을 string하여 얻어낸 OSPPSVC.exe.log를 분석해보자.<br><br>

![image](https://github.com/user-attachments/assets/9958d256-6bb0-4b35-a615-01b91a9ff6ef)<br>
엄청나게 많은 줄이 있다. 일일이 내려서 확인을 해도 되겠지만, 위에서 얻은 단서들을 이용해보자.<br>
공격자가 첨부파일 'Olympic_session_V10'을 이용했다는 것이다. 이를 검색해보면, <br>
Users/VM/Desktop/oLYMPIC_sESSION_V10_이라는 파일이 .xls 형태로 존재했던 거승로 보아, 엑셀 파일이 데스크탑에 있었던 것은 확실해 보인다.<br><br>

filescan.log에서 검색을 해보니 partial로 나뉘어진 zip파일과 xls 파일이 존재한다.<br>
![image](https://github.com/user-attachments/assets/d6078d9c-37f5-43ae-b9d5-693a84ccbe2a)<br>
이 친구를 dumpfiles를 해준다.<br>
혹시나 에러가 생긴다면 중간에 '수정본'이라는 한국어가 있어서 안되는데 의도치 않게 'Olympic_session_V10_수정본_xls'이라는 파일 명을 알아내게 되었다.<br>
이 친구를 수정하면서 OSPPSVC가 실행이 되고 이쪽 프로세스 관련으로 인해 OlympicDestoyer가 나온 것으로 보인다.<br>
메모리 포렌식을 통해서는 위와 같은 내용들을 얻어낼 수 있었다.<br>
추가적으로 분석 가능한 부분들은<br>
- memdump -> strings<br>
    payload(BASE64)<br>
- 네트워크 -> LDAP.<br>
정도가 있겠다.<br>

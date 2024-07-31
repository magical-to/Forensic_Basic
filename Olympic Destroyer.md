**Brought a problem about olympic called 'Olympic Destroyer' becuz its 2024 Paris Olympics Season. Support Korea :V**<br><br>

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


























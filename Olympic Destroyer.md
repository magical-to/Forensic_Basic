![image](https://github.com/user-attachments/assets/edf1d839-49bb-487a-9ac0-f849b84ab474)**Brought a problem about olympic called 'Olympic Destroyer' becuz its 2024 Paris Olympics Season. Support Korea :V**<br><br>

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

















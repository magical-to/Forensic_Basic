- 레지스트리 파일 추출<br>
- FTK Imager 이용<br>
  - [root]\Windows\Users\{USERNAME}\NTUSER.DAT<br>
  - [root]\Windows\System32\config\DEFAULT<br>
  - [root]\Windows\System32\config\SAM<br>
  - [root]\Windows\System32\config\SECURITY<br>
  - [root]\Windows\System32\config\SOFTWARE<br>
  - [root]\Windows\System32\config\SYSTEM<br>
  - 반드시 LOG1, LOG2 파일을 포함해서 추출<br><br>
 
- registry라는 폴더를 만들어서 clean, raw, result 폴더를 각각 생성한다.<br>
- 레지스트리가 각각의 로우 상태가 있고 클린으로 만들어서 클린으로 리조트를 뽑아내야한다.<br>
- 로우 상태로 데이터를 수집을 하면 'dirty'하다고 표현을 한다. 윈도우가 파일에 바로 쓰는 것이 아니라 바로 쓰기 전에 어떤 로그 파일들을 만들어서 써두는데 수집을 할 때 파일뿐만 아니라 로그 파일을 함께 수집을 한다. 로그 파일에 써진 내용들을 원래 파일에 병합을 해서 합쳐줘야 클린한 파일이 나오는 것이다.<br><br>


![20240806_162301](https://github.com/user-attachments/assets/facac0ca-19e4-4ebb-a64c-9eaa122933ed)<br>
NTUSER.DAT와 LOG1, LOG를 뽑아내는 모습이다.<br>
Windows에서는 DEFAULT, SAM, SECURITY, SOFTWARE, SYSTEM과 각각의 LOG1, LOG를 뽑아내면 되겠다.<br><br>

**분석 도구 다운로드**<br>
REGA : http://forensic.korea.ac.kr/tools.html<br>
RLA : https://ericzimmerman.github.io/#!index.md<br>
Regripper : https://github.com/keydet89/RegRipper3.0<br><br>

![1](https://github.com/user-attachments/assets/a91b4da0-49df-4815-ba9f-c07f2e9aad04)<br>
REGA를 통해 레지스트리 파일을 분석하는 모습<br><br>

![image](https://github.com/user-attachments/assets/ce9f7766-6391-433f-b6db-95b85651b735)<br>
도구 상자에서 다양한 옵션을 사용할 수 있다.<br><br>

![2](https://github.com/user-attachments/assets/a5afc511-408a-4c68-a962-52e355d2fc75)<br><br>

![image](https://github.com/user-attachments/assets/340c628c-b90d-446b-a29b-989952df8d9e)<br>
rla를 할 때 d 옵션 아래에는 폴더를 주면 되고 아웃 옵션 아래에는 만들어질 아웃 폴더를 주면 된다.<br><br>

raw에 있는 dirty한 레지스트리를 clean으로 넣을 것이기 때문에<br>
![5](https://github.com/user-attachments/assets/01b23f79-5f43-4c12-a5c4-2d799acd754b)<br>
위 사진과 같이 명령어를 입력해주면 된다.<br><br>

Regripper는 github에서 <> Code를 누르고 Download Zip을 눌러 다운로드를 받으면 된다.<br>
rr.xxe를 사용할 건데, 하이브 파일을 업로드 해줄 것이다.<br>
![image](https://github.com/user-attachments/assets/53edcea2-c756-4840-b005-92a68a9a7add)<br>
Hive 파일에는 위에서 rla로 뽑아낸 clean 파일을 넣은 뒤에 Report File를 설정하고 Rip! 버튼을 누르면 된다.<br>
나온 파일들은 notepad를 이용하여 데이터를 찾아볼 수 있다.<br>
regripper 플러그인이라고 검색을 하면 설명이 전부 다 나와있다.<br><br><br>


**$LogFile**<br>
저널링(Jounaling)<br>
• 데이터 변경을 디스크에 반영하기 전에 행위를 기록하여 추후 오류 복구에 활용<br>
  • 데이터를 기록하는 동안 시스템에 문제가 생기면 데이터가 손실됨<br>
  • 문제가 발생하기 전에 “어떤 데이터를, 언제, 어디에 쓰는지” 기록<br>
  • 문제가 발생하면 기록을 토대로 작업이 이루어지기 전 상태로 시스템을 복원<br><br>

트랜잭션(Transaction)<br>
• "쪼갤 수 없는 업무 처리의 최소 단위”<br>
• 파일이나 디렉토리 생성, 수정, 삭제, MFT 레코드 변경 등
• $LogFile: 메타데이터의 트랜잭션 저널 정보

**$UsnJrnl**<br>
• 파일이나 디렉토리에 변경 사항이 생길 때 이를 기록하는 로그 파일<br>
• 파일 복원의 목적이 아니라, 단순 파일 작업이 있었다는 사실을 확인하기 위함<br>
• 시간 순서대로 엔트리를 저장하고, 기본 크기는 32MB<br>
• 하루 8시간 사용시 4~5일 정도의 데이터를 저장하고 있음<br><br>

![image](https://github.com/user-attachments/assets/255529be-ff7d-4ae9-a27e-cbcdb266959a)<br>
우선, FTK Imager를 통해 root에서 $logFile과 root/$Extend/$UsnJrnl/$J 파일을 추출해낸다.<br>
NTFS Log Tracker를 이용해 로그파일과 J파일, MFT 파일을 넣어준다.<br>
![1](https://github.com/user-attachments/assets/b2efd7c2-ff93-40aa-b313-67e160e1c5d4)<br>
(UI가 깨지는 건 모두가 똑같다...)<br><br>

Parse를 누르고 결과로 생성될 DB의 이름을 설정한 후, Path는 알아서 설정하면 된다.<br><br>

![2](https://github.com/user-attachments/assets/48020a00-dae9-4fb3-be68-99397d2954c0)><br>
그렇게 뽑아낸 db 파일을 DB Browser for SQLite에 업로드한다.<br>
로그 파일과 UsnJRnl을 넣었기 때문에 각각에 대한 분석 데이터가 생성되어 있는 걸 확인할 수 있고, 로그 파일로부터는 EventTime도 확인할 수 있다.<br>
파일이 삭제되었다거나 데이터를 썼다와 같은 파일을 기록하고 썼던 데이터들을 전부 확인할 수 있다.<br><br><br>


**바로가기(LNK)**<br>
• 'Windows Shortcut’<br>
• .lnk 확장자<br><br>

생성하는 방법
• 사용자가 직접 생성<br>
• 프로그램 설치 시에 생성<br>
• 운영체제가 자동으로 생성<br><br>

바탕 화면<br>
• %UserProfile%\Desktop<br><br>

시작 메뉴<br>
• %ProgramData%\Microsoft\Windows\Start Menu<br>
• %UserProfile%\Appdata\Roaming\Microsoft\Windows\Start Menu<br><br>

최근 실행<br>
• %UserProfile%\AppData\Roaming\Microsoft\Windows\Recent<br><br>

빠른 실행<br>
• %ProgramData%\Microsoft\Internet Explorer\Quick Launch<br>
• %UserProfile%\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch<br>
• %UserProfile%\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\User<br>
Pinned\TaskBar<br><br>

FTK Imager 이용하여 추출<br>
• %UserProfile%\Desktop<br>
• %UserProfile%\AppData\Roaming\Microsoft\Windows\Recent<br><br>

LECmd 이용하여 분석<br>
• https://ericzimmerman.github.io/#!index.md<br><br>

![image](https://github.com/user-attachments/assets/c93a7c96-2e51-4e79-a412-ee7955d74099)<br>
아무 간단한 실행파일을 FTK Imager를 통해 추출을 해놓는다.<br>
.\LECme.exe를 입력하면 사용법이 나온다.<br>
-f 옵션이나 -d 옵션 중 하나가 있어야 한다. -d는 Recursively, 폴더 아래에 있는 모든 폴더 안에 파일들을 샅샅이 뒤져서 전부 하겠다.<br>
즉, -d 옵션 아래에는 디렉토리, -f 옵션 아래에는 파일을 주면 된다.<br><br>


.\LECmd.exe -f '.\파일.exe - 바로 가기.lnk' 명령어를 입력하게 된다면,<br>
![1](https://github.com/user-attachments/assets/91fdaed5-cc3e-4fc4-8cb3-94607cd006d0)<br><br>

위 사진이 전부를 담고 있진 않지만, 나온 내용들 일부를 보면, Source File에서 Source라는 것은 우리가 입력한 해당 파일을 Source File이라고 부른다.<br>
Source File이라는 것은 우리가 분석하고자 하는 바로가기 파일 자체를 의미하는 것이고, 이 바로가기가 원본 파일을 가리키고 있기 때문에 원본 파일에 대한 생성시간, 수정시간, 접근시간을 담고 있다.<br><br>

File Size 또한 원본 파일의 크기를 의미하는 것이고 상대적 경로와 절대적 경로는 다른 경로에 있는 것을 확인할 수 있다.<br><br>

• %UserProfile%\AppData\Roaming\Microsoft\Windows\Recent 위치에서 Recent 폴더도 추출을 한 뒤,<br><br>

.\LECmd.exe -d .\Recent\ --html "추출할 폴더 주소"<br>
xHTML파일이 있는데 해당 파일을 클릭하면 모든 것들이 분석이 되어서 정리가 되어있는 모습을 확인할 수 있다.<br>
개인정보 상, 각자가 해보기로 하자.<br><br>

.\LECmd.exe -d .\Recent\ --csv "추출할 폴더 주소"<br>
csv 형태로도 뽑아볼 수 있는데, 엑셀로 열어주면 정리되어 있는 모습을 확인할 수 있다.(엑셀 파일이 깨져있다면 데이터-데이터 가져오기를 통해서 데이터를 가져오면 정상적으로 나오게 된다.)<br><br>















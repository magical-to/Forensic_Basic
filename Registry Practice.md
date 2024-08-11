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
regripper 플러그인이라고 검색을 하면 설명이 전부 다 나와있다.<br>














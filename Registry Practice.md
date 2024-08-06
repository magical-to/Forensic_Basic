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














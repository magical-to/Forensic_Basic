  Volatility - 메모리 관련 데이터를 수집해주는 도구<br><br>

  ![8](https://github.com/user-attachments/assets/bb1d2aa7-b74f-4ae9-a7a0-a6d03788940d)
command in Windows PowerShell<br>
메모리 덤프를 보고 Volatility가 어떤 운영체제의 메모리 덤프인지 판단 -> 어떤 운영체제인지?에 대한 값이 앞으로의 모든 분석에 사용될 예정<br><br><br>

![9](https://github.com/user-attachments/assets/c22f94c7-5e3e-404a-b816-fe62f02e9c8f)
WinXPSP2x86


![10](https://github.com/user-attachments/assets/6c62d416-6502-4313-8c5e-9029832c08ab)
volatility -f .\cridex.vmem --profile=WinXPSP2x86 pslist 명령어를 사용한다.<br>
pslist 명령어는 프로세스들의 리스트를 출력하는 역할을 한다.<br>

![11](https://github.com/user-attachments/assets/8c30e806-9904-4380-8f2f-68166c95eaf2)
출력 화면<br><br><br>

![12](https://github.com/user-attachments/assets/bf3d32a9-46ef-47de-9543-3cb52762dd83)
pslist를 pslist.log 파일로 출력하여 Notepad++ 프로그램을 통해서 확인하는 화면<br>
사진에서 보이는 각 .exe 파일들은 프로세스들을 나타내고 있다.<br><br><br>

![13](https://github.com/user-attachments/assets/65baed9a-bfdc-4523-975b-1d668a0b718a)
pslist, psscan, pstree, psxview 모두 log로 출력한 상태이다.<br>
pslist는 현재 작동중인 모든 프로세스들을 출력해준다. Offset 주소와 PID, PPID 등과 같은 정보도 함께 출력된다.<br>
psscan은 풀 스캐너를 통하여 프로세스를 출력해준다. 따라서 종료된 프로세스나 비활성화된 프로세스, 루트 킷에 의해 숨겨지거나 연결이 끊긴 프로세스를 찾을 수 있다.<br>
pstree는 각 줄의 offset 주소 왼쪽에 .을 통하여 프로세스를 트리 형식으로 나타내준다. 상위, 하위 프로세스를 한 눈에 확인할 수 있으며 상위 프로세스가 없는 프로세스 위주로 분석하면 악성 프로세스를 쉽게 찾아낼 수 있다.<br>
psxview는 다양한 프로세스 리스트로 숨겨진 프로세스를 찾아준다. pslist는 Ture이지만 psscan은 False인 프로세스를 찾으면 해당 프로세스가 숨겨진 프로세스인 걸 확인할 수 있다.<br><br><br>




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
pslist를 pslist.log 파일로 출력하여 Notepad++ 프로그램을 통해서 확인하는 화면

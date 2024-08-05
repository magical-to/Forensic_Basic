**Windows Arfitacts**<br>
- Windows가 가지고 있는 특유의 기능들과 그 기능을 구현하는데 필요한 요소<br>
- Windows의 사용자가 수행하는 활동에 대한 정보를 보유하고 있는 개체<br><br>

- 생성 증거 : 프로세스, 시스템에서 자동으로 생성한 데이터<br>
- 보관 증거 : 사람이 기록하여 작성한 데이터<br><br>

- 레지스트리<br>
- &MFT, &Logfile, &UsnJrnl<br>
- LNK<br>
- JumpList<br>
- Recycle Bin<br>
- Prefetch & Cache(s)<br>
- Timeline<br>
- VSS<br>
- 웹브라우저 아티팩트<br><br>

**Windows Artifacts를 공부할 때 가장 중요한 점!!!**<br>
1. 사용자의 행위에 따라 어디에 어떤 정보가 저장될까?<br>
2. 컴퓨터는 대체 어떻게 동작하는 걸까?<br>
-> 사용자는 컴퓨터로 무슨 일을 했을까?<br><br><br>


**Registry**<br>
- 윈도우 아티팩트 중에서 가장 양이 많고 복잡함.<br>
- 윈도우 운영체제와 응용 프로그램 운영에 필요한 정보를 담고 있는 계층형 데이터베이스<br>
   - 운영체제 및 응용 프로그램의 설정 정보, 서비스의 중요 데이터 등 기록<br>
   - 부팅 과정부터 로그인, 서비스 실행, 응용프로그램 실행, 사용자 행위 등 모든 활동에 관여<br>
- 윈도우 시스템의 모든 정보가 담겨 있음<br>
   - 윈도우 시스템 분석의 필수 요소<br><br>

Reigstry의 극 일부<br>
- 시스템 표준 시간(TimeZone)<br>
- 시스템 정보(SystemInfo)<br>
- 사용자 계정 정보<br>
- 환경 변수 정보<br>
- 자동 실행 프로그램<br>
- 응용프로그램 실행 흔적(UserAssist, OpenSavePidIMRU, LastVisitedPidIMRU)<br>
- USB 연결 흔적<br>
- 접근한 폴더 정보(Shellbag)<br><br>

레지스트리 조회 및 편집 기능은 regedit(레지스트리 편집기)를 이용하여 쉽게 할 수 있다.<br>
레지스트리는 최초 5개의 키인 Root Key, 그 밑 서브 Key들, Value, Type, Data로 이루어져 있다.<br>
루트 키<br>
HKEY_CLASS_ROOT, HKCR, 파일 확장자 연결 정보. COM 객체 등록 정보<br>
HKEY_CURRENT_USER, HKCU, 파일 시스템에 로그인된 사용자의 프로파일 정보<br>
KEY_LOCAL_MACHINE, HKLM, 시스템의 하드웨어, 소프트웨어 설정 및 기타 환경 정보<br>
HKEY_USERS, HKU, 시스템의 모든 사용자와 그룹에 관한 프로파일 정보<br>
HKEY_CURRENT_CONFIG, HKCC, 시스템이 시작할 때 사용되는 하드웨어 프로파일 정보<br><br>

**Registry - Timezone**<br>
경로 : HLKM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation<br>
- Bias를 통해 현재 컴퓨터의 timezone을 알 수 있음.<br><br>

**Registry - SystemInfo**<br>
경로 : HLKM\SOFTWARE\Microsoft\Windows NT\CurrentVersion<br>
- 현재 윈도우 버전, 설치 시간, ProductId 등 시스템과 관련된 정보들<br><br>

**Registry - Autoruns**<Br>
경로 : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run<br>
경로 : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce<br>
경로 : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx<br>
경로 : HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run<br>
경로 : HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce<br>
경로 : HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx<br>
(RunOnce, RunOnceEx는 한 번 실행이 되고 레지스트리가 삭제가 된다.)<br><br>

**Registry - User Account**<br>
경로 : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\ProfileList\<br>
- S-1-5-18 : systemprofile<br>
- S-1-5-19 : LocalService<br>
- S-1-5-20 : NetWorkService<br>
- S-1-5-21 : 사용자가 만든 계정(SID)<br>
   - 1000 이상은 user 권한<br>
   - 500은 administrator<br>
   (악성코드 같은 거 중에서 계정을 하나 더 만들고 관리자 권한으로 상승시켜 백도어, 언제든지 만들어 놓은 계정으로 몰래몰래 접근하는 코드들이 존재하기 때문에 사용자 계정 정보를 추출하는 것도 의미가 있다.)<br>
- 사용자의 최종 로그인 시간<br>
   - LocalProfileLoadTimeHigh<br>
   - LocalProfileLoadTimeLow<br><br>

**각종 시간들은 Dcode를 통해서 확인하기 쉽다.**<br><br>

**Registry - Environment Variables**<br>
- 사용자 환경변수 확인<br>
   - 경로 : HKU\{SID}\Environment(SID)는 위 User Account에서 얻은 사용자가 만든 계정을 입력해주어야 한다.<br>
- 시스템 환경변수<br>
   - HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment<br><br>

**Registry - Executable<**<br>
- 응용프로그램(exe) 실행에 따른 흔적<br>
- UserAssist : 최근에 실행한 프로그램 목록, 마지막 실행 시간, 실행 횟수<br>
   - 경로 : HKCU\Software\Microsoft\Windows\CurrentVerison\Explorer\UserAsisst<br>
- OpenSavePidIMRU : 열기 혹은 저장 기능으로 사용된 파일<br>
   - 경로 : HKCU/Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32/OpenSavePidIMRU<br>
- LastVisitedPidIMRU : 열기 혹은 저장 기능을 사용한 응용 프로그램<br>
   - 경로 : HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidIMRU<br><br>
   
 **Registry - USB Connection**<br>
 - USB 등 외부 저장매체 연결 흔적을 추적 가능<br>
   - USB 제품명, 시리얼 번호, 최초 연결 시각, 마지막 연결 시각<br>
   - 경로 : 모든 USB : HKLM\SYSTEM\ControlSet001\Enum\USB<br>
            - 시스템에 연결되었던 모든 USB 장치의 정보가 기록됨, VIP와 PID를 검색하면, USB 종류를 알 수 있음<br>
           USB 저장장치 : HKLM\SYSTEM\ControlSet001\Enum\USB/USBSTOR<br>
            - 시스템에 연결되었던 모든 USB 저장장치의 정보가 기록됨<<br>
           마운트 디바이스 : HKLM\SYSTEM\MountedDevices<br><br>
            - 시스템에 마운트되었던 장치의 리스트를 나타냄<br><br><br>

**Registry - Shellbags**<br>
- 사용자가 접근한 폴더 정보를 기록함<br>
- BagMRU : 폴더의 구조를 계층적 구조로 나타냄(Bag : 윈도우 사이즈, 위치 등 사용자의 환경설정을 저장)<br>
   경로 : HKCU\Software\Classes\Local Settigns\Software\Microsoft\Windows\Shell\Bags<br>
   경로 : HKCU\Software\Classes\Local Settigns\Software\Microsoft\Windows\Shell\BagMRU<br>
   경로 : HKCU\Software\Microsoft\Windows\Shell\Bags<br>
   경로 : HKCU\Software\Microsoft\Windows\Shell\BagMRU<br><br>




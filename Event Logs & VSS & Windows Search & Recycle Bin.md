**Event Logs**<br><br>

• 로그란<br>
 • 컴퓨터를 이용한 기록 등이 컴퓨터 내에 남아있는 것<br>

• 이벤트 로그(Event Logs)<br>
 • Windows 운영체제에서 시스템의 로그를 남기는 방식<br>
 • 이벤트 뷰어(Event Viewer)를 통해 확인할 수 있음<br>
 • 시스템 로그, 응용프로그램 로그, 보안 로그 등이 존재<br><br>

• 이벤트 로그(Event Logs)<br>
 • 응용 프로그램 로그<br>
 • 보안 로그<br>
 • Setup 로그<br>
 • 시스템 로그<br>
 • 응용프로그램 및 서비스 로그<br>
![image](https://github.com/user-attachments/assets/6a3e65a3-e7ed-4f20-a1a7-35135c268463)<br><br>

• 응용프로그램(Application)<br>
 • 시스템 구성 요소를 제외한 응용프로그램에서 발생한 이벤트기록 (데이터베이스오류, AV 로그 등)<br>
 • 기록할 이벤트유형은 응용프로그램 개발자가 결정<br><br>

• 보안(Security)<br>
 • 파일만들기, 열기 등의 리소스 사용 이벤트 및 로그인성공/실패, 보안정책 변경과 같은 보안이벤트<br>
 • 기록할 이벤트유형은 관리자에 의해 변경가능 (유일하게 사용자가 변경가능)<br><br>

• 설치 (Setup)<br>
 • 응용프로그램 설치 및 설정과 관련한 이벤트 기록<br>
 • 응용 프로그램 및 서비스 로그<br
 • Internet Explorer, Microsoft Office 및 Windows Application 들에서 생성하는 다양한 로그<br>
 • Windows Defender(디펜더), Partition Diagnostic(USB 연결 흔적), WLAN Autoconfig(Wifi 연결) 등<br><br>

• 이벤트 로그 경로<br>
 • C:\Windows\System32\winevt\Logs<br>
 • 많은 파일들 중에서 크기가 같은 파일들은 로그 파일이 있는데 로그 데이터는 없는 것이다.<br>
 • 각각의 EVYX라는 파일이 이벤트 뷰어의 Windows 로그 하위에 각각 대응되는 것을 확인할 수 있다.(Application.evyx -> 응용프로그램, Security.evyx -> 보안)<br><br>

• 이벤트 ID<br>
 • 각각의 이벤트 로그는 이벤트 ID를 가짐<br>
 • 이벤트 ID 별로 나타내는 활동이 유사함<br>
  • ex) Logon: 4624, Logoff: 4634<br><br>

• 어떤 이벤트 ID를 찾을 것인가?(참고 자료들)<br>
 • Spotting the Adversary with Windows Event Log Monitoring, NSA<br>
 • Windows 10 and Windows Server 2016 security auditing and monitoring reference, Microsoft<br>
 • 윈도우 이벤트 로그(EVTX) 분석 및 포렌식 활용방안, 강세림<br>
![3](https://github.com/user-attachments/assets/8fd40c32-1acc-4ab7-9f90-29a260a2ac37)<br><br><br>


• 이벤트 ID 검색 사이트<br>
 • https://kb.eventtracker.com/<br>
 • https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/Default.aspx<br>
 • https://eventid.net/ (현재 지원 중단)<br>

• 이벤트 ID를 찾아보자!<br>
 • 이벤트 뷰어 “사용자 지정 보기 만들기”<br>
 ![4](https://github.com/user-attachments/assets/7524e343-f428-40e4-9814-cfe68adaeab0)<br>
기간은 지정해도 상관없다. 이벤트 로그(E): 는 어떤 것을 기반으로 할 지를 결정을 하는 것이기에 크게는 Windows 로그와 응용프로그램 및 서비스 로그를 체크해주면 된다.<br><br>


만약 외부에서 evtx 이벤트로그 파일들을 가져와서 사용하고 있는 PC에서 분석을 한다하면 메뉴바에 있는 동작 -> 저장된 로그 열기를 통해 가져오면 된다.<br><br>

이벤트 ID를 입력하는 칸에는<br>
![3](https://github.com/user-attachments/assets/8fd40c32-1acc-4ab7-9f90-29a260a2ac37)<br>
위 사진에서 ID 기반으로 복사를 해서 가져오면 된다.<br><br>

EX)<br>
• 소프트웨어 설치, 업데이트 및 삭제<br>
 • 6,7045,1022,1033, 903-908, 800,2,19<br>
![image](https://github.com/user-attachments/assets/62e95bf3-d103-4dc4-8997-0b9802f0ddb4)<br>
최종 세팅<br><br>

![6](https://github.com/user-attachments/assets/99ffcd6d-0d5a-4af1-bb76-1b7a9ffcf0e9)<br>
총 5,145개의 이벤트가 필터링이 되었으니(좌측 software은 직접 지정한 이름) 이벤트들을 살펴보자.<br>
원본이라 써져 있는 곳의 WER은 에러 관련 이벤트를 나타내고 있다. 이 외에도 Windows 업데이트 이벤트, 일정 관리(Task Scheduler),<br>
Time Zone Sync이라는 인터넷으로부터 싱크를 맞추는 애플리케이션과 KernelEventTracing이 뭔가 오류를 발생한 이벤트 등...<br>
만약 악성코드가 있다면 악성코드가 실행되면서 오류가 생겼다거나 악용 프로그램을 설치했다거나와 같은 정보들도 확인할 수도 있다.<br><br><br>

데이터 자체가 방대하기 때문에 예를 들어 이전에 봤던 Prefetch에서 악성코드가 있었다와 같은 타임 데이터를 가져와서 해당 시간대를 살펴보는 것이 주 목적 중 하나이다.<br><br>

• 사용자 로그인<br>
 • 4740,4728,2732,4756,4735,4624, 4625,4648<br><br>

전과 같이 설정을 한 뒤, 이벤트 ID만 변경하면 된다.<br>
로그온을 했던 시간들을 볼 수 있다. Windows + L 버튼을 이용해 잠금을 한 뒤 다시 로그온을 했을 때 새 이벤트를 사용할 수 있음이라는 데이터가 나오게 된다.<br><br>

다른 데이터를 보고 오면 성공적으로 로그인되었다는 데이터도 남는 것을 볼 수 있다.<br><br>

**VSS**<br><br>

• VSS(Volume Shadow Copy Service)<br>
 • 특정한 시각의 파일, 폴더의 복사본이나 볼륨의 스냅샷을 저장해두고 복원할 수 있는 기능<br><br>

• 시스템 복원 기능<br>
 • 컴퓨터 전체를 복원 지점으로 되돌리기<br>
 • 특정 파일/폴더를 이전 버전으로 되돌리기<br><br>

• VSS 설정<br>
 • 복원 지점 만들기 검색<br>
 • 구성 -> 시스템 보호 사용 설정<br>
   구성 -> 디스크 공간 설정<br>
 • 만들기 -> 시스템 복원<br><br>

VSS - Practice<br><br>

• VSS 확인
 • vssadmin list shadows<br>
 • mklink /d(링크폴더)(섀도 복사본 볼륨)<br>
 • 파일 탐색기로 접근하여 확인<br><br>

• ShadowExplorer<br>
 • https://www.shadowexplorer.com/downloads.html<br><br><br>


시스템 속성 -> 시스템 보호 -> 시스템 복원을 들어가면 복원 지점이 만들어져 있는 것이 보이고 다음 버튼을 누르면 영향을 받는 프로그램 검색<br>
이라고 나와있늗네 이 복원 지점으로부터 현재 내 시스템이 어떤 것이 변경되었는지에 대한 정보이다.<br><br>

해당 정보에 보여지는 프로그램은 복원을 하면 해당 프로그램이 제거된다고 말하고 있는 것인데 이는 옛날 복원 시점에 비해 프로그램이 새로 설치되었다라는 의미를 가지고 있는 것이다.<br><br>

CMD를 관리자 권한으로 작동하고 vssadmin list shadows 명령어를 치게 되면 두 개의 복사본이 생긴 걸 확인할 수 있다.<br><br>

**Windows Search**<br><br>

• Windows 검색 기능<br>
 • 작업표시줄 아이콘 클릭 or Windows + S 단축키<br><br>

• **Windows Indexing**<br>
 • 검색 기능을 구현하기 위해 미리 Indexing 작업을 수행함<br>
 • 파일 이름과 전체 파일 경로를 포함하여 파일의 모든 속성이 인덱싱됨<br>
 • 텍스트가 포함된 파일의 경우, 콘텐츠가 인덱싱됨<br><br>

• Windows.edb<br>
 • Windows Search에 사용하기 위한 Indexing 정보 저장<br>
 • 경로: %ProgramData%\Microsoft\Search\Data\Applications\Windows<br><br>

• Windows.edb 수집<br>
 • 온라인 상태에서 수집할 때는 Windows Search (Wsearch) 서비스를 종료시켜야 함<br>
 • 서비스 동작 중 복사하거나 포렌식 도구로 수집 시 정상적인 구조가 아닌 “Dirty” 상태로 수집됨<br>
 • Dirty: 응용프로그램이 데이터베이스를 사용하는 중의 상태<br>
 • Clean: 데이터베이스 API를 사용하여 트랜잭션을 모두 처리한 상태<br><br>

• Windows.edb 수집 과정<br>
 • Windows Search 서비스 ‘사용 안 함’<br>
 • Windows Search 서비스 ‘중지’<br>
 • 이후에 Windows.edb 복사<br><br>

• Clean shutdown 확인<br>
 • esentutl /m <파일이름> | findstr State<br>
 • State: Clean Shutdown 확인<br><br>

• ESEDatabaseView<br>
 • ESE Database를 보여주는 도구<br><br>

• WinSearchDBAnalyzer<br>
 • https://moaistory.blogspot.com/2018/10/winsearchdbanalyzer.html<br><br>

![image](https://github.com/user-attachments/assets/081d6035-24bb-40a0-8661-b71b44c49539)<br>
노말한 레코드를 파싱할 수도 있고, 삭제된 레코드를 리커버리 할 수도 있다.<br><br>

• **휴지통(Recycle Bin)<br>**
 • 파일을 삭제하고, 복원하거나 영구 삭제할 수 있음<br><br>

• 휴지통 폴더 확인<br>
 • 파일탐색기 보기 설정 변경(숨김 폴더 표시)<br><br>

• 휴지통 폴더는 볼륨 단위로 생성<br>
 • 로컬 디스크로 인식되는 경우에 생성<br>
 • USB 등 이동식 디스크, 네트워크 드라이브 등은 생성되지 않음<br><br>

•”휴지통” 아이콘<br>
 • 모든 볼륨의 휴지통 폴더를 통합하여 보여줌<br>
 • 그러나 하나의 폴더로 존재하는 것은 아님<br><br>

• 휴지통 아티팩트(파일 삭제 시)<br>
 • 휴지통 폴더 경로: <Volume>\$Recycle.Bin\<SID>\<br>
 • 삭제된 파일: $R<임의문자열 6자리>.<원본 파일 확장자><br>
 • 삭제 관련 메타데이터: $I<임의문자열 6자리>.<원본 파일 확장자><br>
  • 원본 파일의 경로, 휴지통으로 삭제된 시각 등<br><br>
  
![8](https://github.com/user-attachments/assets/2f9bf13f-0d08-4de2-b4b2-b5e38c6bb94d)<br><br>

• 휴지통 아티팩트(파일 복원시)<br>
 • 삭제된 파일($R)은 사라짐<br>
 • 삭제 관련 메타데이터($I)는 남아 있음<br>
![9](https://github.com/user-attachments/assets/a004634e-258a-4d4e-af19-003257dd4149)<br><br>

• 휴지통 아티팩트(휴지통 비우기)<br>
 • 삭제된 파일($R) 및 삭제 관련 메타데이터($I) 모두 삭제<br><br>

• 휴지통 아티팩트 실습<br>
 • 테스트용 폴더 및 파일 생성<br>
 • 1) 삭제 2) 복구 3) 휴지통 비우기 실습<br>

• 메타데이터 분석
 • Windows File Analyzer, https://www.mitec.cz/wfa.html
 • 파일 경로, 삭제된 시점, 크기 확인

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

• 이벤트 ID를 찾아보자!
 • 이벤트 뷰어 “사용자 지정 보기 만들기”

• 소프트웨어 설치, 업데이트 및 삭제
• 6,7045,1022,1033, 903-908,
800,2,19

• 사용자 로그인
• 4740,4728,2732,4756,4735,4624,
4625,4648

VSS
02

VSS
Digital Forensics

• VSS(Volume Shadow Copy Service)
• 특정한 시각의 파일, 폴더의 복사본이나 볼륨의 스냅샷을 저장해두고 복원할 수 있는 기능

• 시스템 복원 기능
• 컴퓨터 전체를 복원 지점으로 되돌리기
• 특정 파일/폴더를 이전 버전으로 되돌리기

VSS
Digital Forensics

• VSS 설정
• 복원 지점 만들기 검색
• 구성 à 시스템 보호 사용 설정
구성 à 디스크 공간 설정
• 만들기 à 시스템 복원

VSS - Practice
Digital Forensics

• VSS 확인
• vssadmin list shadows
• mklink /d <링크폴더> <섀도 복사본 볼륨>
• 파일 탐색기로 접근하여 확인

• ShadowExplorer
• https://www.shadowexplorer.com/downloads.html

Windows Search
03

Windows Search
Digital Forensics

• Windows 검색 기능
• 작업표시줄 아이콘 클릭 or Windows + S 단축키

Windows Search
Digital Forensics

• Windows Indexing
• 검색 기능을 구현하기 위해 미리 Indexing 작업을 수행함
• 파일 이름과 전체 파일 경로를 포함하여 파일의 모든 속성이 인덱싱됨
• 텍스트가 포함된 파일의 경우, 콘텐츠가 인덱싱됨

Windows Search
Digital Forensics

• Windows.edb
• Windows Search에 사용하기 위한 Indexing 정보 저장
• 경로: %ProgramData%\Microsoft\Search\Data\Applications\Windows

• Windows.edb 수집
• 온라인 상태에서 수집할 때는 Windows Search (Wsearch) 서비스를 종료시켜야 함
• 서비스 동작 중 복사하거나 포렌식 도구로 수집 시 정상적인 구조가 아닌 “Dirty” 상태로 수집됨
• Dirty: 응용프로그램이 데이터베이스를 사용하는 중의 상태
• Clean: 데이터베이스 API를 사용하여 트랜잭션을 모두 처리한 상태

Windows Search - Practice
Digital Forensics

• Windows.edb 수집 과정
• Windows Search 서비스 ‘사용 안 함’
• Windows Search 서비스 ‘중지’
• 이후에 Windows.edb 복사

• Clean shutdown 확인
• esentutl /m <파일이름> | findstr State
• State: Clean Shutdown 확인

Windows Search - Practice
Digital Forensics

• ESEDatabaseView
• ESE Database를 보여주는 도구

• WinSearchDBAnalyzer
• https://moaistory.blogspot.com/2018/10/winsearchdbanalyzer.html

Recycle Bin
04

Recycle Bin
Digital Forensics

• 휴지통(Recycle Bin)
• 파일을 삭제하고, 복원하거나 영구 삭제할 수 있음

• 휴지통 폴더 확인
• 파일탐색기 보기 설정 변경

Recycle Bin
Digital Forensics

• 휴지통 폴더는 볼륨 단위로 생성
• 로컬 디스크로 인식되는 경우에 생성
• USB 등 이동식 디스크, 네트워크 드라이브 등은 생성되지 않음

•
”휴지통” 아이콘
• 모든 볼륨의 휴지통 폴더를 통합하여 보여줌
• 그러나 하나의 폴더로 존재하는 것은 아님

Recycle Bin
Digital Forensics

• 휴지통 아티팩트(파일 삭제 시)
• 휴지통 폴더 경로: <Volume>\$Recycle.Bin\<SID>\
• 삭제된 파일: $R<임의문자열 6자리>.<원본 파일 확장자>
• 삭제 관련 메타데이터: $I<임의문자열 6자리>.<원본 파일 확장자>
• 원본 파일의 경로, 휴지통으로 삭제된 시각 등

Recycle Bin
Digital Forensics

• 휴지통 아티팩트(파일 복원시)
• 삭제된 파일($R)은 사라짐
• 삭제 관련 메타데이터($I)는 남아 있음

Recycle Bin
Digital Forensics

• 휴지통 아티팩트(휴지통 비우기)
• 삭제된 파일($R) 및 삭제 관련 메타데이터($I) 모두 삭제

Recycle Bin - Practice
Digital Forensics

• 휴지통 아티팩트 실습
• 테스트용 폴더 및 파일 생성
• 1) 삭제 2) 복구 3) 휴지통 비우기 실습

• 메타데이터 분석
• Windows File Analyzer, https://www.mitec.cz/wfa.html
• 파일 경로, 삭제된 시점, 크기 확인

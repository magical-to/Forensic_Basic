**ThumbnailCache**<br>

• 썸네일(Thumbnail)<br>
  • ‘미리보기 파일’을 의미함<br><br>
  
• Windows에서는 썸네일 사진들을 미리 생성하여 보관하고 있음<br>
• %UserProfile%\AppData\Local\Microsoft\Windows\Explorer<br><br>

• thumbcache_{크기}.db<br>
  • thumbcache는 크기에 따라 다른 db 형태로 존재하게 되는데, 이렇게 별도로 존재하는 이유는 큰 아이콘부터 작은 아이콘까지 다양한 형태의 미리 보기를 지원하기 위함이다.<br><br>

**IconCache**<br>
• Windows 아이콘(Icon)을 보여주기 위해서 가지고 있는 캐시<br>
  • 공통의 아이콘을 사용(일반적인 폴더, 파일)<br>
  • 별도의 아이콘을 사용(응용프로그램)<br><br>

• Windows에서는 아이콘 사진들을 별도의 공간에 모아서 보관함<br>
  • %UserProfile%\AppData\Local\Microsoft\Windows\Explorer<br><br>
  
• iconcache_{}.db(thumbcache와 같이 크기에 따라서 DB를 별도로 만들어서 보관을 하게 된다.<br><br>

**ThumbnailCache & IconCache**<br><br>

포렌식적 의미<br>
• ThumbnailCache<br>
  • 분석 대상 PC에 해당 파일이 존재하였음을 나타냄<br>
  • 해당 파일이 삭제되더라도 ThumbnailCache는 사라지지 않음<br><br>

• IconCache<br>
  • 분석 대상 PC에 존재했던 응용프로그램의 종류를 확인 가능<br>
  • 외부저장매체 사용 흔적 파악<br
  • 안티포렌식 도구 사용 흔적, 악성코드 실행 흔적 파악<br>
  • 해당 응용프로그램이 삭제되더라도 IconCache는 사라지지 않음<br><br>

• Thumbcache Viewer 다운로드<br>
  • https://thumbcacheviewer.github.io/<br><br>

![1](https://github.com/user-attachments/assets/644ed0cf-dc85-499e-9dc5-123a6d4ba6e7)<br>
• %UserProfile%\AppData\Local\Microsoft\Windows\Explorer 경로로 가서 아무 파일이나 드래그 앤 드롭을 하면 확인할 수 있다.<br><br><br><br>



Windows Timeline


• Windows에서 지원하는 Timeline 기능
• 사용자가 실행하고 있는 응용프로그램
• 사용자가 과거에 실행했던 응용프로그램
• 최대 30일의 사용자 행위를 보관

• Windows + Tab 버튼

Windows Timeline
Digital Forensics

• 설정 활성화
•
‘이 장치에 내 활동 기록 저장’ 설정

• Timeline 데이터 저장 경로
• 유저 계정에 따라 경로가 달라짐
• 로컬 계정: L.{로컬 계정명}
• 마이크로소프트 계정: {마이크로소프트 식별자(CID)}
• Office 365 & AAD 계정: AAD.{보안 식별자(SID)}
• %UserProfile%\AppData\Local\ConnectedDevicesPlatform\{계정명}\ActivitiesCache.db

Windows Timeline
Digital Forensics

• ActivitiesCache.db 구조
• Activity: 응용프로그램 실행 기록, 실행 시간 등 보통의 Timeline 데이터
• ActivityOperation: 생성 혹은 삭제 이벤트에 대한 Timeline 데이터
• Activity_PackageId: 앱별 패키지 이름

Windows Timeline
Digital Forensics

• Windows 10에서 2018년부터 추가된 기능
• Windows 11부터는 지원 중단
• 그러나, 동일한 경로에 데이터가 생성됨을 확인
•
‘활동 기록’ 메뉴 역시 그대로 존재

• 포렌식적 의미
• 시간에 따른 사용자의 행위 추적
• 응용프로그램의 구체적인 사용 시각을 알 수 있음


• 저장 경로 확인
• 계정명 확인
• %UserProfile%\AppData\Local\ConnectedDevicesPlatform\{계정명}\ActivitiesCache.db

• DB Browser for SQLite 활용

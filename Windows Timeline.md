**Windows Timeline**<br><br>


• Windows에서 지원하는 Timeline 기능<br>
 • 사용자가 실행하고 있는 응용프로그램<br>
 • 사용자가 과거에 실행했던 응용프로그램<br>
 • 최대 30일의 사용자 행위를 보관<br>

• 실행방법 : Windows + Tab버튼 <br><br><br>


• 설정 활성화<br>
 • ‘이 장치에 내 활동 기록 저장’ 설정<br><br>

• Timeline 데이터 저장 경로<br>
 • 유저 계정에 따라 경로가 달라짐<br>
  • 로컬 계정: L.{로컬 계정명}<br>
  • 마이크로소프트 계정: {마이크로소프트 식별자(CID)}<br>
  • Office 365 & AAD 계정: AAD.{보안 식별자(SID)}<br>
 • %UserProfile%\AppData\Local\ConnectedDevicesPlatform\{계정명}\ActivitiesCache.db<br><br>

• ActivitiesCache.db 구조<br>
 • Activity: 응용프로그램 실행 기록, 실행 시간 등 보통의 Timeline 데이터<br>
 • ActivityOperation: 생성 혹은 삭제 이벤트에 대한 Timeline 데이터<br>
 • Activity_PackageId: 앱별 패키지 이름<br><br><br>


• Windows 10에서 2018년부터 추가된 기능<br>
 • Windows 11부터는 지원 중단<br>
 • 그러나, 동일한 경로에 데이터가 생성됨을 확인<br>
 • ‘활동 기록’ 메뉴 역시 그대로 존재<br><br>

• 포렌식적 의미<br>
 • 시간에 따른 사용자의 행위 추적<br>
 • 응용프로그램의 구체적인 사용 시각을 알 수 있음<br><br><br>

• 저장 경로 확인<br>
 • 계정명 확인<br>
 • %UserProfile%\AppData\Local\ConnectedDevicesPlatform\{계정명}\ActivitiesCache.db<br>
 • %UserProfile%\AppData\Local\ConnectedDevicesPlatform\ 위치에서 계정을 여러개 사용중이라면 여러 개의 폴더가 존재할 수도 있다.<br><br>
  

![1](https://github.com/user-attachments/assets/7f30fba8-505b-4221-849d-fe29a6c145b9)<br><br>

• Browse Data - Activity 테이블에서 Payload에는 복사 붙여넣기 할 때 클립보드에 저장되는 데이터가 남는 것을 볼 수 있다.<br>
• 맨 왼쪽의 Id를 이용해서 Edit Database Cell을 이용하여 해당 데이터를 찾아낼 수 있다.<br><br>

• ActivityOperation 테이블에서는 생성하거나 삭제한 데이터가 남는다. 한글이나 캡쳐 도구, 스티커 메모, 카카오톡과 같은 데이터들이 생성 시각과 응용 프로그램의 시작 시간과 끝나는 시간들도 남는다.<br><br><br>





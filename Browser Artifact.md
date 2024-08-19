**Web Browser**<br>
• 인터넷을 이용하기 위해 실행하는 응용 프로그램<br>
![image](https://github.com/user-attachments/assets/74917706-5915-4c50-b46b-f6594e52dfcb)<br><br>

• 브라우저를 통해 하는 일들<br>
  • 웹 검색<br>
  • 로그인<br>
  • 파일 다운로드<br>
  • 영상 시청<br><br>

**Web Browser Artifacts**<br>
• History : 방문한 URL, 방문 횟수, 방문 시각 등<br>
• Cache : 캐시로 저장되는 이미지, 텍스트, 스크립트, 아이콘, 시간, 크기 등<br>
• Cookie : 사용자 데이터, 자동 로그인 등<br>
• Download list : 저장 경로, URL, 크기, 시간, 성공 여부 등<br><br>

• 브라우저별 경로<br>
  • Chrome: %UserProfile%\AppData\Local\Google\Chrome\User Data\Default\<br>
  • Edge: %UserProfile%\AppData\Local\Microsoft\Windows\WebCache\<br>
  • Whale: %UserProfile%\AppData\Local\Naver\Naver Whale\User Data\Default\<br><br>

• Chrome 아티팩트 분석<br>
  • History<br>
  • Cache<br>
  • Top Sites<br>
  • Shortcuts<br>
  • Bookmarks<br>
  • Last Tabs<br><br>

• DB Browser for SQLite<br>
https://sqlitebrowser.org/<br><br>

![2](https://github.com/user-attachments/assets/a345d74b-a78a-44e5-91cb-6ed198b7046e)<br>
해당 파일들을 드래그 앤 드롭으로 DB Browser for SQLite 프로그램에 던져준다.<br>
그냥 드래그 앤 드롭을 하게 되면 lock 되어있다고 표시되는데, 해제하는 방법은 브라우저를 끄고 실행을 하면 된다.<br><br>

![3](https://github.com/user-attachments/assets/e24089e5-2e0b-42f2-a787-3a1fd5a6a997)<br>
Browse Data 탭으로 와서 테이블을 하나하나 옮겨가며 어떠한 데이터가 남는 지 확인을 할 것이다.<br><br>

History 테이블에서는 Download, URL, visits를 볼 것이다.<br><br>

![4](https://github.com/user-attachments/assets/c73222ec-4326-424a-8729-76353148cc2a)<br>
옆 줄에 보면 target_path 뿐만 아니라 start_time, received_bytes, total_bytes, state 등의 내용을 확인할 수 있다.<br><br>
state 값은 성공 실패 여부를 나타낸다. 끝까지 다운로드를 성공했는지, 못했는지.<br><br>
Referrer는 다운로드 URL에 접근하기 이전 사이트를 나타낸다.<br><br>
tab_url은 tap에 띄워져 있던 url을 나타낸다.<br><br><br>

다운로드를 직접 받은 url은 download_url_chain이라는 곳에서 확인할 수 있는데, ID 필드를 기반으로 연결하고 있다.<br><br>
즉, download 탭에서의 2번이 download_url_chains에서 id 목록의 2번에 해당하는 파일이라는 것이다.<br><br>

start_time이라는 부분이 시간 데이터인데,<br>
![image](https://github.com/user-attachments/assets/03516db2-fe08-4b06-baf3-072e33b40f3b)<br>
요 DCode라는 프로그램을 이용해서 Format을 정수로 바꿔주고 데이터를 넣은 뒤 Decode를 하면 시간이 변환이 된다.<br><br><br>

url 테이블은 당연하게도, 사용자가 어디 url에 접속을 했는지 기록들이 나오게 된다.<br><br>
title은 url에 들어갔을 때, 도메인의 이름이 테이블이다. 해당 페이지의 타이틀은 주소 위의 Forensic_basic/Browser Artifact_md이겠다.<br><br>
visit_count는 방문한 횟수, last_visit_time은 마지막 방문 시각이다.<br><br>
사용자의 방문 기록을 추적하는 법은 url id 값을 가지고 visits 테이블로 넘어가게 된다면 확인을 할 수 있다.<br><br>
visit_duration은 얼마나 오랫동안 켜놨는지 추축할 수 있다.<br><br><br>

• Chrome 아티팩트 분석<br>
<p>$\bf{\rm{\color{#DD6565}  • History}}$</p><br>
  • Cache<br>
  • Top Sites<br>
  • Shortcuts<br>
  • Bookmarks<br>
  • Last Tabs<br><br>

History가 가장 데이터가 많이 남아있는 아티팩트이기도 하다.















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

History가 가장 데이터가 많이 남아있는 아티팩트이기도 하다.<br><br><br><br>

(아... 어제 분명 작성하고 저장을 눌렀는데 저장이 안 되어있다... 벌써 2번째인데 덕분에 contribution 빵꾸 또 생겼다 ㅠㅠ..)<br><br><br>

무튼 기억을 되살려서 복습을 하는 느낌으로 다시 작성을 해보자면,<br><br>

%UserProfile%\AppData\Local\Local\Microsoft\Windows\WebCache<br>
위 경로에 가게된다면 Web에서 남겨진 기록들을 모두 담고 있는 WebCacheV01.dat 파일이 있다.<br><br>

이 파일을 통해서 Edge 아티팩트 분석을 할 것이다.<br><br>

사용한 도구는<br>
• ESEDatabaseView(https://www.nirsoft.net/utils/ese_database_view.html)이다.<br><br>

EseDatabaseView 프로그램을 통해서 WebCacheV01.dat을 드래그 앤 드롭 형식으로 두려고 하면 오류가 뜬다.<br>
그 이유는 WebCacheV01.dat 파일은 Windows 자체에서 잡고 있는 파일이기 때문이다. 쉽게 말해서 우리가 편집 중인 파일을 이동시키려고 하면 해당 파일이 열려 있어서 불가능한 것이라고 생각하면 된다.<br><br>
![6](https://github.com/user-attachments/assets/8547dc01-1ec1-4ffb-92c5-fe309ac5cb22)<br>
그렇기에, 위 사진처럼 FTK Imager로 해당 파일의 경로에 가서 WebCacheV01.dat 파일을 추출해낼 것이다.<br><br>

사실, 올바른 추출 방식은 서비스를 끈 다음에 복사를 해서 해당 파일을 다시 클린을 해서 뭐시기 하는데,,, 편의상 진행하도록 한다.<br><br>

![7](https://github.com/user-attachments/assets/661eb138-4363-4858-967a-b6be949be41f)
File 밑밑 줄을 클릭해보면 테이블들이 상당히 많이 존재하는 것을 볼 수 있다.<br>
Containers 테이블에 들어가게 되면 Name 필드를 보면 어떤 컨테이너에서 어떤 정보를 담고 있는지에 대해서 간단하게 정보를 얻을 수 있다.<br>
예를 들어, History라는 사용자의 접속 기록같은 것을 보고 싶으면 맨 왼쪽의 ContentId를 보고 ContentId가 10이라면 Conatiner 10테이블로 이동하면 되는 것이다.<br><br>

또 다른 도구를 소개하고자 하는데 그것은 바로<br>
• BrowsingHistoryView이다.<br>
  • https://www.nirsoft.net/utils/browsing_history_view.html<br><br>

![8](https://github.com/user-attachments/assets/a4afb3a5-b389-400a-8daa-6b81711496e0)<br>
위 사진은 BrowingHistoyView 프로그램을 처음 실행하였을 때 나오는 Advanced Options 창이다.<br><br>
Filter by visit data/time에서 Anytime을 누르게 되면 컴퓨터에 존재하는 모든 브라우징 히스토리를 불러오는 것이다.<br><br>
다른 옵션을 통해서 기간, range를 조절할 수 있다. 밑에 Web Browser는 지원하는 웹 브라우저들을 보여주는 것이다.<br><br><br>

Ok 버튼만 누르게 되면 모든 기록들이 싹 다 수집되는 모습을 볼 수 있다. URL 뿐만 아니라 Visit Count, Title 그리고 시간값들이 언젠지도 한국 시간으로 자동 변경되어서 확인할 수 있다.<br><br>

Visit Duration, 사이트의 접속 기간과 어떤 웹브라우저를 사용했는지, History 파일 경로도 나오고 있다.<br><br>

이 프로그램의 큰 단점은 History밖에 안 보여준다는 단점이 있다...<br><Br>

History, Cache, Cookie, Download List 중에서 History를 제외한 3가지는 볼 수 없는데 History가 제일 중요한 정보이기도 하기 때문에 일반적으로 볼 때 BrowsingHistoryView가 편하긴 하다.<br><Br>

• Chrome<br>
  • ChromeCacheView, Hindsight<br>
• Edge<br>
  • IE10Analyzer, ESEDatabaseView<br>
• Whale<br>
  • Carpe Forensics<br><br><br>
위는 브라우저별 도구 목록이다.<br>






<br>



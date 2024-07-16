# Forensic_Basic
The Real Basic Of Forensic </br>


컴퓨터 범죄와 관련하여 디지털 장치에서 발견되는 자료를 복구하고 조사하는 법과학의 한 분야 </br>

해킹 등 컴퓨터 관련 범죄 뿐만 아니라 일반 범죄에서도 디지털 포렌식으로 획득할 수 있는 증거가 주요 단서가 되는 경우가 많아지고 있다. <br/>

범죄 수사 이외의 분야에서도 활용도가 증가하였음
- 형사 사건이 아닌 민사 사건에서의 포렌식
- 일반 기업에서의 수요가 증가

<div align=center><br><br><br>
<p>$\huge{\rm{\color{#5ad7b7}디지털\ 포렌식의\ 큰\ 유형}}$</p>

   침해 사고 대응 vs 증거 추출
- 실시간                       사후 조사      
- 사태 파악 및 수습             범죄 증거 수집
- 엄격한 입증 필요 X            엄격한 입증 필요 O
</div>

<br><br><br>
<div align=center>
<p>$\huge{\rm{\color{#5ad7b7}디지털\ 포렌식의\ 대상}}$</p>
</div>
1. 디스크 포렌식 -> 컴퓨터 디스크 (윈도우, 리눅스, MacOS / 개인, 서버, 클라우드) <br>
2. 메모리 포렌식 -> 컴퓨터 메모리 (RAM)  <br>
3. 네트워크 포렌식 -> 네트워크 패킷, 네트워크 장비 로그, 네트워크 관련 설정들 <br>
4. 모바일 포렌식 -> 모바일 디바이스 (저장소, 메모리) / IoT 디바이스) <br>
5. 기타 -> 데이터베이스 포렌식, 암호 포렌식, 회계 포렌식, 소스코드 포렌식 ..etc <br>


<br><br><br><br><br><br>
Using Tools : Hxd, AutoPsy, 7zip, Everything, Notepad++, FTK-imager, Sysinternal Suite(strings ,procexcp, procmon)<br><br>

디스크 이미징이란, 디스크를 파일의 형태로 가져오는 것을 말한다. 디스크를 분석하기 위해서는 파일의 형태로 존재해야 하므로 디스크 이미징을 수행한다. 이 때, 주의해야 할 점은 C 드라이브의 이미지를 같은 드라이브에 저장할 수 없다는 것이다. 따라서 USB의 이미지를 C 드라이브에 저장하거나, D 드라이브의 이미지를 C 드라이브에 저장하는 방식을 사용한다.<br><br>

<div align=center>
<p>$\huge{\rm{\color{#5ad7b7}디스크\ 마운트\ }}$</p>

   ![1](https://github.com/user-attachments/assets/353abbc6-1342-4fc9-8674-39be1f330207)
디스크 마운트란, 이미징된 파일을 내 컴퓨터로 등록시키는 것이다. 디스크 이미지를 다시 드라이브처럼 내 컴퓨터에 등록하여 D, E, F... 드라이브 등이 새로 생성된다.
</div>
<br><br><br><br>

<div align=center>
<p>$\huge{\rm{\color{#5ad7b7}Meomry\ Dump\ }}$</p>
   
   ![2](https://github.com/user-attachments/assets/530a6492-0f44-4a70-9a3d-f24b72e676ff)
   ![3](https://github.com/user-attachments/assets/40923045-5cae-47a9-850c-882600bd602e)

   
메모리 덤프란, 메모리의 특정 시점 상태를 파일로 만들어 저장하는 것이다. 주로 켜져있는 컴퓨터를 수사할 때 사용한다.
   
</div>









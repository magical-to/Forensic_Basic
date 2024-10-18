**MFT(Master File Table)**<br>
• NTFS 파일시스템에서 파일, 디렉터리를 관리하기 위한 구조<br>
• 하나의 파일당 하나의 MFT 엔트리를 가짐<br>
• $MFT란 MFT 엔트리들의 집합<br><br>

**MFT 엔트리**<br>
• 파일의 이름, 생성·수정·변경시간, 크기, 속성 등을 가지고 있음<br>
• 파일의 디스크 내부 위치, 파일의 시스템 경로를 알 수 있음<br><br>

• FTK Imager를 이용<br>
  • [root]\$MFT 추출<br><br>

• MFTExplorer 다운로드(https://ericzimmerman.github.io/#!index.md)<br><br>

FTK Imager를 이용해 Logical Drive로 C Drive를 연 다음에, MFT를 스캐닝해서 폴더 구조를 파악하는 작업을 거친다.<br><br>

![7](https://github.com/user-attachments/assets/38ab2521-1565-4818-941e-7267a2c20eb4)<br>
root 디렉토리에서 $MFT를 찾을 수 있는데 이것을 추출할 것이다.<br>
그 후, MFT Explorer를 이용해 추출한 $MFT 파일을 오픈한다.<br>









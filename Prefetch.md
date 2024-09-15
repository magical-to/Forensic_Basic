**Prefetch**<br>
• 응용프로그램의 빠른 실행을 위해서 존재하는 파일<br><br>

• 응용프로그램을 실행할 때에 생성<br>
  • 실행 파일 이름, 경로<br>
  • 실행 파일의 실행 횟수<br>
  • 실행 파일의 마지막 실행 시간<br>
  • 실행 파일의 최초 실행 시간<br><br>

• 프리패치의 경로<br>
  • %SystemRoot%\Prefetch<br><br>

• WinPrefetchView 이용하여 분석<br>
  • https://www.nirsoft.net/utils/win_prefetch_view.html<br><br><br><br>

  

**MUICache**<br><br>
• Windows에서 다중 언어를 지원하기 위해 존재하는 캐시<br>
  • MUI(Multilingual User Interface)<br>
  • 실행 파일 별로, 유저 언어(한국어) 이름을 별도로 저장하고 있음<br><br>

• 응용프로그램을 실행하면 캐시에 기록이 남음<br>
  • 실행 파일 경로, 이름<br>
  • 실행 파일이 삭제되거나, 경로가 변경된 경우에도 기록이 지워지지 않음<br><br>

• MUICache 경로<br>
  • HKCU\Software\Classes\Local Settings\MuiCache<br>
  • HKCU\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\MuiCache<br><br>

• MUICache View 이용하여 분석<br>
  • https://www.nirsoft.net/utils/muicache_view.html<br><br><br><br>



**AmCache & ShimCache**<br>
• 응용프로그램과 운영체제의 호환성을 위해 존재하는 캐시<br>
  • 운영체제가 업데이트되면 DLL이 생성 혹은 삭제 à 호환성 문제 발생<br>
  • Windows에서는 프로그램 호환성 관리자를 이용하여 이 문제를 해결<br><br>

• Amcache<br>
  • 모든 실행 파일의 이름, 경로, 크기, 해시값 확인<br><br>
  
• ShimCache(AppCompatCache)<br>
  • 실행 파일의 경로, 최초 실행 시간 확인<br><br>

• AmCache & ShimCache 경로<br>
  • %SystemDrive%\Windows\AppCompat\Programs\Amcache.hve<br>
  • HKLM\SYSTEM\ControlSet001\Control\Session Manager\AppCompatCache<br>
  • HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\AppCompatCache<br><br>

• AmcacheParser, AppCompatCacheParser 이용하여 분석<br>
  • https://ericzimmerman.github.io/#!index.md<br><br><br>



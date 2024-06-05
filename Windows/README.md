# Windows

## 1. 윈도우 비밀번호 분실한 경우

    (1) left shift 누르고 다시시작 
    (2) [계속] - [고급옵션] - [명령 프롬프트]
    (3) copy c:\Windows\System32\Utilman.exe c:\Windows\System32\Utilman.bak
        >> 1개 파일이 복사되었습니다.
        copy c:\Windows\System32\cmd.exe c:\Windows\System32\Utilman.bak
        >> y 
        >> exit
        (드라이버 간 이동 C: or D: 입력하면 해당 드라이버로 이동됨)
    (4) [계속]
    (5) [로그인 화면에서 사람모양 아이콘 클릭]
    (6) >> net user {윈도우계정} {새로운비밀번호}
        >> exit

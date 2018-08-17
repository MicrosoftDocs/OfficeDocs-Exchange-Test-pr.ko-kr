---
title: '운영 체제가 디버그 mode_OSCheckedBuild입니다.: Exchange 2013 Help'
TOCTitle: 운영 체제가 디버그 mode_OSCheckedBuild입니다.
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50483691
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 운영 체제가 디버그 mode\_OSCheckedBuild입니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-15_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft® Exchange Server 분석기 도구는 **디버깅** 속성에 대 한 값을 설정할 수 있는지 여부를 확인 하려면 **위해 Win32\_OperatingSystem** Microsoft Windows® WMI (Management Instrumentation) 클래스를 쿼리 합니다. Exchange Server 컴퓨터에서이 키의 값은 **True**로 설정 하는 경우 오류가 표시 됩니다.

Boot.ini 파일에서 디버그/매개 변수를 추가 하 여 Windows 디버그 모드를 전환 됩니다. 디버그/가 Windows 서버 컴퓨터의 Boot.ini 파일에 지정 된 경우 커널 디버거를 시작 하는 동안 로드 하 고 모든 시점에 메모리에 저장 합니다. 이렇게 하면 디버깅 하 고 시스템에 전화 접속 및 디버거를 중단, 시스템 커널 중지 화면에서 일시 중단 되지 않은 경우에 지원 전문가입니다. **/Crashdebug** 스위치와는 달리 디버그/스위치는 있는지 여부를 디버깅 하는 COM 포트를 사용 합니다. 이 스위치는 정기적으로 발생할 수 있는 문제를 디버깅 하는 경우에 사용 됩니다. 디버그/매개 변수는 문제를 해결 하기 위한 수단으로 설정 된 및 설정 되었는데 우연히 가능성이 높습니다.

실행 되는 추가 프로세스로 인해 성능이 크게 저하. 따라서 Exchange Server 컴퓨터에 Windows 디버그 모드에서 실행 되 고 있는 권장 되지 않습니다.

이 오류를 제거 하려면 Boot.ini 파일을 편집 하 고 디버그/매개 변수를 제거 합니다.

## 이 오류를 수정하려면 다음을 수행합니다.

1.  Windows 탐색기에서 시스템 파티션으로 이동 합니다. Boot.ini 및 NTLDR와 같은 하드웨어 특정 파일을 포함 하는 파티션입니다.

2.  Boot.ini 파일을 볼 수 없는 경우 **폴더 옵션숨기기 보호 된 운영 체제 파일을**설정 하기 때문에 때문일 수 있습니다. Windows 탐색기 창에는 경우에는 해당 하는 경우 **도구**, **폴더 옵션**을 클릭 하 고 **보기**를 클릭 합니다. **보호 된 운영 체제 파일 (권장) 숨기기** 확인란의 선택을 취소 합니다. 대화 상자가 나타나면 **예**를 클릭 합니다.

3.  Boot.ini 파일 Windows 탐색기에 표시 되 면 파일을 마우스 오른쪽 단추로 클릭, **연결**을 클릭 하 고 **메모장** 파일을 여를 선택 합니다.

4.  **\[운영 체제\]** 섹션에서 디버그/매개 변수를 제거 합니다.

5.  하 여 파일을 저장 하 고 닫은 다음 변경 내용을 적용 하려면 Exchange Server 컴퓨터를 다시 시작 합니다.

Boot.ini 파일에서 사용할 수 있는 매개 변수에 대 한 자세한 내용은 Microsoft 기술 자료 문서 833721, "Windows XP 및 Windows Server 2003 Boot.ini 파일에 대 한 사용 가능한 스위치 옵션"을 참조 하십시오. ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052&kbid=833721)).


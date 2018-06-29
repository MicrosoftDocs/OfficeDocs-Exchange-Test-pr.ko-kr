---
title: '메시지 포함 되는 문서를 무시할 수 있도록 메일 흐름 규칙을 사용 하 여: Exchange 2013 Help'
TOCTitle: 메시지 포함 되는 문서를 무시할 수 있도록 메일 흐름 규칙을 사용 하 여
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64363186
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 포함 되는 문서를 무시할 수 있도록 메일 흐름 규칙을 사용 하 여

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

특정 메시지를 받을 수 있는지 확인 하려는 경우에 이러한 메시지 검사 간단 하 게 표시 폴더를 우회 하 게 하는 Exchange 전송 규칙을 만들 수 있습니다. 포함 되는 문서에 대 한 추가 정보에 대 한 [낮은 우선순위 메시지를 Outlook Web App에서 정렬에 포함 되는 사용 하 여 문서](https://go.microsoft.com/fwlink/p/?linkid=528411) 를 체크아웃 합니다.

전송 규칙과 관련 된 추가 관리 작업에 대 한 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) 및 [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\)) PowerShell 항목 체크아웃 합니다. PowerShell의 새로운 기능 인 경우 다음 Powershell을 사용 하 여에 대 한 도움말 항목을 확인해보세요.

  - [원격 PowerShell을 사용하여 Exchange Online에 연결](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))

  - [원격 셸을 사용하여 Exchange에 연결](https://technet.microsoft.com/ko-kr/library/dd335083\(v=exchg.150\))

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "전송 규칙" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## UI를 사용 하 여 간단 하 게 표시 폴더를 무시 하도록 전송 규칙을 만들려면

이 예제에서는 "회의" 간단 하 게 표시 하지 않으려면 제목이 있는 모든 메시지를 허용 합니다.

1.  Exchange 관리 센터에서 **메일 흐름** 으로 이동 \> **규칙** 입니다. ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 를 클릭 하 고 **... 새 규칙 만들기** 를 선택 합니다.

2.  마치면 새 규칙 만들기 (영문) 규칙을 시작 하려면 **저장** 을 클릭 합니다.

![아트 예제: 제목에 모임이 포함되어 있으면 낮은 우선 순위 메일 바이패스](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "아트 예제: 제목에 모임이 포함되어 있으면 낮은 우선 순위 메일 바이패스")

## 셸을 사용 하 여 간단 하 게 표시 폴더를 바이패스 하는 전송 규칙 만들기

이 예제에서는 "회의" 간단 하 게 표시 하지 않으려면 제목이 있는 모든 메시지를 허용 합니다.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> 이 예제에서는 "X-MS-Exchange-조직-BypassClutter"와 "true"은 대/소문자 구분 합니다.



구문과 매개 변수에 대한 자세한 내용은 [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

전자 메일 메시지 헤더를 간단 하 게 표시 전송 규칙으로 인해 받은 편지함에 전자 메일 메시지는 방문 하는 경우 무시를 확인할 수 있습니다. 전송 규칙을 적용 바이패스는 간단 하 게 표시 된 조직에 사서함에서 전자 메일 메시지를 선택 합니다. 헤더에 게 메시지를 표시 하는 확인 하 고 확인할 수는 **X-MS-Exchange-조직-BypassClutter: true** 헤더입니다. 이 바이패스가 작동 하는 것을 의미 합니다. 헤더 정보를 확인 하는 방법에 대 한 정보에 대 한 [전자 메일 메시지에 대 한 인터넷 헤더 정보 보기](https://go.microsoft.com/fwlink/p/?linkid=822530) 항목을 확인 합니다.


> [!NOTE]
> 일정 항목, 허용, 전송 하거나 거절 모임에서 이러한 헤더를 갖지 않도록와 동일 하 게 합니다. 곧 이러한 일정 항목에 포함 되는 문서 기능 확장 (영문) 진행 중입니다.



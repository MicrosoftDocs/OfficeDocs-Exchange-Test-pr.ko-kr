---
title: '공용 폴더 계층 구조 업데이트: Exchange 2013 Help'
TOCTitle: 공용 폴더 계층 구조 업데이트
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52058020
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더 계층 구조 업데이트

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2014-04-03_

계층 구조 동기화 장치 및 사서함 도우미를 수동으로 호출하려는 경우에만 공용 폴더 계층 구조를 업데이트해야 합니다. 둘 다 조직의 각 공용 폴더 사서함에 대해 24시간에 한 번 이상 호출됩니다. 계층 구조 동기화 장치는 사용자가 Microsoft Outlook 또는 Microsoft Exchange 웹 서비스 클라이언트를 통해 보조 사서함에 로그온되어 있는 경우 15분마다 호출됩니다.

Exchange Online의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

Exchange Server 2013의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "공용 폴더" 항목

  - EAC에서는 이 절차를 수행할 수 없으며, 셸을 사용해야 합니다.

  - *InvokeSynchronizer* 매개 변수를 포함하여 이 명령을 실행할 때는 *SuppressStatus* 매개 변수를 사용하는 것이 좋습니다. 명령에서 이 매개 변수를 사용하지 않으면 출력에서 최대 1분 동안 3초마다 상태 메시지를 표시합니다. 1분이 지나야 해당 셸 인스턴스를 사용할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 공용 폴더 계층 구조 업데이트

이 예에서는 공용 폴더 사서함 PF\_marketing에 대한 공용 폴더 계층 구조를 업데이트하고 명령 출력은 표시하지 않습니다.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

이 예에서는 모든 공용 폴더 사서함을 업데이트하고 명령 출력은 표시하지 않습니다.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus


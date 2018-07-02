---
title: 'Exchange 관리 센터에 대 한 내부 및 외부 Url 찾기: Exchange 2013 Help'
TOCTitle: Exchange 관리 센터에 대 한 내부 및 외부 Url 찾기
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50482924
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 관리 센터에 대 한 내부 및 외부 Url 찾기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-04_

EAC(Exchange 관리 센터)가 Exchange Server 2013의 웹 기반 관리 콘솔이기 때문에 웹 브라우저에서 ECP 가상 디렉터리 URL을 사용하여 EAC에 액세스합니다. 이 항목에서는 ECP 가상 디렉터리 URL을 찾는 방법을 보여줍니다.


> [!NOTE]
> ECP는 Exchange Server 2010용으로 개발된 웹 기반 사용자 인터페이스입니다. 가상 디렉터리에 대한 EAC cmdlet은 여전히 이름에 "ECP"를 사용하며, 이러한 cmdlet을 사용하여 Exchange 2010 및 Exchange 2013 ECP 가상 디렉터리를 관리할 수 있습니다.



EAC에 대한 자세한 내용은 [Exchange 2013의 Exchange 관리 센터](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이 절차를 수행하는 데 EAC를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "Exchange 관리 센터 연결" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 ECP 가상 디렉터리의 내부 및 외부 URL 찾기

이 예에서는 ECP 가상 디렉터리 이름, 내부 URL 및 외부 URL을 서식이 지정된 목록으로 반환합니다.

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

명령이 완료되면 웹 브라우저에서 *InternalURL* 또는 *ExternalURL* 값을 사용하여 EAC를 시작합니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd351058\(v=exchg.150\))를 참조하십시오.


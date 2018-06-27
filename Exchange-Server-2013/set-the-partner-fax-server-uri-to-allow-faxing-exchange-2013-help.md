---
title: '팩스 서버 팩스를 허용 하는 URI 파트너를 설정 합니다.: Exchange 2013 Help'
TOCTitle: 팩스 서버 팩스를 허용 하는 URI 파트너를 설정 합니다.
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52057997
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 팩스 서버 팩스를 허용 하는 URI 파트너를 설정 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM(통합 메시징) 사서함 정책과 연결된 사용자에 대해 인바운드 팩스를 사용하거나 사용하지 않도록 설정할 수 있습니다. 기본적으로 사용자가 UM을 사용할 수 있도록 설정할 경우 해당 사용자는 UM 사서함 정책에 대해 인바운드 팩스를 사용하도록 설정하고 파트너 팩스 서버에 대해 URI를 지정할 때까지는 팩스 메시지를 수신할 수 없습니다. UM 사서함 정책에 대해 URI가 구성되었지만 수신 팩스를 허용하는 옵션이 UM 다이얼 플랜이나 개별 사용자에 대해 사용하지 않도록 설정된 경우 UM 사서함 정책에 연결된 UM 사용 가능 사용자는 계속해서 팩스를 수신할 수 없습니다.

팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)를 참조 하십시오.

팩스와 관련된 추가 관리 작업에 대한 자세한 내용은 [절차를 팩스](faxing-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 팩스 파트너 URI 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 수정하려는 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **일반**에 있는 **파트너 팩스 서버 URI** 상자에 TCP나 TLS URI를 입력합니다. 예를 들면 다음과 같습니다. *sip:faxserver1.contoso.com:5060;transport=tcp* 또는 *sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!NOTE]
    > 상자에 둘 이상의 팩스 서버 URI가 포함되어도 하나만 사용됩니다. 두 개의 URI를 입력한 경우 첫 번째 URI만 사용됩니다.



4.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 팩스 파트너 URI 설정

이 예에서는 UM 사서함 정책 `UMDialPlan Default Policy`에 연결된 사용자가 파트너 팩스 서버 `faxserver1`에 대해 TCP 5060 포트를 사용할 수 있도록 허용합니다.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

이 예에서는 UM 사서함 정책 `UMDialPlan Default Policy`에 연결된 사용자가 파트너 팩스 서버 `faxserver2`에 대해 TLS 5061 포트를 사용할 수 있도록 허용합니다.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls


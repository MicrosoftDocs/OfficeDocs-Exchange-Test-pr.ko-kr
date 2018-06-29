---
title: '메일 사용이 가능한 또는 공용 폴더 메일-사용 안함: Exchange 2013 Help'
TOCTitle: 메일 사용이 가능한 또는 공용 폴더 메일-사용 안함
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50482907
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 사용이 가능한 또는 공용 폴더 메일-사용 안함

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-06-15_

공용 폴더 공유 액세스를 위해 설계 되었으며를 간편 하 고 효율적으로 수집, 구성 및 작업 그룹 또는 조직에서 다른 사용자와 정보를 공유할 수입니다. 공용 폴더가 메일을 사용 하도록 설정 하 여 전자 메일 메시지를 전송 하 여 공용 폴더에 게시할 수 있습니다. 공용 폴더가 추가 설정 메일 사용이 가능한 메일 할당량 및 전자 메일 주소와 같은 Exchange 관리 센터 (EAC)에서 공용 폴더에 대해 사용할 수 있게 되는 경우입니다. 셸에서 메일 사용 가능 공용 폴더는 전에 있습니다 cmdlet을 사용 **Set-PublicFolder** 모든 해당 설정을 관리할 수입니다. 메일 사용이 가능한 공용 폴더를 되 면 설정을 관리 하는 **Set-PublicFolder** 및 **Set-MailPublicFolder** cmdlet 사용 합니다.

메일 사용이 가능한 공용 폴더에 메일을 보내려고 인터넷에서 사용자가 원할 경우 **Add-PublicFolderClientPermission** cmdlet를 사용 하 여 추가 권한을 설정 해야 합니다.

공용 폴더 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 사용자가 인터넷에서 메일 사용이 가능한 공용 폴더에 전자 메일 메시지를 보낼 수 있도록 공용 폴더에는 적어도 *CreateItems* 액세스 권한이 익명 계정에 부여 해야 합니다. 이 작업을 수행 하는 방법을 설명 하려는 경우 메일 사용이 가능한 공용 폴더에 전자 메일을 보내도록 허용 익명 사용자가체크아웃 합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md) 항목의 "공용 폴더" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 메일 사용이 가능한 또는 공용 폴더 메일-사용 안함

1.  **공용 폴더** \> **공용 폴더**로 이동합니다.

2.  목록 보기에서 메일 사용이 가능한 또는 메일 사용 안함 하려는 공용 폴더를 선택 합니다.

3.  세부 정보 창에서 **메일 설정활성화** 또는 **비활성화** 를 클릭 합니다.

4.  공용 폴더에 대 한 전자 메일을 사용할지 여부를 묻는 확인 하는 경우를 표시 하는 경고 상자입니다. **예** 를 계속을 클릭 합니다.

이 공용 폴더에 메일을 보낼를 외부 사용자가 메일 사용이 가능한 공용 폴더에 전자 메일을 보내도록 허용 익명 사용자의 단계를 수행 해야 합니다.

## 셸을 사용 하 여 메일 사용이 가능한 공용 폴더를

이 예에서는 메일을 사용할 수 있도록 공용 폴더 Help Desk.

    Enable-MailPublicFolder -Identity "\Help Desk"

이 예에서는 메일을 사용할 수 있도록 마케팅 공용 폴더 아래 공용 폴더 보고서 하지만 주소 목록에서 폴더를 숨깁니다.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

외부 사용자가이 공용 폴더에 메일을 보낼 수 메일 사용이 가능한 공용 폴더에 대 한 전자 메일을 보내도록 허용 익명 사용자의 단계를 수행 해야 합니다.

자세한 구문 및 매개 변수 정보 [Enable-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/aa998824\(v=exchg.150\))를 참조 합니다.

## 셸을 메일-사용할 수 없도록 설정할 공용 폴더 사용

이 예제에서는 메일을 사용할 수 없도록 공용 폴더 Marketing\\Reports 합니다.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

자세한 구문 및 매개 변수 정보에 대 한 [Disable-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/bb123781\(v=exchg.150\))를 참조 하십시오.

## 익명 사용자가 메일 사용이 가능한 공용 폴더에 전자 메일을 보내도록 허용

공용 폴더의 익명 계정에 사용 권한을 설정 하려면 Outlook 또는 셸을 중 하나를 사용할 수 있습니다. 익명 계정에 권한을 설정 하려면 EAC를 사용할 수 없습니다.

**Outlook 를 사용 하 여 익명 계정에 대 한 사용 권한을 설정 하려면**

1.  익명 사용자를 전자 메일 사용이 가능한 공용 폴더에 대 한 소유자 권한을 메일을 보낼 부여 되는 계정을 사용 하 여 Outlook 를 엽니다.

2.  **\< 사용자의 이름 \>-공용** 폴더로 이동 됩니다.

3.  변경 하려는 공용 폴더로 이동 합니다.

4.  마우스 오른쪽 단추로 클릭 공용 폴더에서 **속성** 을 클릭 한 다음 **사용 권한** 탭을 선택 합니다.

5.  **익명** 계정을 선택 하 고 **를 작성**, 아래에 있는 **항목 만들기** 선택한 다음 **확인** 을 클릭 합니다.

**셸을 사용 하 여 익명 계정에 대 한 사용 권한을 설정 하려면**

"고객 의견" 메일 사용이 가능한 공용 폴더에는 익명 계정에 대 한 `CreateItems` 권한이 설정 하는이 예제입니다.

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

자세한 구문 및 매개 변수 정보에 대 한 [Add-PublicFolderClientPermission](https://technet.microsoft.com/ko-kr/library/bb124743\(v=exchg.150\))를 참조 하십시오.


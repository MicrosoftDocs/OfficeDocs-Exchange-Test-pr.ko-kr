---
title: '새 조직에서 공용 폴더 설정: Exchange 2013 Help'
TOCTitle: 새 조직에서 공용 폴더 설정
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50483479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 새 조직에서 공용 폴더 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-11-09_

**요약:**  EAC에서 자신에 게 사용 권한 할당을 포함 하 여 공용 폴더를 설정 하는 방법입니다.

이 항목에서는 이전에 공용 폴더가 없었던 조직이나 새 조직에서 공용 폴더를 구성 및 실행하는 방법을 보여줍니다.


> [!NOTE]
> 공용 폴더에 대한 제한 및 저장소 할당량에 대한 자세한 내용은 다음 항목을 참조하세요. 
> <UL>
> <LI>
> <P>Office 365의 공용 폴더에 대한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 제한</A>을 참조하세요.</P>
> <LI>
> <P>온-프레미스 Exchange Server 2013의 공용 폴더에 대한 내용은 <A href="limits-for-public-folders-exchange-2013-help.md">공용 폴더의 제한</A>을 참조하세요.</P></LI></UL>



Exchange Server 2013의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

Exchange Online의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "공용 폴더" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 기본 공용 폴더 사서함 만들기

기본 공용 폴더 사서함은 공용 폴더 계층 구조의 쓰기 가능한 복사본 및 콘텐츠를 포함하며, 조직에 대해 만드는 첫 번째 공용 폴더 사서함입니다. 이후 공용 폴더 사서함은 보조 공용 폴더 사서함으로, 계층 구조의 읽기 전용 복사본 및 콘텐츠를 포함합니다.

자세한 단계는 [공용 폴더 사서함 만들기](create-a-public-folder-mailbox-exchange-2013-help.md)을 참조하십시오.

## 2단계: 첫 번째 공용 폴더 만들기

자세한 단계는 [공용 폴더 만들기](create-a-public-folder-exchange-2013-help.md)을 참조하십시오.

## 3단계: 공용 폴더에 대한 사용 권한 할당

공용 폴더를 만든 후에는 적어도 한 명의 사용자가 클라이언트에서 공용 폴더에 액세스하고 하위 폴더를 만들 수 있도록 **소유자** 권한 수준을 할당해야 합니다. 이후에 만들어지는 공용 폴더에는 상위 공용 폴더의 사용 권한이 상속됩니다.

1.  EAC(Exchange 관리 센터)에서 **공용 폴더** \> **공용 폴더**로 이동합니다.

2.  목록 보기에서 공용 폴더를 선택합니다.

3.  세부 정보 창의 **폴더 사용 권한**에서 **관리**를 클릭합니다.

4.  **공용 폴더 사용 권한**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **찾아보기**를 클릭하여 사용자를 선택합니다.

6.  **권한 수준** 목록에서 수준을 선택합니다. 적어도 한 명의 사용자가 **소유자**여야 합니다.

7.  **저장**을 클릭합니다.

8.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 위의 단계를 통해 적절한 사용 권한을 할당하여 여러 사용자를 추가할 수 있습니다. 확인란을 선택하거나 선택 취소하여 사용 권한 수준을 사용자 지정할 수도 있습니다. **소유자**와 같이 미리 정의된 권한 수준을 편집할 경우 권한 수준이 **사용자 지정**으로 변경됩니다.

셸을 사용하여 공용 폴더에 사용 권한을 할당하는 방법에 대한 자세한 내용은 [Add-PublicFolderClientPermission](https://technet.microsoft.com/ko-kr/library/bb124743\(v=exchg.150\))을 참조하십시오.

## 4단계(옵션): 메일 사용 가능 공용 폴더

사용자가 공용 폴더에 메일을 보내도록 하려면 메일을 사용 가능하도록 만듭니다. 이 단계는 선택입니다. 공용 폴더에서 메일을 사용할 수 없는 경우 사용자는 항목을 Outlook 내에서 끌어 공용 폴더에 메시지를 게시할 수 있습니다.

1.  EAC에서 **공용 폴더** \> **공용 폴더**로 이동합니다.

2.  목록 보기에서 메일을 사용하도록 설정할 공용 폴더를 선택합니다.

3.  세부 정보 창의 **메일 설정 - 사용 안 함**에서 **사용**을 클릭합니다.
    
    공용 폴더에 대한 메일을 사용하도록 설정할지 묻는 경고가 표시됩니다. **예**를 클릭합니다.

공용 폴더에서 메일을 사용할 수 있으며 공용 폴더의 이름이 공용 폴더의 별칭이 됩니다. 해당 이름의 여러 받는 사람이 있는 경우 공용 폴더의 별칭에 숫자가 추가됩니다. 예를 들어 SalesTeam이라는 메일 그룹이 있고 SalesTeam이라는 공용 폴더를 만든 다음 메일을 사용하도록 설정한 경우 해당 공용 폴더의 별칭은 SalesTeam1이 됩니다.

셸을 사용하여 공용 폴더에서 메일을 사용 가능하도록 설정하는 방법에 대한 자세한 내용은 [Enable-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/aa998824\(v=exchg.150\))를 참조하십시오.


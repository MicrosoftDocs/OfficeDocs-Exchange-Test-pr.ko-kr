---
title: '공용 폴더 만들기: Exchange 2013 Help'
TOCTitle: 공용 폴더 만들기
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50483394
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# 공용 폴더 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-02-24_

공용 폴더는 공유 액세스를 위해 설계된 폴더입니다. 이 폴더를 통해 간단하고 효율적으로 정보를 수집 및 구성하고 작업 그룹이나 조직의 다른 사람과 공유할 수 있습니다.

기본적으로 공용 폴더는 사용 권한 설정을 비롯한 상위 폴더의 설정을 상속받습니다.


> [!NOTE]
> 공용 폴더에 대한 제한 및 저장소 할당량에 대한 자세한 내용은 다음 항목을 참조하세요. 
> <UL>
> <LI>
> <P>Office 365의 공용 폴더에 대한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 제한</A>을 참조하세요.</P>
> <LI>
> <P>온-프레미스 Exchange Server 2013의 공용 폴더에 대한 내용은 <A href="limits-for-public-folders-exchange-2013-help.md">공용 폴더의 제한</A>을 참조하세요.</P></LI></UL>



공용 폴더 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md) 항목의 "공용 폴더" 항목

  - 먼저 공용 폴더 사서함을 만들지 않으면 공용 폴더를 만들 수 없습니다. 공용 폴더 사서함을 만드는 방법에 대한 자세한 내용은 [공용 폴더 사서함 만들기](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/create-public-folder-mailbox)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공용 폴더 만들기

EAC를 사용하여 공용 폴더를 만드는 경우에는 공용 폴더의 이름과 경로만 설정할 수 있습니다. 추가 설정을 구성하려면 공용 폴더를 만든 후 편집해야 합니다.

1.  **공용 폴더** \> **공용 폴더**로 이동합니다.

2.  이 공용 폴더를 기존 공용 폴더의 하위 공용 폴더로 만들려면 목록 보기에서 기존 공용 폴더를 클릭합니다. 최상위 공용 폴더를 만들려는 경우 이 단계를 건너뜁니다.

3.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **공용 폴더**에 새 폴더의 이름을 입력합니다.
    

    > [!IMPORTANT]
    > 공용 폴더를 만들 때 이름에 백슬래시(\)를 사용하지 마십시오.



5.  **경로** 상자에서 공용 폴더의 경로를 확인합니다. 원하는 경로가 아닌 경우 **취소**를 클릭하고 이 절차의 2단계를 수행합니다.

6.  **저장**을 클릭합니다.

## 셸을 사용하여 공용 폴더 만들기

이 예에서는 경로 Marketing\\2013에 Reports라는 공용 폴더를 만듭니다.

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> 공용 폴더를 만들 때 이름에 백슬래시(\)를 사용하지 마십시오.



구문과 매개 변수에 대한 자세한 내용은 [New-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa996405\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

공용 폴더가 만들어졌는지 확인하려면 다음을 수행합니다.

  - EAC에서 **새로 고침**을 클릭하여 공용 폴더 목록을 새로 고칩니다. 새 공용 폴더가 목록에 표시되어야 합니다.

  - 셸에서 다음 명령을 실행합니다.
    
    ```
    Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    ```

    ```
    Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    ```

    ```
    Get-PublicFolder -Recurse
    ```


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



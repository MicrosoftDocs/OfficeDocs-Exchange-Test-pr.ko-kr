---
title: '공용 폴더 사서함 만들기: Exchange 2013 Help'
TOCTitle: 공용 폴더 사서함 만들기
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50483276
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더 사서함 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2014-10-23_

공용 폴더를 만들려면 먼저 공용 폴더 사서함을 만들어야 합니다. 공용 폴더 사서함에는 계층 구조 정보와 공용 폴더에 대한 콘텐츠가 포함됩니다. 만드는 첫 번째 공용 폴더는 기본 계층 구조 사서함이 되며, 이 사서함에는 계층 구조의 쓰기 가능한 하나의 복사본이 포함됩니다. 만드는 그 이외의 공용 폴더 사서함은 보조 사서함이 되며, 이 사서함에는 계층 구조의 읽기 전용 복사본이 포함됩니다.


> [!NOTE]
> 공용 폴더에 대한 제한 및 저장소 할당량에 대한 자세한 내용은 다음 항목을 참조하세요. 
> <UL>
> <LI>
> <P>Office 365의 공용 폴더에 대한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 제한</A>을 참조하세요.</P>
> <LI>
> <P>온-프레미스 Exchange Server 2013의 공용 폴더에 대한 내용은 <A href="limits-for-public-folders-exchange-2013-help.md">공용 폴더의 제한</A>을 참조하세요.</P></LI></UL>



Exchange 2013의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

Exchange Online의 공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만

  - Exchange 2013 공용 폴더와 레거시 Exchange 서버에서 공용 폴더 같은 조직에 존재할 수 없습니다. 레거시 공용 폴더에 있을 때 공용 폴더 사서함을 만들려고 하면 오류 **배포에서 발견 된 기존 공용 폴더 받게 됩니다. 기존 공용 폴더 데이터를 마이그레이션하려면-HoldForMigration 스위치를 사용 하 여 새 공용 폴더 사서함을 만듭니다.**
    
    Exchange 2013의 공용 폴더를 만들 수 있습니다, 전에 Exchange 2013으로 레거시 공용 폴더 마이그레이션을 세워야 합니다. 이 작업을 수행 하려면 [직렬 마이그레이션을 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션](https://technet.microsoft.com/ko-kr/library/jj150486\(v=exchg.150\))의 단계를 수행 합니다. 다음이 단계를 마이그레이션된 공용 폴더를 저장 하는데 사용할 수 있는 공용 폴더 사서함을 만드는 방법을 표시 됩니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md) 항목의 "공용 폴더" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공용 폴더 사서함 만들기

1.  **공용 폴더** \> **공용 폴더 사서함**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **공용 폴더 사서함** 페이지에서 공용 폴더 사서함의 이름을 지정합니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 공용 폴더 사서함 만들기

이 예에서는 기본 공용 폴더 사서함을 만듭니다.

    New-Mailbox -PublicFolder -Name MasterHierarchy

이 예에서는 보조 공용 폴더 사서함을 만듭니다. 기본 계층 구조 사서함과 보조 계층 구조 사서함을 만들 때의 유일한 차이점은 기본 사서함이 먼저 조직에 만들어진다는 것뿐입니다. 부하 분산을 위해 공용 폴더 사서함을 추가로 만들 수 있습니다.

    New-Mailbox -PublicFolder -Name Istanbul 

구문과 매개 변수에 대한 자세한 내용은 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

기본 공용 폴더 사서함이 만들어졌는지 확인하려면 다음 셸 명령을 실행하십시오.

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

구문과 매개 변수에 대한 자세한 내용은 [Get-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997571\(v=exchg.150\))를 참조하십시오.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)


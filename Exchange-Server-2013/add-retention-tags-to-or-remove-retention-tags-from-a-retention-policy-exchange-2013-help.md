---
title: '보존 태그를 추가 하거나 보존 정책에서 보존 태그를 제거 합니다.: Exchange 2013 Help'
TOCTitle: 보존 태그를 추가 하거나 보존 정책에서 보존 태그를 제거 합니다.
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50482882
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보존 태그를 추가 하거나 보존 정책에서 보존 태그를 제거 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-02_

보존 정책을 만들 때 또는 그 후 언제든지 보존 정책에 보존 태그를 추가할 수 있습니다. 보존 태그를 동시에 추가하는 방법을 비롯하여 보존 정책을 만드는 방법에 대한 자세한 내용은 [보존 정책 만들기](create-a-retention-policy-exchange-2013-help.md)를 참조하십시오.

보존 정책에는 다음과 같은 보존 태그가 포함될 수 있습니다.

  - 지원되는 기본 폴더에 대한 하나 이상의 RPT(보존 정책 태그)

  - **보관함으로 이동** 작업이 있는 기본 정책 태그(DPT) 하나

  - **삭제 및 복구 허용** 또는 **영구 삭제** 작업이 포함된 하나의 DPT

  - 음성 메일에 대한 하나의 DPT

  - 임의 개수의 개인 태그

보존 태그에 대 한 자세한 내용은 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목

  - 보존 태그는 보존 정책에 연결 된 사서함을 관리 하는 폴더 도우미가 처리 될 때까지 사서함에 적용 되지 않습니다. 사서함을 처리할 수 있도록에 관리 되는 폴더 도우미를 시작 하 고, [관리 되는 폴더 도우미를 구성 합니다.](configure-the-managed-folder-assistant-exchange-2013-help.md)를 참조 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 추가 하거나 보존 태그를 제거 하려면

1.  **규정 준수 관리** 로 이동 \>**보존 정책** 입니다.

2.  목록 보기에서 보존 태그를 추가하려는 보존 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **보존 정책**에서 다음 설정을 사용합니다.
    
      - **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")   이 단추를 클릭하여 보존 태그를 정책에 추가합니다.
    
      - **제거** ![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")   목록에서 태그를 선택하고 이 단추를 클릭하여 정책에서 태그를 제거합니다.

## 셸을 사용 하 여 추가 또는 보존 태그를 제거 합니다.

이 예에서는 보존 태그가 아직 연결되어 있지 않은 보존 정책 RetPolicy-VPs에 보존 태그 VPs-Default, VPs-Inbox 및 VPs-DeletedItems를 추가합니다.


> [!WARNING]
> 정책에 보존 태그가 연결되어 있을 경우 이 명령은 기존 태그를 바꿉니다.



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

다음은 보존 태그 VPs-DeletedItems를 이미 다른 보존 태그가 연결되어 있는 보존 정책 RetPolicy-VPs에 추가하는 예입니다.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

이 예에서는 보존 정책 RetPolicy-VPs에서 보존 태그 VPs-Inbox를 제거합니다.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

구문과 매개 변수에 대한 자세한 내용은 [Set-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd335196\(v=exchg.150\)) 및 [Get-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd298086\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

보존 정책에서 보존 태그를 성공적으로 추가하거나 제거했는지 확인하려면 [Get-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd298086\(v=exchg.150\)) cmdlet을 사용하여 *RetentionPolicyTagLinks* 속성을 확인합니다.

이 예에서는 **Get-RetentionPolicy** cmdlet을 사용하여 Default MRM Policy에 추가된 보존 태그를 검색하고 검색한 태그를 **Format-Table** cmdlet으로 파이프하여 각 태그의 이름 속성만 출력합니다.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name


---
title: '그룹 메트릭 구성: Exchange 2013 Help'
TOCTitle: 그룹 메트릭 구성
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50483447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 그룹 메트릭 [2013] 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

메일 그룹 및 동적 메일 그룹의 크기 정보를 제공하는 메일 설명은 그룹 메트릭 데이터를 사용합니다. 그룹 메트릭 데이터는 지정된 사서함 서버에서 생성됩니다. 그룹 메트릭에 대한 자세한 내용은 [그룹 메트릭 및 메일 설명](group-metrics-and-https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips)를 참조하십시오.

사서함 서버에 대해 그룹 메트릭 생성을 사용하거나 사용하지 않도록 설정할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "그룹 메트릭" 항목

  - 그룹 메트릭 데이터는 메일 설명에만 사용됩니다. 조직에서 그룹 메트릭 메일 설명이 사용하도록 설정되었는지 확인합니다. 자세한 단계는 [조직 관계에 대 한 메일 설명 관리](https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships)을 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 그룹 메트릭 생성을 사용하거나 사용하지 않도록 설정


> [!NOTE]
> 기본적으로 그룹 메트릭 데이터는 OAB(오프라인 주소록)를 생성하는 서버에서 생성됩니다. 이러한 예는 OAB를 사용하지 않는 조직에서만 필요합니다.



사서함 서버에서 그룹 메트릭 생성을 사용하거나 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>
```

이 예에서는 MBX1이라는 사서함 서버에서 그룹 메트릭 생성을 사용하도록 설정합니다.

```powershell
Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true
```

## 작동 여부는 어떻게 확인합니까?

OAB를 사용하지 않는 조직에서 그룹 메트릭 생성을 사용하거나 사용하지 않도록 설정했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration
```

2.  표시된 설정이 구성한 설정과 같은지 확인합니다.


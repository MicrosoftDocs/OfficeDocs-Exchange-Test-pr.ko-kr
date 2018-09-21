---
title: '관리자가 관리 감사 로깅: Exchange 2013 Help'
TOCTitle: 관리자가 관리 감사 로깅
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50555944
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자가 관리 감사 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-05-17_

Microsoft Exchange Server 2013의 관리자 감사 로깅을 사용하면 지정된 cmdlet을 실행할 때마다 로그 항목을 만들 수 있습니다. 로그 항목은 실행된 cmdlet, 사용된 매개 변수, cmdlet을 실행한 사용자 및 영향을 받은 개체에 대한 정보를 제공합니다. 관리자 감사 로깅에 대한 자세한 내용은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "관리자 감사 로깅" 항목

  - 관리자 감사 로깅은 Active Directory 복제를 사용하여 지정한 구성 설정을 조직의 도메인 컨트롤러에 복제합니다. 복제 설정에 따라 변경한 내용이 조직의 일부 Microsoft Exchange 2013 서버에 즉시 적용되지 않을 수도 있습니다.

  - 감사 로그 구성의 변경 내용은 구성 변경 시 셸이 열리는 컴퓨터에서 60분마다 새로 고쳐집니다. 변경 내용을 즉시 적용하려면 각 컴퓨터에서 셸을 닫은 후 다시 여십시오.

  - 실행된 명령이 감사 로그 검색 결과에 나타나려면 최대 15분까지 걸릴 수 있습니다. 감사 로그 항목은 인덱싱되어야 검색이 가능하기 때문입니다. 명령이 관리자 감사 로그에 표시되지 않으면 몇 분간 기다렸다가 검색을 다시 실행해 보십시오.

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 감사할 cmdlet 지정

기본적으로 감사 로깅은 실행된 각 cmdlet에 대해 로그 항목을 만듭니다. 처음으로 감사 로깅을 사용하도록 설정하는 경우에는 이 동작을 사용하기 위해 cmdlet 감사 목록을 변경할 필요가 없습니다. 이전에 감사할 cmdlet을 지정했지만 지금 모든 cmdlet을 감사하려면 다음 명령에서와 같이 **Set-AdminAuditLogConfig** cmdlet에서 *AdminAuditLogCmdlets* 매개 변수에 별표(\*) 와일드카드 문자를 지정하면 모든 cmdlet을 감사할 수 있습니다.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

*AdminAuditLogCmdlets* 매개 변수를 사용하여 cmdlet 목록을 제공하면 감사할 cmdlet을 지정할 수 있습니다. 감사할 cmdlet의 목록을 제공할 경우에는 단일 cmdlet, 별표(\*) 와일드카드 문자가 있는 cmdlet 또는 이 두 가지를 혼합하여 제공할 수 있습니다. 목록에 있는 각 항목은 쉼표로 구분합니다. 유효한 값은 다음과 같습니다.

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

이 예에서는 위 목록에 지정된 cmdlet을 감사합니다.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

구문과 매개 변수에 대한 자세한 내용은 [Set-AdminAuditLogConfig](https://technet.microsoft.com/ko-kr/library/dd298169\(v=exchg.150\))를 참조하십시오.

## 감사할 매개 변수 지정

기본적으로 감사 로깅은 지정된 매개 변수에 관계없이 실행된 모든 cmdlet에 대해 로그 항목을 만듭니다. 처음으로 감사 로깅을 사용하도록 설정하는 경우에는 이 동작을 사용하기 위해 매개 변수 감사 목록을 변경할 필요가 없습니다. 이전에 감사할 매개 변수를 지정했지만 지금 모든 매개 변수를 감사하려면 다음 명령에서와 같이 **Set-AdminAuditLogConfig** cmdlet에서 *AdminAuditLogParameters* 매개 변수에 별표(\*) 와일드카드 문자를 지정하면 모든 매개 변수를 감사할 수 있습니다.

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

*AdminAuditLogParameters* 매개 변수를 사용하여 감사할 매개 변수를 지정할 수 있습니다. 감사할 매개 변수의 목록을 제공할 경우에는 단일 매개 변수, 별표(\*) 와일드카드 문자가 있는 매개 변수 또는 이 두 가지를 혼합하여 제공할 수 있습니다. 목록에 있는 각 항목은 쉼표로 구분합니다. 유효한 값은 다음과 같습니다.

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`


> [!NOTE]
> 명령을 실행할 때 감사 로그 항목을 만들려면 명령에 <EM>AdminAuditLogCmdlets</EM> 매개 변수로 지정된 하나 이상의 cmdlet에 있는 매개 변수가 하나 이상 포함되어야 합니다.



이 예에서는 위 목록에 지정된 매개 변수를 감사합니다.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

구문과 매개 변수에 대한 자세한 내용은 [Set-AdminAuditLogConfig](https://technet.microsoft.com/ko-kr/library/dd298169\(v=exchg.150\))를 참조하십시오.

## 감사 로그 보존 기간 지정

감사 로그 보존 기간은 감사 로그 항목을 유지할 기간을 결정합니다. 보존 기간이 지난 로그 항목은 삭제됩니다. 기본값은 90일입니다.

감사 로그 항목을 유지할 일수, 시간, 분 및 초를 지정할 수 있습니다. 값을 지정하려면 dd.hh.mm:ss 형식을 사용합니다. 여기서 각 항목은 다음을 나타냅니다.

  - **dd**   감사 로그 항목을 보존할 일수

  - **hh**   감사 로그 항목을 보존할 시간

  - **mm**   감사 로그 항목을 보존할 시간(분)

  - **ss**   감사 로그 항목을 보존할 시간(초)


> [!WARNING]
> 감사 로그 보존 기간을 현재 보존 기간보다 작게 설정할 수 있습니다. 이 경우 보존 기간이 새 보존 기간을 초과하는 모든 감사 로그 항목이 삭제됩니다.<BR>보존 기간을 0으로 설정할 경우 Exchange는 감사 로그의 모든 항목을 삭제합니다.<BR>감사 로그 보존 기간을 구성할 수 있는 권한은 신뢰할 수 있는 사용자에게만 부여하는 것이 좋습니다.



이 예에서는 보존 기간으로 2년 6개월을 지정합니다.

```powershell
Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00
```

구문과 매개 변수에 대한 자세한 내용은 [Set-AdminAuditLogConfig](https://technet.microsoft.com/ko-kr/library/dd298169\(v=exchg.150\))를 참조하십시오.

## Test cmdlet 로깅을 사용하거나 사용하지 않도록 설정

동사 **Test**로 시작하는 cmdlet은 기본적으로 기록되지 않습니다. 이는 **Test** cmdlet이 단시간에 많은 양의 데이터를 생성할 수 있기 때문입니다. 짧은 시간 동안만 **Test** cmdlet 로깅을 사용하도록 설정하십시오.

이 명령은 **Test** cmdlet의 로깅을 사용하도록 설정합니다.

```powershell
Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True
```

이 명령은 **Test** cmdlet의 로깅을 사용하지 않도록 설정합니다.

```powershell
Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False
```

구문과 매개 변수에 대한 자세한 내용은 [Set-AdminAuditLogConfig](https://technet.microsoft.com/ko-kr/library/dd298169\(v=exchg.150\))를 참조하십시오.

## 관리자 감사 로깅 사용 안 함

관리자 감사 로깅을 사용하지 않도록 설정하려면 다음 명령을 사용합니다.

```powershell
Set-AdminAuditLogConfig -AdminAuditLogEnabled $False
```

## 관리자 감사 로깅 사용

관리자 감사 로깅을 사용하도록 설정하려면 다음 명령을 사용합니다.

```powershell
Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
```

## 관리자 감사 로깅 설정 보기

조직에 대해 구성한 관리자 감사 로깅 설정을 보려면 다음 명령을 사용합니다.

```powershell
Get-AdminAuditLogConfig
```


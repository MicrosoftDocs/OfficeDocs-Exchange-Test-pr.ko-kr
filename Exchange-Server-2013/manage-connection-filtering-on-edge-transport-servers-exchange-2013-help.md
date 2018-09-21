---
title: 'Edge 전송 서버에서 연결 필터링 관리: Exchange 2013 Help'
TOCTitle: Edge 전송 서버에서 연결 필터링 관리
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60829916
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버에서 연결 필터링 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

연결 필터링은 연결 필터링 에이전트에서 제공되지 않는 스팸 방지 기능으로, Microsoft Exchange 2013의 Edge 전송 서버에서만 사용할 수 있습니다. 연결 필터링을 통해 다음 기능을 사용할 수 있습니다.

  - IP 차단 목록

  - IP 차단 목록 공급자

  - IP 허용 목록

  - IP 허용 목록 공급자

이러한 각 기능은 개별적으로 사용하거나 사용하지 않도록 설정할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 연결 필터링을 사용하거나 사용하지 않도록 설정

연결 필터링을 완전히 사용하거나 사용하지 않도록 설정하려면 연결 필터링 에이전트를 사용하거나 사용하지 않도록 설정합니다. 변경 내용은 Microsoft Exchange Transport Service를 다시 시작한 후에 적용됩니다. Edge 전송 서버에서 Microsoft Exchange Transport Service를 다시 시작하면 서버의 메일 흐름이 일시적으로 중지됩니다.

연결 필터링을 사용하지 않으려면 다음 명령을 실행합니다.

```powershell
Disable-TransportAgent "Connection Filtering Agent"
```

연결 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Enable-TransportAgent "Connection Filtering Agent"
```

변경 내용을 적용하려면 다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작해야 합니다.

```powershell
Restart-Service MSExchangeTransport
```

## 작동 여부는 어떻게 확인합니까?

연결 필터링이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled
```

## IP 차단 목록 절차

다음 절차는 수동으로 구성한 IP 차단 목록에 적용됩니다. IP 차단 목록 공급자에는 적용되지 않습니다.

**IPBlockListConfig** cmdlet을 사용하여 연결 필터링에서 IP 차단 목록을 사용하는 방법을 보고 구성합니다. IP 차단 목록에서 IP 주소를 보고 구성하려면 **IPBlockListEntry** cmdlet을 사용합니다.

## 셸을 사용하여 IP 차단 목록의 구성 보기

IP 차단 목록의 구성을 확인하려면 다음 명령을 실행합니다.

    Get-IPBlockListConfig | Format-List *Enabled,*Response

## 셸을 사용하여 IP 차단 목록을 사용하거나 사용하지 않도록 설정

IP 차단 목록을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPBlockListConfig -Enabled $false
```

IP 차단 목록을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPBlockListConfig -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPBlockListConfig | Format-List Enabled
```

## 셸을 사용하여 IP 차단 목록 구성

IP 차단 목록을 구성하려면 다음 구문을 사용합니다.

    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]

이 예에서는 다음과 같은 설정으로 IP 차단 목록을 구성합니다.

  - IP 차단 목록은 내부 및 외부 메일 서버에서 들어오는 연결을 필터링합니다. 기본적으로 외부 메일 서버의 연결만 필터링됩니다(*ExternalMailEnabled*가 `$true`로 설정되고, *InternalMailEnabled*가 `$false`로 설정됨). 인증되지 않은 연결과 외부 파트너의 인증된 연결은 외부 연결로 간주됩니다.

  - 프로토콜 분석 에이전트의 보낸 사람 신뢰도 기능을 통해 IP 차단 목록에 자동으로 추가된 IP 주소별로 필터링된 연결에 대한 사용자 지정 응답 텍스트는 "IP 주소 {0}의 연결이 보낸 사람 신뢰도에 의해 거부됨" 값으로 설정됩니다.

  - IP 차단 목록에 수동으로 추가된 IP 주소별로 필터링된 연결에 대한 사용자 지정 응답 텍스트는 "IP 주소 {0}의 연결이 연결 필터링에 의해 거부됨" 값으로 설정됩니다.

<!-- end list -->

    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록을 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

    Get-IPBlockListConfig | Format-List *MailEnabled,*Response

## 셸을 사용하여 IP 차단 목록 항목 보기

모든 IP 차단 목록 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPBlockListEntry
```

각 IP 차단 목록 항목은 정수 값으로 식별됩니다. IP 차단 목록과 IP 허용 목록에 항목을 추가하면 정수 ID가 오름차순으로 할당됩니다.

특정 IP 차단 목록 항목을 보려면 다음 구문을 사용합니다.

```powershell
Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

예를 들어 IP 주소 192.168.1.13이 포함된 IP 차단 목록 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> <EM>IPAddress</EM> 매개 변수를 사용한 경우 결과 IP 차단 목록 항목은 개별 IP 주소, IP 주소 범위 또는 CIDR(Classless InterDomain Routing) IP일 수 있습니다. <EM>Identity</EM> 매개 변수를 사용하려면 IP 차단 목록 항목에 할당된 정수 값을 지정합니다.



## 셸을 사용하여 IP 차단 목록 항목 추가

IP 차단 목록 항목을 추가하려면 다음 구문을 사용합니다.

    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]

다음 예에서는 IP 주소 범위 192.168.1.10~192.168.1.15에 대해 IP 차단 목록 항목을 추가하고 2014년 7월 4일 오후 3시에 만료되도록 IP 차단 목록 항목을 구성합니다.

```powershell
Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 항목을 올바르게 추가했는지 확인하려면 다음 명령을 실행하여 새 IP 차단 목록 항목이 표시되는지 확인합니다.

```powershell
Get-IPBlockListEntry
```

## 셸을 사용하여 IP 차단 목록 항목 제거

IP 차단 목록 항목을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-IPBlockListEntry <IdentityInteger>
```

다음 예에서는 *Identity* 값이 3인 IP 차단 목록 항목을 제거합니다.

```powershell
Remove-IPBlockListEntry 3
```

다음 예에서는 *Identity* 정수 값을 사용하지 않고 IP 주소 192.168.1.12가 포함된 IP 차단 목록 항목을 제거합니다. IP 차단 목록 항목은 개별 IP 주소 또는 IP 주소 범위일 수 있습니다.

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry
```

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 항목을 올바르게 제거했는지 확인하려면 다음 명령을 실행하여 제거한 IP 차단 목록 항목이 사라졌는지 확인합니다.

```powershell
Get-IPBlockListEntry
```

## IP 차단 목록 공급자 절차

다음 절차는 IP 차단 목록 공급자에 적용됩니다. IP 차단 목록에는 적용되지 않습니다.

**IPBlockListProvidersConfig** cmdlet을 사용하여 연결 필터링에서 모든 IP 차단 목록 공급자를 사용하는 방법을 보고 구성합니다. IP 차단 목록 공급자를 확인, 구성 및 테스트하려면 **IPBlockListProvider** cmdlet을 사용합니다.

## 셸을 사용하여 모든 IP 차단 목록 공급자의 구성 보기

콘텐츠 필터링에서 모든 IP 차단 목록 공급자를 사용하는 방법을 보려면 다음 명령을 실행합니다.

    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*

## 셸을 사용하여 모든 IP 차단 목록 공급자를 사용하거나 사용하지 않도록 설정

모든 IP 차단 목록 공급자를 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPBlockListProvidersConfig -Enabled $false
```

모든 IP 차단 목록 공급자를 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPBlockListProvidersConfig -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

모든 IP 차단 목록이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPBlockListProvidersConfig | Format-List Enabled
```

## 셸을 사용하여 모든 IP 차단 목록 공급자 구성

콘텐츠 필터링에서 모든 IP 차단 목록 공급자를 사용하는 방법을 구성하려면 다음 구문을 사용합니다.

    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

다음 예에서는 아래 설정을 사용하여 모든 IP 차단 목록 공급자를 구성합니다.

  - IP 차단 목록 공급자는 내부 및 외부 메일 서버에서 들어오는 연결을 필터링합니다. 기본적으로 외부 메일 서버의 연결만 필터링됩니다(*ExternalMailEnabled*가 `$true`로 설정되고, *InternalMailEnabled*가 `$false`로 설정됨). 인증되지 않은 연결과 외부 파트너의 인증된 연결은 외부 연결로 간주됩니다.

  - 내부 받는 사람 chris@fabrikam.com 및 michelle@fabrikam.com으로 전송된 메시지는 IP 차단 목록 공급자의 필터링 대상에서 제외됩니다. 기존 받는 사람에게 영향을 주지 않고 목록에 받는 사람을 추가하려면 `@{Add="<recipient1>","<recipient2>"...}` 구문을 사용해야 합니다.

<!-- end list -->

    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true

자세한 내용은 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/ko-kr/library/aa998543\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

모든 IP 차단 목록 공급자를 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*

## 셸을 사용하여 IP 차단 목록 공급자 보기

모든 IP 차단 목록 공급자의 요약 목록을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPBlockListProvider
```

특정 공급자의 세부 정보를 보려면 다음 구문을 사용합니다.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity>
```

다음 예에서는 Contoso IP Block List Provider라는 공급자의 세부 정보를 표시합니다.

    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response

## 셸을 사용하여 IP 차단 목록 공급자 추가

IP 차단 목록 공급자를 추가하려면 다음 구문을 사용합니다.

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

다음 예에서는 아래 옵션으로 "Contoso IP Block List Provider"라는 IP 차단 목록 공급자을 만듭니다.

  - **공급자를 사용할 FQDN**   rbl.contoso.com

  - **공급자에서 사용할 비트 마스크 코드**   127.0.0.1

<!-- end list -->

    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1


> [!NOTE]
> 새 IP 차단 목록 공급자를 추가한 경우 기본적으로 사용하도록 설정되고(<EM>Enabled</EM> 값이 <CODE>$true</CODE>), 우선 순위 값이 증분됩니다(첫 번째 항목의 <EM>Priority</EM> 값이 1).



자세한 내용은 [Add-IPBlockListProvider](https://technet.microsoft.com/ko-kr/library/bb124358\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 공급자를 올바르게 추가했는지 확인하려면 다음 명령을 실행하여 새 IP 차단 목록 공급자가 표시되는지 확인합니다.

```powershell
Get-IPBlockListProvider
```

## 셸을 사용하여 IP 차단 목록 공급자를 사용하거나 사용하지 않도록 설정

특정 IP 차단 목록 공급자를 사용하거나 사용하지 않도록 설정하려면 다음 구문을 사용합니다.

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>
```

다음 예에서는 Contoso IP Block List Provider라는 공급자를 사용하지 않도록 설정합니다.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false
```

다음 예에서는 Contoso IP Block List Provider라는 공급자를 사용하도록 설정합니다.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 공급자가 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled
```

## 셸을 사용하여 IP 차단 목록 공급자 구성

**Set-IPBlockListProvider** cmdlet에서 사용할 수 있는 구성 옵션은 **New-IPBlockListProvider** cmdlet의 구성 옵션과 동일합니다.

기존 IP 차단 목록 공급자를 구성하려면 다음 구문을 사용합니다.

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

예를 들어 Contoso IP Block List Provider라는 공급자의 기존 상태 코드 목록에 IP 주소 상태 코드 127.0.0.1을 추가하려면 다음 명령을 실행합니다.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

자세한 내용은 [Set-IPBlockListProvider](https://technet.microsoft.com/ko-kr/library/bb124979\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 공급자를 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List
```

## 셸을 사용하여 IP 차단 목록 공급자 테스트

IP 차단 목록 공급자를 테스트하려면 다음 구문을 사용합니다.

```powershell
Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>
```

다음 예에서는 IP 주소 192.168.1.1을 조회하여 Contoso IP Block List Provider라는 공급자를 테스트합니다.

```powershell
Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1
```

## 셸을 사용하여 IP 차단 목록 공급자 제거

IP 차단 목록 공급자를 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-IPBlockListProvider <IPBlockListProviderIdentity>
```

다음 예에서는 Contoso IP Block List Provider라는 IP 차단 목록 공급자를 제거합니다.

```powershell
Remove-IPBlockListProvider "Contoso IP Block list Provider"
```

## 작동 여부는 어떻게 확인합니까?

IP 차단 목록 공급자를 올바르게 제거했는지 확인하려면 다음 명령을 실행하여 제거한 IP 차단 목록 공급자가 사라졌는지 확인합니다.

```powershell
Get-IPBlockListProvider
```

## IP 허용 목록 절차

다음 절차는 수동으로 구성한 IP 허용 목록에 적용됩니다. IP 허용 목록 공급자에는 적용되지 않습니다.

**IPAllowListConfig** cmdlet을 사용하여 연결 필터링에서 IP 허용 목록을 사용하는 방법을 보고 구성합니다. IP 허용 목록에서 IP 주소를 보고 구성하려면 **IPAllowListEntry** cmdlet을 사용합니다.

## 셸을 사용하여 IP 허용 목록의 구성 보기

IP 허용 목록의 구성을 확인하려면 다음 명령을 실행합니다.

    Get-IPAllowListConfig | Format-List *Enabled

## 셸을 사용하여 IP 허용 목록을 사용하거나 사용하지 않도록 설정

IP 허용 목록을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPAllowListConfig -Enabled $false
```

IP 허용 목록을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPAllowListConfig -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPAllowListConfig | Format-List Enabled
```

## 셸을 사용하여 IP 허용 목록 구성

IP 허용 목록을 구성하려면 다음 구문을 사용합니다.

    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>

다음 예에서는 내부 및 외부 메일 서버에서 들어오는 연결을 필터링하도록 IP 허용 목록을 구성합니다. 기본적으로 외부 메일 서버의 연결만 필터링됩니다(*ExternalMailEnabled*가 `$true`로 설정되고, *InternalMailEnabled*가 `$false`로 설정됨). 인증되지 않은 연결과 외부 파트너의 인증된 연결은 외부 연결로 간주됩니다.

```powershell
Set-IPAllowListConfig -InternalMailEnabled $true
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록을 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

    Get-IPAllowListConfig | Format-List *MailEnabled

## 셸을 사용하여 IP 허용 목록 항목 보기

모든 IP 허용 목록 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPAllowListEntry
```

각 IP 허용 목록 항목은 정수 값으로 식별됩니다. IP 차단 목록과 IP 허용 목록에 항목을 추가하면 정수 ID가 오름차순으로 할당됩니다.

특정 IP 허용 목록 항목을 보려면 다음 구문을 사용합니다.

```powershell
Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

예를 들어 IP 주소 192.168.1.13이 포함된 IP 허용 목록 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> <EM>IPAddress</EM> 매개 변수를 사용한 경우 결과 IP 허용 목록 항목은 개별 IP 주소, IP 주소 범위 또는 CIDR(Classless InterDomain Routing) IP일 수 있습니다. <EM>Identity</EM> 매개 변수를 사용하려면 IP 허용 목록 항목에 할당된 정수 값을 지정합니다.



## 셸을 사용하여 IP 허용 목록 항목 추가

IP 허용 목록 항목을 추가하려면 다음 구문을 사용합니다.

    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]

다음 예에서는 IP 주소 범위 192.168.1.10~192.168.1.15에 대해 IP 허용 목록 항목을 추가하고 2014년 7월 4일 오후 3시에 만료되도록 IP 허용 목록 항목을 구성합니다.

```powershell
Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 항목을 올바르게 추가했는지 확인하려면 다음 명령을 실행하여 새 IP 허용 목록 항목이 표시되는지 확인합니다.

```powershell
Get-IPAllowListEntry
```

## 셸을 사용하여 IP 허용 목록 항목 제거

IP 허용 목록 항목을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-IPAllowListEntry <IdentityInteger>
```

다음 예에서는 *Identity* 값이 3인 IP 허용 목록 항목을 제거합니다.

```powershell
Remove-IPAllowListEntry 3
```

다음 예에서는 *Identity* 정수 값을 사용하지 않고 IP 주소 192.168.1.12가 포함된 IP 허용 목록 항목을 제거합니다. IP 허용 목록 항목은 개별 IP 주소 또는 IP 주소 범위일 수 있습니다.

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 항목을 올바르게 제거했는지 확인하려면 다음 명령을 실행하여 제거한 IP 허용 목록 항목이 사라졌는지 확인합니다.

```powershell
Get-IPAllowListEntry
```

## IP 허용 목록 공급자 절차

다음 절차는 IP 허용 목록 공급자에 적용됩니다. IP 허용 목록에는 적용되지 않습니다.

**IPAllowListProvidersConfig** cmdlet을 사용하여 연결 필터링에서 모든 IP 허용 목록 공급자를 사용하는 방법을 보고 구성합니다. IP 허용 목록 공급자를 확인, 구성 및 테스트하려면 **IPAllowListProvider** cmdlet을 사용합니다.

## 셸을 사용하여 모든 IP 허용 목록 공급자의 구성 보기

콘텐츠 필터링에서 모든 IP 허용 목록 공급자를 사용하는 방법을 보려면 다음 명령을 실행합니다.

    Get-IPAllowListProvidersConfig | Format-List *Enabled

## 셸을 사용하여 모든 IP 허용 목록 공급자를 사용하거나 사용하지 않도록 설정

모든 IP 허용 목록 공급자를 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPAllowListProvidersConfig -Enabled $false
```

모든 IP 허용 목록 공급자를 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-IPAllowListProvidersConfig -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

모든 IP 허용 목록이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPAllowListProvidersConfig | Format-List *Enabled
```

## 셸을 사용하여 모든 IP 허용 목록 공급자 구성

콘텐츠 필터링에서 모든 IP 허용 목록 공급자를 사용하는 방법을 구성하려면 다음 구문을 사용합니다.

    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

다음 예에서는 내부 및 외부 메일 서버에서 들어오는 연결을 필터링하도록 모든 IP 허용 목록 공급자를 구성합니다. 기본적으로 외부 메일 서버의 연결만 필터링됩니다(*ExternalMailEnabled*가 `$true`로 설정되고, *InternalMailEnabled*가 `$false`로 설정됨). 인증되지 않은 연결과 외부 파트너의 인증된 연결은 외부 연결로 간주됩니다.

```powershell
Set-IPAllowListProvidersConfig -InternalMailEnabled $true
```

자세한 내용은 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/ko-kr/library/aa998543\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

모든 IP 허용 목록 공급자를 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

    Get-IPAllowListProvidersConfig | Format-List *MailEnabled

## 셸을 사용하여 IP 허용 목록 공급자 보기

모든 IP 허용 목록 공급자의 요약 목록을 보려면 다음 명령을 실행합니다.

```powershell
Get-IPAllowListProvider
```

특정 공급자의 세부 정보를 보려면 다음 구문을 사용합니다.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity>
```

다음 예에서는 Contoso IP Allow List Provider라는 공급자의 세부 정보를 표시합니다.

    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match

## 셸을 사용하여 IP 허용 목록 공급자 추가

IP 허용 목록 공급자를 추가하려면 다음 구문을 사용합니다.

    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

다음 예에서는 아래 옵션으로 "Contoso IP Allow List Provider"라는 IP 허용 목록 공급자을 만듭니다.

  - **공급자를 사용할 FQDN**   allow.contoso.com

  - **공급자에서 사용할 비트 마스크 코드**   127.0.0.1

<!-- end list -->

    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1


> [!NOTE]
> 새 IP 허용 목록 공급자를 추가한 경우 기본적으로 사용하도록 설정되고(<EM>Enabled</EM> 값이 <CODE>$true</CODE>), 우선 순위 값이 증분됩니다(첫 번째 항목의 <EM>Priority</EM> 값이 1).



자세한 내용은 [Add-IPBlockListProvider](https://technet.microsoft.com/ko-kr/library/bb124358\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 공급자를 올바르게 추가했는지 확인하려면 다음 명령을 실행하여 새 IP 허용 목록 공급자가 표시되는지 확인합니다.

```powershell
Get-IPAllowListProvider
```

## 셸을 사용하여 IP 허용 목록 공급자를 사용하거나 사용하지 않도록 설정

특정 IP 허용 목록 공급자를 사용하거나 사용하지 않도록 설정하려면 다음 구문을 사용합니다.

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>
```

다음 예에서는 Contoso IP Allow List Provider라는 공급자를 사용하지 않도록 설정합니다.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false
```

다음 예에서는 Contoso IP Allow List Provider라는 공급자를 사용하도록 설정합니다.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 공급자가 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled
```

## 셸을 사용하여 IP 허용 목록 공급자 구성

**Set-IPAllowListProvider** cmdlet에서 사용할 수 있는 구성 옵션은 **New-IPAllowListProvider** cmdlet의 구성 옵션과 동일합니다.

기존 IP 허용 목록 공급자를 구성하려면 다음 구문을 사용합니다.

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

예를 들어 Contoso IP Allow List Provider라는 공급자의 기존 상태 코드 목록에 IP 주소 상태 코드 127.0.0.1을 추가하려면 다음 명령을 실행합니다.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

자세한 내용은 [Set-IPBlockListProvider](https://technet.microsoft.com/ko-kr/library/bb124979\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 공급자를 올바르게 구성했는지 확인하려면 다음 명령을 실행하여 표시되는 값이 구성한 값인지 확인합니다.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List
```

## 셸을 사용하여 IP 허용 목록 공급자 테스트

IP 허용 목록 공급자를 테스트하려면 다음 구문을 사용합니다.

```powershell
Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>
```

다음 예에서는 IP 주소 192.168.1.1을 조회하여 Contoso IP Allow List Provider라는 공급자를 테스트합니다.

```powershell
Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1
```

## 셸을 사용하여 IP 허용 목록 공급자 제거

IP 허용 목록 공급자를 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-IPAllowListProvider <IPAllowListProviderIdentity>
```

다음 예에서는 Contoso IP Allow List Provider라는 IP 허용 목록 공급자를 제거합니다.

```powershell
Remove-IPAllowListProvider "Contoso IP Allow List Provider"
```

## 작동 여부는 어떻게 확인합니까?

IP 허용 목록 공급자를 올바르게 제거했는지 확인하려면 다음 명령을 실행하여 제거한 IP 허용 목록 공급자가 사라졌는지 확인합니다.

```powershell
Get-IPAllowListProvider
```


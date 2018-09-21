---
title: 'Edge 전송 서버의 주소 다시 쓰기 관리: Exchange 2013 Help'
TOCTitle: Edge 전송 서버의 주소 다시 쓰기 관리
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060545
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버의 주소 다시 쓰기 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

주소 다시 쓰기 및 주소 다시 쓰기 에이전트와 관련된 모든 관리 작업에 대해 Edge 전송 서버에서 Exchange 관리 셸을 사용할 수 있습니다. 주소 다시 쓰기에 대한 자세한 내용은 [주소 Edge 전송 서버에서 다시 쓰기](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)를 참조하세요.

단일 받는 사람, 특정 도메인/하위 도메인의 모든 받는 사람 또는 여러 하위 도메인의 모든 받는 사람에게 적용되는 주소 다시 쓰기 항목을 만들 수 있습니다. 주소 다시 쓰기는 아웃바운드 전용일 수도 있고 인바운드 및 아웃바운드(양방향)일 수도 있습니다. 주소 다시 쓰기 항목을 만들 때는 다음 사항에 유의하세요.

  - 생성되는 전자 메일 주소가 조직에서 고유한지 확인합니다.

  - 전자 메일 주소 값에는 리터럴 문자열만 지원됩니다.

  - 와일드카드 문자(\*)는 내부 주소, 즉 변경하려는 주소에만 지원됩니다. 와일드카드 문자 사용에 유효한 구문은 **\*.contoso.com**입니다. **\*contoso.com** 또는 **sales.\*.com**과 같은 값은 사용할 수 없습니다.

  - 와일드카드 문자를 사용할 때는 주소 다시 쓰기를 아웃바운드 전용으로 구성해야 합니다. 즉, *OutboundOnly* 매개 변수의 값을 `$true`로 설정해야 합니다.

  - *OutboundOnly* 매개 변수의 값을 `$true`로 설정하여 아웃바운드 전용 주소 다시 쓰기를 구성할 때는 해당되는 받는 사람에 대해 프록시 주소를 구성해야 합니다. 그러면 다시 쓴 주소로 보내는 메일을 올바르게 배달할 수 있습니다.

  - 기본적으로 주소 다시 쓰기는 단일 받는 사람 또는 특정 도메인/하위 도메인의 모든 받는 사람에 대해 양방향으로 수행됩니다. 즉, *OutboundOnly* 매개 변수의 값이 `$false`입니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "Edge 전송 서버" 섹션

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 주소 다시 쓰기를 구성할 때는 다음 사항에 주의하세요. 모든 변경 내용은 명령을 실행하면 즉시 적용됩니다. *WhatIf* 매개 변수를 포함하여 명령을 실행할 수 있습니다. *WhatIf* 매개 변수에 대한 자세한 내용은 [WhatIf, Confirm 및 ValidateOnly 스위치](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 주소 다시 쓰기를 사용하거나 사용하지 않도록 설정

주소 다시 쓰기를 완전히 사용하거나 사용하지 않도록 설정하려면 주소 다시 쓰기 에이전트를 사용하거나 사용하지 않도록 설정합니다. 기본적으로 Edge 전송 서버의 주소 다시 쓰기 에이전트는 사용하도록 설정됩니다.

주소 다시 쓰기를 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

주소 다시 쓰기를 사용하도록 설정하려면 다음 명령을 실행합니다.

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## 작동 여부는 어떻게 확인합니까?

주소 다시 쓰기가 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-TransportAgent
```

2.  주소 다시 쓰기 인바운드 에이전트 및 주소 다시 쓰기 아웃바운드 에이전트의 **Enabled** 속성 값이 구성한 값인지 확인합니다.

## 셸을 사용하여 주소 다시 쓰기 항목 확인

모든 주소 다시 쓰기 항목의 요약 목록을 보려면 다음 명령을 실행합니다.

```powershell
Get-AddressRewriteEntry
```

주소 다시 쓰기 항목의 세부 정보를 보려면 다음 구문을 사용합니다.

```powershell
Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List
```

다음 예에서는 주소 다시 쓰기 항목 Rewrite Contoso.com to Northwindtraders.com의 세부 정보가 표시됩니다.

```powershell
Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List
```

## 셸을 사용하여 주소 다시 쓰기 항목 만들기

## 단일 받는 사람의 전자 메일 주소 다시 쓰기

단일 받는 사람의 전자 메일 주소를 다시 쓰려면 다음 구문을 사용합니다.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

다음 예에서는 받는 사람 joe@contoso.com에 대해 Exchange 조직에서 보내고 받는 모든 메시지의 전자 메일 주소를 다시 씁니다. 아웃바운드 메시지는 support@nortwindtraders.com에서 보내는 것으로 표시되도록 다시 쓰고, support@northwindtraders.com으로 보내는 인바운드 메시지는 해당 받는 사람에게 배달되도록 joe@contoso.com으로 다시 씁니다. *OutboundOnly* 매개 변수의 기본값은 `$false`입니다.

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## 단일 도메인/하위 도메인의 받는 사람에 대해 전자 메일 주소 다시 쓰기

단일 도메인 또는 하위 도메인의 받는 사람에 대해 전자 메일 주소를 다시 쓰려면 다음 구문을 사용합니다.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

다음 예에서는 contoso.com 도메인의 받는 사람에 대해 Exchange 조직에서 보내고 받는 모든 메시지의 전자 메일 주소를 다시 씁니다. 아웃바운드 메시지는 fabrikam.com 도메인에서 보내는 것으로 표시되도록 다시 쓰고, fabrikam.com 전자 메일 주소로 보내는 인바운드 메시지는 해당 도메인의 받는 사람에게 배달되도록 contoso.com으로 다시 씁니다. *OutboundOnly* 매개 변수의 기본값은 `$false`입니다.

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

다음 예에서는 sales.contoso.com 하위 도메인의 받는 사람이 전송하는 Exchange 조직에서 보내는 모든 메시지의 전자 메일 주소를 다시 씁니다. 아웃바운드 메시지는 contoso.com 도메인에서 보내는 것으로 표시되도록 다시 쓰고, contoso.com 전자 메일 주소로 보내는 인바운드 메시지는 다시 쓰지 않습니다.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## 여러 하위 도메인의 받는 사람에 대해 전자 메일 주소 다시 쓰기

단일 도메인과 모든 하위 도메인의 받는 사람에 대해 전자 메일 주소를 다시 쓰려면 다음 구문을 사용합니다.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

다음 예에서는 contoso.com 도메인 및 모든 하위 도메인의 받는 사람이 전송하는 Exchange 조직에서 보내는 모든 메시지의 전자 메일 주소를 다시 씁니다. 아웃바운드 메시지는 contoso.com 도메인에서 보내는 것으로 표시되도록 다시 쓰고, *InternalAddress* 매개 변수에 와일드카드가 사용되므로 contoso.com 받는 사람에게 보내는 인바운드 메시지는 다시 쓸 수 없습니다.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

다음 예는 위의 예와 같지만 여기서는 legal.contoso.com 및 corp.contoso.com 하위 도메인의 받는 사람이 전송하는 메시지는 다시 쓰지 않습니다.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## 작동 여부는 어떻게 확인합니까?

주소 다시 쓰기 항목이 만들어졌는지 확인하려면 다음을 수행합니다.

1.  `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` 명령을 실행하고 표시되는 설정이 구성한 설정인지 확인합니다.

2.  주소 다시 쓰기 항목의 영향을 받는 사서함에서 외부 사서함으로 테스트 메시지를 보냅니다. 테스트 메시지가 다시 쓴 전자 메일 주소에서 보낸 것으로 표시되는지 확인합니다.

3.  외부 사서함에서 테스트 메시지에 회신을 보냅니다. 원래 사서함에 회신이 수신되었는지 확인합니다.

## 셸을 사용하여 주소 다시 쓰기 항목 수정

기존 주소 다시 쓰기 항목을 수정할 때 사용 가능한 구성 옵션은 새 주소 다시 쓰기 항목을 만들 때의 구성 옵션과 동일합니다.

## 단일 받는 사람에 대해 주소 다시 쓰기 항목 수정

단일 받는 사람의 전자 메일 주소를 다시 쓰는 주소 다시 쓰기 항목을 수정하려면 다음 구문을 사용합니다.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

다음 예에서는 "joe@contoso.com to support@nortwindtraders.com"라는 단일 받는 사람 주소 다시 쓰기 항목의 다음 속성을 수정합니다.

  - 외부 주소를 support@northwindtraders.net으로 변경합니다.

  - 주소 다시 쓰기 항목의 이름을 "joe@contoso.com to support@northwindtraders.net"으로 변경합니다.

  - *OutboundOnly*의 값을 `$true`로 변경합니다. 이렇게 변경하려면 Joe의 사서함에서 support@northwindtraders.net을 프록시 주소로 구성해야 합니다.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## 단일 도메인/하위 도메인의 받는 사람에 대해 주소 다시 쓰기 항목 수정

단일 도메인 또는 하위 도메인의 받는 사람 전자 메일 주소를 다시 쓰는 주소 다시 쓰기 항목을 수정하려면 다음 구문을 사용합니다.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

다음 예에서는 "Northwind Traders to Contoso"라는 단일 도메인 주소 다시 쓰기 항목의 내부 주소 값을 변경합니다.

```powershell
Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net
```

## 여러 하위 도메인의 받는 사람에 대해 주소 다시 쓰기 항목 수정

단일 도메인 및 모든 하위 도메인의 받는 사람 전자 메일 주소를 다시 쓰는 주소 다시 쓰기 항목을 수정하려면 다음 구문을 사용합니다.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

여러 하위 도메인 주소 다시 쓰기 항목의 기존 예외 목록 값을 바꾸려면 다음 구문을 사용합니다.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

다음 예에서는 Contoso to Northwind Traders라는 여러 하위 도메인 주소 다시 쓰기 항목의 기존 예외 목록을 marketing.contoso.com 및 legal.contoso.com 값으로 바꿉니다.

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

기존 예외 목록 값을 수정하지 않고 여러 하위 도메인 주소 다시 쓰기 항목의 예외 값 목록을 선택적으로 추가하거나 제거하려면 다음 구문을 사용합니다.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

다음 예에서는 Contoso to Northwind Traders라는 여러 하위 도메인 주소 다시 쓰기 항목의 예외 목록에 finance.contoso.com을 추가하고 marketing.contoso.com을 목록에서 제거합니다.

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## 작동 여부는 어떻게 확인합니까?

주소 다시 쓰기 항목이 수정되었는지 확인하려면 다음을 수행합니다.

1.  `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` 명령을 실행하고 표시되는 설정이 구성한 설정인지 확인합니다.

2.  주소 다시 쓰기 항목의 영향을 받는 사서함에서 외부 사서함으로 테스트 메시지를 보냅니다. 테스트 메시지가 다시 쓴 전자 메일 주소에서 보낸 것으로 표시되는지 확인합니다.

3.  외부 사서함에서 테스트 메시지에 회신을 보냅니다. 원래 사서함에 회신이 수신되었는지 확인합니다.

## 셸을 사용하여 주소 다시 쓰기 항목 제거

단일 주소 다시 쓰기 항목을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>
```

다음 예에서는 "Contoso.com to Northwindtraders.com" 주소 다시 쓰기 항목을 제거합니다.

```powershell
Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"
```

여러 주소 다시 쓰기 항목을 제거하려면 다음 구문을 사용합니다.

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

다음 예에서는 모든 주소 다시 쓰기 항목을 제거합니다.

```powershell
Get-AddressRewriteEntry | Remove-AddressRewriteEntry
```

다음 예에서는 이름에 "to contoso.com"이라는 텍스트가 포함된 주소 다시 쓰기 항목 제거를 시뮬레이트합니다. *WhatIf* 스위치를 사용하면 변경 내용을 커밋하지 않고 결과를 미리 볼 수 있습니다.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

원하는 결과가 표시되면 *WhatIf* 스위치를 사용하지 않고 명령을 다시 실행하여 주소 다시 쓰기 항목을 제거합니다.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## 작동 여부는 어떻게 확인합니까?

주소 다시 쓰기 항목이 제거되었는지 확인하려면 다음을 수행합니다.

1.  `Get-AddressRewriteEntry` 명령을 실행하여 제거한 주소 다시 쓰기 항목이 나열되지 않는지 확인합니다.

2.  주소 다시 쓰기 항목의 영향을 받는 사서함에서 외부 사서함으로 테스트 메시지를 보냅니다. 테스트 메시지가 제거된 주소 다시 쓰기 항목의 영향을 더 이상 받지 않는지 확인합니다.

3.  외부 사서함에서 테스트 메시지에 회신을 보냅니다. 원래 사서함이 회신을 받으며 메시지가 제거된 주소 다시 쓰기 항목의 영향을 받지 않는지 확인합니다.


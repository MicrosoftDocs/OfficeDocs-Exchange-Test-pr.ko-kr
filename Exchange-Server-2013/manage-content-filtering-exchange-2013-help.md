---
title: '콘텐츠 필터링 관리: Exchange 2013 Help'
TOCTitle: 콘텐츠 필터링 관리
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50482419
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 콘텐츠 필터링 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

콘텐츠 필터링은 콘텐츠 필터 에이전트에서 제공됩니다. 콘텐츠 필터 에이전트는 Exchange 서버의 모든 수신 커넥터를 통해 들어오는 메시지를 모두 필터링합니다. 인증되지 않은 원본에서 들어오는 메시지만 필터링됩니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 항목의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 콘텐츠 필터링을 사용하거나 사용하지 않도록 설정

콘텐츠 필터링을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -Enabled $false
```

콘텐츠 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -Enabled $true
```


> [!NOTE]
> 콘텐츠 필터링을 사용하지 않도록 설정해도 기본 콘텐츠 필터 에이전트는 여전히 사용됩니다. 콘텐츠 필터 에이전트를 사용하지 않도록 설정하려면 다음 명령을 실행합니다. <CODE>Disable-TransportAgent "Content Filter Agent"</CODE>.



## 작동 여부는 어떻게 확인합니까?

콘텐츠 필터링을 성공적으로 사용하거나 사용하지 않도록 설정했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

2.  표시된 *Enabled* 속성의 값을 확인합니다.

## 셸을 사용하여 외부 메시지에 대해 콘텐츠 필터링을 사용하거나 사용하지 않도록 설정

기본적으로 외부 메시지에는 콘텐츠 필터링 기능이 사용됩니다.

외부 메시지에 콘텐츠 필터링을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $false
```

외부 메시지에 콘텐츠 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $true
```

## 작동 여부는 어떻게 확인합니까?

외부 메시지에 콘텐츠 필터링을 성공적으로 사용하거나 사용하지 않도록 설정했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ContentFilterConfig | Format-List ExternalMailEnabled
```

2.  표시된 *ExternalMailEnabled* 속성의 값을 확인합니다.

## 셸을 사용하여 내부 메시지에 대해 콘텐츠 필터링을 사용하거나 사용하지 않도록 설정

신뢰할 수 있는 파트너나 조직 내부에서 오는 메시지는 필터링하지 않는 것이 가장 좋습니다. 스팸 방지 필터를 실행하면 언제나 메시지를 잘못 필터링할 가능성이 있습니다. 필터가 합법적인 전자 메일 메시지를 잘못 처리할 가능성을 줄이려면 잠재적으로 신뢰할 수 없거나 알 수 없는 원본의 메시지에 대해서만 실행되도록 스팸 방지 에이전트를 설정해야 합니다.

내부 메시지에 콘텐츠 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -InternalMailEnabled $true
```

내부 메시지에 콘텐츠 필터링을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -InternalMailEnabled $false
```

## 작동 여부는 어떻게 확인합니까?

내부 메시지에 콘텐츠 필터링을 성공적으로 사용하거나 사용하지 않도록 설정했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ContentFilterConfig | Format-List InternalMailEnabled
```

2.  표시된 *InternalMailEnabled* 속성의 값을 확인합니다.

## 셸을 사용하여 받는 사람과 보낸 사람 예외 구성

기존 값을 바꾸려면 다음 명령을 실행합니다.

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

이 예에서는 다음 콘텐츠 필터링 예외를 구성합니다.

  - 받는 사람 laura@contoso.com 및 julia@contoso.com은 콘텐츠 필터링으로 확인되지 않습니다.

  - 보낸 사람 steve@fabrikam.com 및 cindy@fabrikam.com은 콘텐츠 필터링으로 확인되지 않습니다.

  - 도메인 nwtraders.com과 모든 하위 도메인의 모든 보낸 사람은 콘텐츠 필터링으로 확인되지 않습니다.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

기존 값을 수정하지 않고 항목을 추가 또는 제거하려면 다음 명령을 실행합니다.

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

이 예에서는 다음 콘텐츠 필터링 예외를 구성합니다.

  - 콘텐츠 필터링으로 확인되지 않는 기존 받는 사람 목록에 tiffany@contoso.com 및 chris@contoso.com을 추가합니다.

  - 콘텐츠 필터링으로 확인되지 않는 기존 보낸 사람 목록에 joe@fabrikam.com 및 michelle@fabrikam.com을 추가합니다.

  - 보낸 사람이 콘텐츠 필터링으로 확인되지 않는 기존 도메인 목록에 blueyonderairlines.com을 추가합니다.

  - 보낸 사람이 콘텐츠 필터링으로 확인되지 않는 기존 도메인 목록에서 도메인 woodgrovebank.com과 모든 하위 도메인을 제거합니다.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## 작동 여부는 어떻게 확인합니까?

받는 사람 및 보낸 사람 예외를 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  표시된 값이 지정한 설정과 일치하는지 확인합니다.

## 셸을 사용하여 허용되고 차단되는 구 구성

허용되고 차단되는 단어와 구를 추가하려면 다음 명령을 실행합니다.

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

이 예에서는 "customer feedback"이라는 구가 포함된 메시지를 모두 허용합니다.

```powershell
Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"
```

이 예에서는 "stock tip"이라는 구가 포함된 메시지를 모두 차단합니다.

```powershell
Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"
```

허용되거나 차단되는 구를 제거하려면 다음 명령을 실행합니다.

```powershell
Remove-ContentFilterPhrase -Phrase <Phrase>
```

이 예에서는 "stock tip"이라는 구를 제거합니다.

```powershell
Remove-ContentFilterPhrase -Phrase "stock tip"
```

## 작동 여부는 어떻게 확인합니까?

허용되고 차단되는 구를 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ContentFilterPhrase | Format-List Influence,Phrase
```

2.  표시된 값이 지정한 설정과 일치하는지 확인합니다.

## 셸을 사용하여 SCL 임계값 구성

SCL(스팸 지수) 임계값과 작업을 구성하려면 다음 명령을 실행합니다.

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>


> [!NOTE]
> 삭제 작업은 거부 작업보다 우선 순위가 높고 거부 작업은 격리 작업보다 우선 순위가 높습니다. 따라서 삭제 작업의 SCL 임계값은 거부 작업의 SCL 임계값보다 커야 하고, 거부 작업의 SCL 임계값은 격리 작업의 SCL 임계값보다 커야 합니다. 거부 작업만 기본적으로 사용되고 해당 SCL 임계값은 7입니다.



이 예에서는 다음 SCL 임계값을 구성합니다.

  - 삭제 작업이 사용되고 해당 SCL 임계값은 9로 설정됩니다.

  - 거부 작업이 사용되고 해당 SCL 임계값은 8로 설정됩니다.

  - 격리 작업이 사용되고 해당 SCL 임계값은 7로 설정됩니다.

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 작동 여부는 어떻게 확인합니까?

SCL 임계값을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-ContentFilterConfig | Format-List SCL*

2.  표시된 값이 지정한 설정과 일치하는지 확인합니다.

## 셸을 사용하여 거부 응답 구성

거부 작업이 사용되는 경우 메시지 보낸 사람에게 전송되는 거부 응답을 사용자 지정할 수 있습니다. 거부 응답은 240자를 초과할 수 없습니다.

사용자 지정 거부 응답을 구성하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -RejectionResponse "<Custom Text>"
```

이 예에서는 사용자 지정된 거부 응답을 보내도록 콘텐츠 필터 에이전트를 구성합니다.

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## 작동 여부는 어떻게 확인합니까?

거부 응답을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  표시된 값이 지정한 설정과 일치하는지 확인합니다.

## 셸을 사용하여 Outlook 전자 메일 소인을 사용하거나 사용하지 않도록 설정

*Outlook 전자 메일 소인* 유효성 검사는 받는 사람 메시징 시스템이 합법적인 전자 메일과 정크 메일을 구별할 수 있도록 Microsoft Outlook이 보내는 메시지에 적용하는 전산 증명입니다. Outlook 2007 이상에서 소인을 사용할 수 있습니다. 소인을 사용하면 가양성을 줄일 수 있습니다. Outlook 전자 메일 소인은 기본적으로 사용됩니다.

Outlook 전자 메일 소인을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false
```

Outlook 전자 메일 소인을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true
```

## 작동 여부는 어떻게 확인합니까?

Outlook 전자 메일 소인을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled
```

2.  표시된 값이 지정한 설정과 일치하는지 확인합니다.


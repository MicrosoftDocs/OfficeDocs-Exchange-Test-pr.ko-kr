---
title: '사서함에 대해 스팸 방지 설정 구성: Exchange 2013 Help'
TOCTitle: 사서함에 대해 스팸 방지 설정 구성
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50483589
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대해 스팸 방지 설정 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-11-17_

개별 사서함에서 Exchange 조직의 나머지 사서함에 적용되는 스팸 방지 설정과는 다른 특정 스팸 방지 설정을 구성할 수 있습니다. 사서함에서 스팸 방지 설정을 구성하면 그 설정이 해당 조직 차원의 콘텐츠 필터링 또는 조직 구성 스팸 방지 설정을 재정의합니다.


> [!NOTE]
> 2016년 11월 1일, Microsoft가 Exchange 및 Outlook에서 SmartScreen 필터에 대한 스팸 정의 업데이트 생성을 중지했습니다. 기존 SmartScreen 스팸 정의는 제자리에 남게 되지만 시간 경과에 따라 효율성이 저하될 가능성이 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 및 Exchange에서 SmartScreen에 대한 지원 삭제</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 항목의 "스팸 방지 기능" 항목 및 [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "스팸 방지" 항목

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 정크 메일 폴더 SCL 임계값은 SCL 삭제, 거부 및 격리 값과는 다르게 작동합니다. 자세한 내용은 [스팸 지수 임계값](spam-confidence-level-threshold-exchange-2013-help.md) 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 단일 사서함에서 스팸 방지 기능 구성

단일 사서함에서 스팸 방지 설정을 구성하려면 다음 구문을 사용합니다.

```powershell
Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>
```

이 예에서는 모든 스팸 방지 필터를 무시하고 정크 메일 폴더 SCL 임계값 5를 충족하거나 초과하는 메시지를 Microsoft Outlook의 정크 메일 폴더로 배달하도록 Jeff Phillips라는 사용자의 사서함을 구성합니다.

```powershell
Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4
```

## 작동 여부는 어떻게 확인합니까?

단일 사서함에서 스팸 방지 기능을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*
    ```

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 여러 사서함에서 스팸 방지 기능 구성

여러 사서함에서 모든 스팸 방지 설정을 구성하려면 다음 구문을 사용합니다.

```powershell
Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>
```

이 예에서는 Contoso.com 도메인의 Users 컨테이너에 있는 모든 사서함에서 SCL 격리 임계값 7을 사용하도록 설정합니다.

```powershell
Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7
```

## 작동 여부는 어떻게 확인합니까?

여러 사서함에서 스팸 방지 기능을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*
    ```

2.  표시된 값이 구성한 값인지 확인합니다.

## 셸을 사용하여 조직의 모든 사서함에 대한 정크 메일 임계값 구성

다음 명령을 실행합니다.

```powershell
Set-OrganizationConfig -SCLJunkThreshold <Integer>
```

이 예에서는 조직의 정크 메일 임계값을 5로 설정합니다.

```powershell
Set-OrganizationConfig -SCLJunkThreshold 5
```

## 작동 여부는 어떻게 확인합니까?

조직의 모든 사서함에 대한 정크 메일 임계값을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-OrganizationConfig | Format-List SCLJunkThreshold
    ```

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.


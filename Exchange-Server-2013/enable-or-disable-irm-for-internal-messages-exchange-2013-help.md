---
title: '내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50483887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-12_

Microsoft Exchange Server 2013에서는 기본적으로 내부 메시지에 IRM(정보 권한 관리)을 사용할 수 있도록 설정되어 있습니다. 이 설정을 사용하여 전송 보호 규칙과 Microsoft Outlook 보호 규칙을 만들어 전송되는 메시지와 Microsoft Outlook 2010 이후 클라이언트의 메시지를 IRM으로 보호할 수 있습니다. 전송 암호 해독, 저널 규칙 암호 해독, Microsoft Exchange Server 2013 Office의 IRM, Microsoft Outlook Web App의 IRM과 같은 Exchange ActiveSync의 기타 모든 IRM 기능을 사용하려면 내부 메시지에 IRM을 사용하도록 설정해야 합니다.


> [!WARNING]
> 내부 메시지에 IRM을 사용하지 않도록 설정하면 Exchange 조직의 모든 IRM 기능이 비활성화됩니다. AD&nbsp;RMS(Outlook Rights Management Services) 서버를 이용한 IRM으로 보호된 메시지 읽기, 회신, 전달, 생성과 같은 Active Directory의 클라이언트 쪽 IRM 기능은 영향을 받지 않습니다.



IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - EAC(Exchange 관리 센터)를 사용하여 내부 메시지에 IRM을 사용하거나 사용하지 않도록 설정할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 내부 메시지에 IRM을 사용하도록 설정

이 예에서는 Exchange 조직의 내부 메시지에 IRM을 사용하도록 설정합니다.

```powershell
Set-IRMConfiguration -InternalLicensingEnabled $true
```

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 내부 메시지에 IRM을 사용하지 않도록 설정

이 예에서는 Exchange 조직의 내부 메시지에 IRM을 사용하지 않도록 설정합니다.

```powershell
Set-IRMConfiguration -InternalLicensingEnabled $false
```

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) 항목을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

내부 메시지에 IRM을 사용하거나 사용하지 않도록 설정했는지 확인하려면 [Get-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd776120\(v=exchg.150\)) cmdlet을 사용하여 구성을 확인합니다.


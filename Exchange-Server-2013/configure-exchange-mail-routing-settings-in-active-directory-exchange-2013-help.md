---
title: 'Active Directory의 Exchange 메일 라우팅 설정 구성: Exchange 2013 Help'
TOCTitle: Active Directory의 Exchange 메일 라우팅 설정 구성
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50484241
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory의 Exchange 메일 라우팅 설정 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

기본적으로 Microsoft Exchange Server 2013은 Active Directory의 IP 사이트 링크 개체를 참조하여 최저 비용 라우팅 경로를 결정합니다. 그러나 Active Directory 사이트 링크 비용과 트래픽 흐름 패턴이 Exchange의 메일 라우팅에 대해 최적화되어 있지 않다고 판단되면 Exchange에서만 사용되는 Active Directory의 설정을 구성하여 메일 흐름을 최적화할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "Active Directory 사이트 및 사이트 링크 관리" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 Active Directory IP 사이트 링크에 대한 Exchange 관련 비용 구성

Exchange 비용을 설정할 Active Directory IP 사이트 링크의 이름을 확인합니다. 비용이 낮을수록 더 적절한 경로를 나타냅니다. 라우팅 테이블 로그 내용과 **ADTopologyPath ID** 섹션의 데이터를 검토하여 두 Active Directory 사이트 간에 계산된 최소 비용 라우팅 경로에 대한 자세한 정보를 확인할 수 있습니다.

Active Directory 사이트 링크에 Exchange 관련 비용을 설정하려면 다음 명령을 실행합니다.

```powershell 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

이 예에서는 IPSiteLinkAB라는 IP 사이트 링크에 Exchange 관련 비용 10을 설정합니다.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10
```

이 예에서는 IPSiteLinkAB라는 IP 사이트 링크에서 Exchange 비용을 지웁니다.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null
```

## 작동 여부는 어떻게 확인합니까?

Active Directory 사이트 링크에 Exchange 비용이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-AdSiteLink | Format-List Name,ExchangeCost
    ```

2.  Active Directory 사이트 링크에 Exchange 비용이 구성되어 있는지 확인합니다.

## 셸을 사용하여 Active Directory 사이트를 허브 사이트로 구성

허브 사이트가 메시지에 대한 최저 비용 라우팅 경로상에 있을 경우 해당 메시지는 허브 사이트를 통해 라우팅되어야 합니다. 라우팅 테이블 로그 내용과 **ADTopologyPath ID** 섹션의 데이터를 검토하여 선택한 사이트가 두 Active Directory 사이트 간의 최소 비용 라우팅 경로상에 있는지 확인합니다. 그렇지 않은 경우 Exchange 관련 비용을 IP 사이트 링크에 할당하여 최소 비용 라우팅 경로가 선택한 사이트를 거치도록 해야 합니다.

Active Directory 사이트를 허브 사이트로 구성하려면 다음 명령을 실행합니다.

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

이 예에서는 Site A라는 Active Directory 사이트를 허브 사이트로 구성합니다.

```powershell
Set-AdSite "Site A" -HubSiteEnabled $true
```

이 예에서는 Site B라는 Active Directory 사이트에서 허브 사이트 특성을 제거합니다.

```powershell
Set-AdSite "Site B" -HubSiteEnabled $false
```

## 작동 여부는 어떻게 확인합니까?

Active Directory 사이트가 허브 사이트로 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-AdSite | Format-List Name,HubSiteEnabled
    ```

2.  Active Directory 사이트의 *HubSiteEnabled* 값이 `True`인지 확인합니다.


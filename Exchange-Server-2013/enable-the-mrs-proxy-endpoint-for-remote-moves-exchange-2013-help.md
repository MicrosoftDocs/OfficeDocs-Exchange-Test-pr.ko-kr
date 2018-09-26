---
title: '원격 이동에 대 한 MRS 프록시 끝점을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 원격 이동에 대 한 MRS 프록시 끝점을 사용 하도록 설정
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54651832
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원격 이동에 대 한 MRS 프록시 끝점을 사용 하도록 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-07-02_

MRS 프록시(사서함 복제 서비스 프록시)를 통해 온-프레미스 Exchange 조직과 Exchange Online 간 포리스트 간 사서함 이동 및 원격 이동 마이그레이션을 보다 쉽게 수행할 수 있습니다. Exchange 2013에서 MRS 프록시는 사서함 서버 역할(*사서함 서버*라고도 함)에 포함됩니다. 포리스트 간 및 원격 이동 마이그레이션 동안 클라이언트 액세스 서버는 사서함 서버의 들어오는 이동 요청에 대해 프록시 역할을 합니다. 클라이언트 액세스 서버에서 이러한 요청을 수락하는 기능은 기본적으로 사용하지 않도록 설정되어 있습니다. 클라이언트 액세스 서버에서 들어오는 이동 요청을 수락하도록 하려면 MRS 프록시 끝점을 사용하도록 설정해야 합니다.

MRS 프록시 끝점을 사용하도록 설정할 클라이언트 액세스 서버는 사서함 이동의 방향 및 유형에 따라 달라집니다.

  - **포리스트 간 엔터프라이즈 이동**   대상 환경에서 시작된 포리스트 간 이동(*끌어오기* 이동 유형이라고 함)의 경우 원본 환경의 클라이언트 액세스 서버에서 MRS 프록시 끝점을 사용하도록 설정해야 합니다. 반면 원본 환경에서 시작된 포리스트 간 이동(*밀어넣기* 이동 유형이라고 함)의 경우 대상 환경의 클라이언트 액세스 서버에서 MRS 프록시 끝점을 사용하도록 설정해야 합니다.

  - **온-프레미스 Exchange 조직과 Exchange Online 간 원격 이동 마이그레이션**   온보딩 및 오프보딩 원격 이동 마이그레이션 둘 다의 경우 온-프레미스 조직의 클라이언트 액세스 서버에서 MRS 프록시 끝점을 사용하도록 설정해야 합니다.


> [!NOTE]
> EAC를 사용하여 사서함을 이동할 경우 요청이 대상 환경에서 시작되므로 포리스트 간 이동 및 온보딩 원격 이동 마이그레이션은 끌어오기 이동 유형이 됩니다. 반면 오프보딩 원격 이동 마이그레이션은 요청이 원본 환경에서 시작되므로 밀어넣기 이동 유형이 됩니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 서버당 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Exchange 웹 서비스 권한" 섹션

  - Exchange 조직에 둘 이상의 클라이언트 액세스 서버를 배포한 경우 각 서버에서 MRS 프록시 끝점을 사용하도록 설정해야 합니다. 클라이언트 액세스 서버를 추가할 경우 새 서버에서도 MRS 프록시 끝점을 사용하도록 설정해야 합니다. 일부 클라이언트 액세스 서버에서 MRS 프록시 끝점이 사용하도록 설정되지 않은 경우 포리스트 간 이동 및 원격 이동 마이그레이션이 실패할 수 있습니다.

  - 포리스트 간 이동이나 원격 이동 마이그레이션을 수행하지 않을 경우에는 MRS 프록시 끝점을 사용하지 않도록 설정하여 조직의 공격 영역을 줄이십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 MRS 프록시 끝점을 사용하도록 설정

1.  EAC에서 **받는 사람** \> **서버** \> **가상 디렉터리**로 이동합니다.

2.  **서버 선택** 드롭다운 목록에서 MRS 프록시 끝점을 사용하도록 설정할 클라이언트 액세스 서버의 이름을 선택합니다. 또는 **모든 서버**를 선택하여 조직의 모든 클라이언트 액세스 서버의 가상 디렉터리를 표시합니다.

3.  **유형 선택** 드롭다운 목록에서 **EWS**를 선택하여 선택한 서버의 EWS(Exchange 웹 서비스) 가상 디렉터리를 표시합니다.

4.  가상 디렉터리 목록에서 구성할 클라이언트 액세스 서버의 <strong>EWS(기본 웹 사이트)</strong>를 클릭한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

5.  **EWS (기본 웹사이트)** 속성 페이지에서 **사용 하도록 설정 MRS 프록시 끝점** 확인란을 선택 하 고 **저장** 을 클릭 합니다.

## 셸을 사용하여 MRS 프록시 끝점을 사용하도록 설정

다음 명령은 EXCH-SRV-01이라는 클라이언트 액세스 서버에서 MRS 프록시 끝점을 사용하도록 설정합니다.

  ```powershell
  Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true
  ```

다음 명령은 Exchange 조직의 모든 클라이언트 액세스 서버에서 MRS 프록시 끝점을 사용하도록 설정합니다.

```powershell
Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true
```


> [!IMPORTANT]
> 앞서 언급했듯이 MRS 프록시 끝점은 조직의 각 클라이언트 액세스 서버에서 사용하도록 설정해야 합니다. 새 클라이언트 액세스 서버가 조직에 추가되면 앞에 나온 명령을 실행합니다.



## 작동 여부는 어떻게 확인합니까?

MRS 프록시 끝점이 사용하도록 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

1.  EAC에서 **받는 사람** \> **서버** \> **가상 디렉터리**로 이동합니다.

2.  가상 디렉터리 목록에서 <strong>EWS(기본 웹 사이트)</strong>를 클릭하고 MRS 프록시 끝점이 사용하도록 설정되었는지 세부 정보 창에서 확인합니다.
    
    또는 **EWS (기본 웹사이트)** 속성 페이지를 보려면 하 고 **MRS 프록시를 사용 하도록 설정 끝점** 확인란이 선택 되었는지 확인 하 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘") 클릭 수 있습니다.

또는

셸에서 다음 명령을 실행합니다.

```powershell
Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled
```

*MRSProxyEnabled* 매개 변수가 `True`로 설정되었는지 확인합니다.

MRS 프록시 끝점이 사용하도록 설정되었는지 확인할 수 있는 또 다른 방법은 **Test-MigrationServerAvailability** cmdlet을 사용하여 이동할 사서함을 호스트하는 원격 서버와 통신하는 기능을 테스트하거나 온-프레미스 조직에 대한 오프보딩 Exchange Online 사서함의 경우 온-프레미스 조직의 서버와 통신하는 기능을 테스트하는 것입니다. 자세한 내용은 [Test-MigrationServerAvailability](https://technet.microsoft.com/ko-kr/library/jj219169\(v=exchg.150\))를 참조하십시오.

다음 예에서는 corp.contoso.com 포리스트에서 서버와의 연결을 테스트합니다.

```powershell
$Credentials = Get-Credential
```

```powershell
Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials
```

이 명령을 실행하려면 MRS 프록시 끝점이 사용하도록 설정되어야 합니다.


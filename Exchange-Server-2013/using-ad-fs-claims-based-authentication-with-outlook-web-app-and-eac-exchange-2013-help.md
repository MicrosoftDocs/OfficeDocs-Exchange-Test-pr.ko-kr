---
title: 'Outlook Web App 및 EAC에서 AD FS 클레임 기반 인증 사용: Exchange 2013 Help'
TOCTitle: Outlook Web App 및 EAC에서 AD FS 클레임 기반 인증 사용
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61203323
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 및 EAC에서 AD FS 클레임 기반 인증 사용

 

_**적용 대상:** Exchange Server 2013 SP1_

_**마지막으로 수정된 항목:** 2017-04-14_

**요약**:

온-프레미스 Exchange 2013 서비스 팩 1 (SP1) 배포에 대 한 설치 및 구성 Active Directory Federation Services (AD FS) 의미 Outlook Web App 및 EAC에 연결할 이제 AD FS 클레임 기반 인증을 사용할 수 있습니다. Exchange 2013 s p 1으로 AD FS 및 클레임 기반 인증을 통합할 수 있습니다. 클레임 기반 인증을 사용 하 여 다음을 비롯 한 전통적인 인증 방법 대체 합니다.

  - Windows 인증

  - 폼 인증

  - 다이제스트 인증

  - 기본 인증

  - Active Directory 클라이언트 인증서 인증

인증은 사용자의 ID를 확인하는 프로세스로, 사용자가 본인이 맞는지 유효성을 검사합니다. 또 다른 인증 방식으로 클레임 기반 ID가 있습니다. 클레임 기반 인증에서는 응용 프로그램(이 경우에는 Outlook Web App 및 EAC)에서 인증을 관리하지 않고 중앙에서 관리하므로 계정을 보다 쉽게 관리할 수 있습니다. Outlook Web App 및 EAC는 사용자 인증, 사용자 계정 및 암호 저장, 사용자 ID 세부 정보 조회 또는 다른 ID 시스템과의 통합을 수행하지 않습니다. 이처럼 인증을 중앙에서 관리하면 나중에 원하는 인증 방법으로 쉽게 업그레이드할 수 있습니다.


> [!NOTE]
> 장치용 OWA에서는 AD FS 클레임 기반 인증을 지원하지 않습니다.



다음 표에 요약 된 대로는 여러 버전을 사용할 수 있는 AD FS입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Server 버전</th>
<th>설치</th>
<th>AD FS 버전</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p>추가 기능 Windows 구성 요소인 AD FS 2.0을 <strong>다운로드 및 설치</strong>합니다.</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p><strong>기본 제공</strong> AD FS 서버 역할을 설치합니다.</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p><strong>기본 제공</strong> AD FS 서버 역할을 설치합니다.</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


여기서 수행하는 작업은 AD FS 역할 서비스가 포함된 Windows Server 2012 R2를 기준으로 합니다.

**필수 단계 개요**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

3 단계-Outlook Web App 및 EAC에 대 한 신뢰 당사자 트러스트 및 사용자 지정 클레임 규칙 만들기

4 단계-웹 응용 프로그램 프록시 역할 서비스 (선택 사항)를 설치 합니다.

5 단계-웹 응용 프로그램 프록시 역할 서비스 (선택 사항) 구성

6 단계-Outlook Web App 및 (선택 사항) 웹 응용 프로그램 프록시를 사용 하 여 EAC를 게시 합니다.

7 단계-AD FS 인증을 사용 하 여 Exchange 2013 구성

단계 8-OWA 및 ECP 가상 디렉터리에서 인증을 사용 하도록 설정 AD FS

단계 9-다시 시작 또는 재활용 인터넷 정보 서비스 (IIS)

단계-Outlook Web App 및 EAC에 대해 AD FS 클레임을 테스트 합니다.

Additional information you might want to know

## 시작하기 전에 알아두어야 할 사항

  - 최소한 개별 Windows Server 2012 R2 서버를 설치해야 합니다. 서버 중 하나는 AD DS(Active Directory 도메인 서비스), Exchange 2013 서버, 웹 응용 프로그램 프록시 서버 및 AD FS(Active Directory Federation Services) 서버를 사용하는 도메인 컨트롤러로 설치합니다. 모든 업데이트가 설치되어 있는지 확인합니다.

  - 조직에서 적절한 수의 Windows Server 2012 R2 서버에 AD DS를 설치합니다. **Server Manager** \> **대시보드**의 **알림**을 사용하여 **이 서버를 도메인 컨트롤러로 승격**할 수도 있습니다.

  - 조직에 적합한 수의 클라이언트 액세스 서버 및 사서함 서버를 설치합니다. 조직의 모든 Exchange 2013 서버에 SP1을 포함한 모든 업데이트가 설치되어 있는지 확인합니다. SP1을 다운로드하려면 [Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)를 참조하세요.

  - 서버에서 웹 응용 프로그램 프록시를 배포하려면 로컬 관리자 권한이 필요합니다. 조직에서 Windows Server 2012 R2를 실행 중인 서버에 AD FS를 배포해야 웹 응용 프로그램 프록시를 배포할 수 있습니다.

  - Windows Server 2012 R2에서 AD FS 역할을 설치 및 구성하고 신뢰 당사자 트러스트 및 클레임 규칙을 만듭니다. 이 작업을 수행하려면 Domain Admins, Enterprise Admins 또는 로컬 Administrators 그룹 구성원인 사용자 계정으로 로그인해야 합니다.

  - [기능 사용 권한](feature-permissions-exchange-2013-help.md)을 확인하여 Exchange 2013에 필요한 사용 권한을 결정합니다.

  - Outlook Web App을 관리하는 데 필요한 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "Outlook Web App 사용 권한" 항목을 참조하세요.

  - EAC를 관리하는 데 필요한 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 "Exchange 관리 센터 연결" 항목을 참조하세요.

  - 일부 절차를 수행하려면 셸만 사용해야 할 수 있습니다. 온-프레미스 Exchange 조직에서 셸을 여는 방법을 확인하려면 [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 1단계 - AD FS의 인증서 요구 사항 검토

인증서는 Exchange 2013 SP1 서버, Outlook Web App 등의 웹 클라이언트와 EAC, Windows Server 2012 R2 서버(AD FS(Active Directory Federation Services) 서버 및 웹 응용 프로그램 프록시 서버 포함) 간의 통신을 보호하는 데 핵심적인 역할을 합니다. 인증서의 요구 사항은 설정 중인 항목(AD FS 서버, AD FS 프록시 또는 웹 응용 프로그램 프록시 서버)에 따라 달라집니다. \`SSL 및 토큰 서명 인증서를 비롯하여 AD FS 서비스에 사용되는 인증서는 모든 Exchange, AD FS 및 웹 응용 프로그램 프록시 서버의 신뢰 루트 인증 기관 저장소로 가져와야 합니다. 가져오는 인증서의 지문은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) cmdlet을 사용할 때 Exchange 2013 SP1 서버에서도 사용됩니다.

모든 AD FS 디자인, 다양 한 인증서를 사용 하 여 인터넷 및 AD FS 서버에 있는 사용자 간의 통신을 보호 수 있어야 합니다. 서비스 통신 인증서 또는 Secure Socket Layer (SSL) 인증서와 AD FS 서버, Active Directory 도메인 컨트롤러 하기 전에 토큰 서명 인증서를 각 페더레이션 서버 있어야 하 고 Exchange 2013 서버가 통신할 수 및 인증 합니다. 보안 및 예산 요구 사항에 따라 신중 하 게 하는 인증서의 됩니다을 통해 가져올 수는 공용 CA 또는 엔터프라이즈 CA 고려 합니다. 엔터프라이즈 루트 또는 하위 CA를 설치 및 구성 하려는 경우에 Active Directory (AD CS) 인증서 서비스를 사용할 수 있습니다. AD CS에 대해 자세히 알고 하려는 경우 [Active Directory 인증서 서비스 개요](https://go.microsoft.com/fwlink/?linkid=392697)를 참조 하십시오.

AD FS에서는 CA가 인증서를 발급하지 않아도 되지만 SSL 인증서, 즉 기본적으로 서비스 통신 인증서로도 사용되는 SSL 인증서를 AD FS 클라이언트가 신뢰해야 합니다. 자체 서명 인증서는 사용하지 않는 것이 좋습니다. 페더레이션 서버는 SSL 인증서를 사용하여 웹 클라이언트 및 페더레이션 서버 프록시와의 SSL 통신에 대한 웹 서비스 트래픽을 보호합니다. 클라이언트 컴퓨터에서 SSL 인증서를 신뢰해야 하므로 신뢰할 수 있는 CA에서 서명한 인증서를 사용하는 것이 좋습니다. 선택하는 모든 인증서에는 해당 개인 키가 있어야 합니다. 엔터프라이즈 또는 공용 CA에서 인증서를 받은 후에는 모든 서버의 신뢰 루트 인증 기관 저장소로 인증서를 가져왔는지 확인하세요. **Certificates** MMC 스냅인을 사용하여 인증서를 저장소로 가져오거나 Active Directory 인증서 서비스를 사용하여 인증서를 배포할 수 있습니다. 가져온 인증서가 만료되면 다른 유효한 인증서를 수동으로 가져옵니다.


> [!IMPORTANT]
> AD FS의 자체 서명된 토큰 서명 인증서를 사용하는 경우에는 모든 Exchange 2013 서버의 신뢰 루트 인증 기관 저장소로 이 인증서를 가져와야 합니다. 자체 서명된 토큰 서명 인증서를 사용하지 않고 웹 응용 프로그램 프록시를 배포하는 경우에는 웹 응용 프로그램 프록시 구성과 모든 AD FS 신뢰 당사자 트러스트에서 공개 키를 업데이트해야 합니다.



Exchange 2013 SP1, AD FS 및 웹 응용 프로그램 프록시를 설정할 때는 다음의 인증서 관련 권장 사항을 따르세요.

  - **사서함 서버**   사서함 서버에서 사용되는 인증서는 Exchange 2013 설치 시 자체 서명된 인증서입니다. 모든 클라이언트는 Exchange 2013 클라이언트 액세스 서버를 통해 Exchange 2013 사서함 서버에 연결하므로 클라이언트 액세스 서버의 인증서만 관리하면 됩니다.

  - **클라이언트 액세스 서버**   서비스 통신에 사용되는 SSL 인증서가 필요합니다. 신뢰 당사자 트러스트 끝점을 설정하는 데 사용하는 FQDN이 기존 SSL 인증서에 이미 포함되어 있으면 추가 인증서는 필요하지 않습니다.

  - **AD FS**   AD FS에는 두 가지 유형의 인증서가 필요합니다.
    
      - 서비스 통신에 사용되는 SSL 인증서
        
          - 주체 이름: **adfs.contoso.com**(AD FS 배포 이름)
        
          - SAN(주체 대체 이름): 없음
    
      - 토큰 서명 인증서
        
          - 주체 이름: **tokensigning.contoso.com**
        
          - SAN(주체 대체 이름): 없음
        

        > [!NOTE]
        > AD FS에서 토큰 서명 인증서를 바꿀 때는 새 토큰 서명 인증서를 사용하도록 기존 신뢰 당사자 트러스트를 업데이트해야 합니다.



  - **웹 응용 프로그램 프록시**
    
      - 서비스 통신에 사용되는 SSL 인증서
        
          - 주체 이름: **owa.contoso.com**
        
          - SAN(주체 대체 이름): 없음
        

        > [!NOTE]
        > 웹 응용 프로그램 프록시 외부 URL이 내부 URL과 같으면 Exchange의 SSL 인증서를 여기서 다시 사용할 수 있습니다.

    
      - AD FS 프록시 SSL 인증서
        
          - 주체 이름: **adfs.contoso.com**(AD FS 배포 이름)
        
          - SAN(주체 대체 이름): 없음
    
      - 토큰 서명 인증서 - 아래 단계의 일부분으로 AD FS에서 자동으로 복사됩니다. 이 인증서를 사용하는 경우 조직의 Exchange 2013 서버에서 인증서를 신뢰해야 합니다.

인증서에 대 한 자세한 내용은 [AD FS를 배포 하기 위한 요구 사항 검토](https://go.microsoft.com/fwlink/?linkid=392699) 의 인증서 요구 사항 섹션을 참조 하십시오.


> [!NOTE]
> AD FS용 SSL 인증서가 있어도 Outlook Web App 및 EAC에는 SSL 암호화 인증서가 계속 필요합니다. SSL 인증서는 OWA 및 ECP 가상 디렉터리에서 사용됩니다.



## 2단계 - AD FS(Active Directory Federation Services) 설치 및 구성

Windows Server 2012 R2의 AD FS에서는 간소화된 보안 ID 페더레이션 및 웹 SSO(Single Sign-On) 기능이 제공됩니다. AD FS에는 브라우저 기반 웹 SSO, 다단계 및 클레임 기반 인증을 사용할 수 있도록 하는 페더레이션 서비스가 포함되어 있습니다. AD FS는 클레임 기반 인증 및 액세스 권한 부여 메커니즘을 사용하여 응용 프로그램 보안을 유지함으로써 시스템과 응용 프로그램 액세스를 간소화합니다.

Windows Server 2012 R2에서 AD FS를 설치하려면 다음을 수행합니다.

1.  바탕 화면 작업 표시줄의 **Server Manager** 또는 **시작** 화면에서 **Server Manager**를 엽니다. **관리** 메뉴에서 **역할 및 기능 추가**를 클릭합니다.

2.  **시작하기 전에** 페이지에서 **다음**을 클릭합니다.

3.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 후 **다음**을 클릭합니다.

4.  **대상 서버 선택** 페이지의 **서버 풀에서 서버 선택**을 클릭하고 로컬 컴퓨터가 선택되어 있는지 확인한 후에 **다음**을 클릭합니다.

5.  **서버 역할 선택** 페이지에서 **Active Directory Federation Services**를 클릭하고 **다음**을 클릭합니다.
    
    **기능 선택** 페이지에서 **다음**을 클릭합니다. 필요한 필수 구성 요소 또는 기능은 미리 선택되어 있습니다. 다른 기능은 선택할 필요가 없습니다.

6.  **AD FS(Active Directory Federation Service)** 페이지에서 **다음**을 클릭합니다.

7.  **설치 선택 확인** 페이지에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 선택한 후 **설치**를 클릭합니다.
    

    > [!NOTE]
    > 설치 프로세스 중에 마법사를 닫지 마세요.



필요한 AD FS 서버를 설치 하 고 필요한 인증서를 생성 한 후에 AD FS를 구성 하 고 AD FS 제대로 작동 하는지 테스트 해야 합니다. 설정 하 고 AD FS를 구성 하는데 도움이 되는 검사 목록을 여기 사용할 수도 있습니다: [검사 목록: 페더레이션 서버 설정](https://go.microsoft.com/fwlink/?linkid=392700)합니다.

Active Directory Federation Services를 구성하려면 다음을 수행합니다.

1.  **설치 진행률** 페이지의 **Active Directory Federation Services** 아래 창에서 **이 서버에 페더레이션 서비스를 구성**을 클릭합니다. Active Directory Federation Service 구성 마법사가 열립니다.

2.  **시작** 페이지에서 <strong>페더레이션 서버 팜에 첫 번째 페더레이션 서버를 만듭니다.</strong>를 클릭하고 **다음**을 클릭합니다.

3.  **AD DS에 연결** 페이지에서 이 컴퓨터가 구독된 올바른 Active Directory 도메인에 대한 도메인 관리자 권한이 있는 계정을 지정하고 **다음**을 클릭합니다. 다른 사용자를 선택하려면 **변경**을 클릭합니다.

4.  **서비스 속성 지정** 페이지에서 다음 작업을 수행하고 **다음**을 클릭합니다.
    
      - AD CS 또는 공용 CA에서 이전에 가져온 SSL 인증서를 가져옵니다. 이 인증서에 필요한 서비스 인증 인증서가입니다. SSL 인증서의 위치를 이동 합니다. 만들기 (영문) 및 SSL 인증서 가져오기 (영문)에 대 한 자세한 내용은, [서버 인증서](https://go.microsoft.com/fwlink/?linkid=392703)를 참조 하십시오.
    
      - 페더레이션 서비스의 이름을 **adfs.contoso.com**과 같이 입력합니다.
    
      - 페더레이션 서비스의 표시 이름을 지정하려면 **Contoso, Ltd.** 와 같이 조직 이름을 입력합니다.

5.  **서비스 계정 지정** 페이지에서 **기존 도메인 사용자 계정 또는 그룹 관리 서비스 계정 사용**을 선택하고 도메인 컨트롤러를 만들 때 만든 GMSA 계정(FsGmsa)을 지정합니다. 계정 암호를 입력하고 **다음**을 클릭합니다.
    

    > [!NOTE]
    > GMSA(전역 관리 서비스 계정)는 도메인 컨트롤러를 구성할 때 만들어야 하는 계정입니다. AD FS 설치 및 구성 중에는 GMSA 계정이 필요합니다. 이 계정을 아직 만들지 않았으면 다음 Windows PowerShell 명령을 실행합니다. 이 명령은 contoso.com 도메인 및 AD FS 서버에 대해 계정을 만듭니다.



6.  다음 명령을 실행합니다.
    
    ```powershell
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    ```

7.  이 예제에서는 adfs.contoso.com과 같이 명명 된 페더레이션 서비스에 대 한 FsGmsa 라는 새 GMSA 계정을 만듭니다. 페더레이션 서비스 이름에는 클라이언트에 게 표시 되는 값입니다.
    
    ```powershell
    New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com
    ```

8.  **구성 데이터베이스 지정** 페이지에서 <strong>Windows 내부 데이터베이스를 사용하여 이 서버에 데이터베이스를 만듭니다.</strong>를 선택하고 **다음**을 클릭합니다.

9.  **옵션 검토** 페이지에서 구성 선택을 확인합니다. 원하는 경우 **스크립트 보기** 단추를 사용하여 추가 AD FS 설치를 자동화할 수 있습니다. **다음**을 클릭합니다.

10. **필수 구성 요소 확인** 페이지에서 모든 필수 구성 요소 확인이 정상적으로 완료되었는지 확인하고 **구성**을 클릭합니다.

11. **설치 진행률** 페이지에서 모든 항목이 정상적으로 설치되었는지 확인하고 **닫기**를 클릭합니다.

12. **결과** 페이지에서 결과를 검토하여 구성이 정상적으로 완료되었는지 확인한 후에 **페더레이션 서비스 배포를 완료하는 데 필요한 다음 단계**를 클릭합니다.

다음 Windows PowerShell 명령을 앞의 단계와 동일한 작업을 수행 합니다.

```powershell
Import-Module ADFS
```

```powershell
Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

자세한 내용 및 구문에 대 한 [설치 AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704)을 참조 하십시오.

설치를 확인하려면 AD FS 서버에서 웹 브라우저를 열고 페더레이션 메타데이터의 URL(예: **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**)로 이동합니다.

## 3 단계-Outlook Web App 및 EAC에 대 한 신뢰 당사자 트러스트 및 사용자 지정 클레임 규칙 만들기

모든 응용 프로그램 및 웹 응용 프로그램 프록시를 통해 게시 하려는 서비스에 대 한 AD FS 서버에서 신뢰 당사자 트러스트를 구성 해야 합니다. 별도 네임 스페이스를 사용 하는 여러 Active Directory 사이트 배포의 경우, 각 네임 스페이스에 대 한 신뢰 당사자 트러스트 Outlook Web App 및 EAC에 대 한 추가 되어야 합니다.

EAC는 ECP 가상 디렉터리를 사용합니다. [Get-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd351058\(v=exchg.150\)) 및 [Set-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd297991\(v=exchg.150\)) cmdlet을 사용하여 EAC에 대한 설정을 확인하거나 구성할 수 있습니다. EAC에 액세스하려면 웹 브라우저를 통해 <strong>http://server1.contoso.com/ecp</strong>로 이동해야 합니다.


> [!NOTE]
> 아래에 표시 된 URL 예에서 후행 슬래시 <STRONG>/</STRONG> 를 포함 하는 의도적인 것입니다. AD FS의 신뢰 당사자 트러스트와 Exchange 사용자를 대상 URI <STRONG>동일</STRONG>확인을 고려해 야 합니다. 즉, 신뢰 당사자 트러스트 AD FS와 Exchange 사용자를 대상 URI가 <STRONG>모두</STRONG> 해야 또는 사이트의 Url에 슬래시 뒤에를 <STRONG>모두 내보냅니다</STRONG> . 이 섹션의 예제에서는 "owa" (/owa/) 또는 "ecp" (/ecp/)로 끝나는 모든 url 후의 뒤에 오는 <STRONG>/</STRONG> 의 포함 합니다.



Outlook Web App의 경우 Windows Server 2012 R2에서 AD FS 관리 스냅인을 사용하여 신뢰 당사자 트러스트를 만들려면 다음을 수행합니다.

1.  **Server Manager**에서 **도구**를 클릭하고 **AD FS 관리**를 선택합니다.

2.  **AD FS 스냅인**의 **AD FS\\트러스트 관계**에서 **신뢰 당사자 트러스트**를 마우스 오른쪽 단추로 클릭하고 **신뢰 당사자 트러스트 추가**를 클릭하여 **신뢰 당사자 트러스트 추가** 마법사를 엽니다.

3.  **시작** 페이지에서 **시작**을 클릭합니다.

4.  **데이터 원본 선택** 페이지에서 **신뢰 당사자에 대한 데이터를 수동으로 입력**을 클릭하고 **다음**을 클릭합니다.

5.  **표시 이름 지정** 페이지의 **표시 이름** 상자에서 **Outlook Web App**를 입력 하 고 다음 **메모** (예: **이 https://mail.contoso.com/owa/에 대 한 신뢰는**)이 신뢰 당사자 트러스트에 대 한 설명을 입력 하 고 그런 다음 **다음** 을 클릭 합니다.

6.  **프로필 선택** 페이지에서 **AD FS 프로필**을 클릭하고 **다음**을 클릭합니다.

7.  **인증서 구성** 페이지에서 **다음**을 클릭합니다.

8.  **URL 구성** 페이지에서 **Ws-federation 수동 프로토콜 지원 사용** 을 클릭 하 고 **신뢰 당사자 Ws-federation 수동 프로토콜 URL**, <strong>유형 https://mail.contoso.com/owa/</strong>아래에서 다음 다음 **다음을 클릭 하 고** .

9.  **식별자 구성** 페이지에서 이 신뢰 당사자에 대한 식별자를 하나 이상 지정하고 **추가**를 클릭하여 식별자를 목록에 추가한 후에 **다음**을 클릭합니다.

10. **지금 다단계 인증을 구성하시겠습니까?** 페이지에서 **이 신뢰 당사자 트러스트에 대해 다단계 인증 설정 구성**을 선택합니다.

11. **다단계 인증 구성** 페이지에서 **지금 이 신뢰 당사자 트러스트에 대해 다단계 인증 설정을 구성하지 않음**이 선택되어 있는지 확인한 후에 **다음**을 클릭합니다.

12. **발급 권한 규칙 선택** 페이지에서 **모든 사용자가 이 신뢰 당사자에 액세스하도록 허용**을 선택한 후 **다음**을 클릭합니다.

13. **트러스트 추가 준비** 페이지에서 설정을 검토한 후 **다음**을 클릭하여 신뢰 당사자 트러스트 정보를 저장합니다.

14. **마침** 페이지에서 **마법사를 닫을 때 이 신뢰 당사자 트러스트에 대한 클레임 규칙 편집 대화 상자 열기**가 선택되어 있지 않은지 확인한 후 **닫기**를 클릭합니다.

EAC에 대해 신뢰 당사자 트러스트를 만들려면 위의 단계를 다시 수행하여 두 번째 신뢰 당사자 트러스트를 만들되 표시 이름으로 **Outlook Web App**이 아닌 **EAC**를 입력해야 합니다. 설명으로는 **This is a trust for the Exchange Admin Center**를 입력하고 **신뢰 당사자 WS-Federation 수동 프로토콜 URL**로는 <strong>https://mail.contoso.com/ecp</strong>를 입력합니다.

클레임 기반 ID 모델에서 페더레이션 서비스로서의 AD FS(Active Directory Federation Services) 기능은 클레임 집합이 포함된 토큰을 발급하는 것입니다. 클레임 규칙은 AD FS에서 발급하는 클레임과 관련한 결정을 관리합니다. 클레임 규칙 및 모든 서버 구성 데이터는 AD FS 구성 데이터베이스에 저장됩니다.

필요한 두 클레임 규칙을 만들어야 합니다.

  - Active Directory 사용자 SID

  - Active Directory UPN

필수 클레임 규칙을 추가 합니다.

1.  **Server Manager**에서 **도구**를 클릭하고 **AD FS 관리**를 클릭합니다.

2.  콘솔 트리의 **AD FS\\트러스트 관계**에서 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**를 클릭한 다음 Outlook Web App에 대한 신뢰 당사자 트러스트를 클릭합니다.

3.  **신뢰 당사자 트러스트** 창에서 Outlook Web App 트러스트를 마우스 오른쪽 단추로 클릭한 다음 **클레임 규칙 편집**을 클릭합니다.

4.  **클레임 규칙 편집** 창의 **발급 변환 규칙** 탭에서 **규칙 추가**를 클릭하여 변환 클레임 규칙 추가 마법사를 시작합니다.

5.  **규칙 서식 파일 선택** 페이지의 **클레임 규칙 서식 파일**에 있는 목록에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택한 후 **다음**을 클릭합니다.

6.  **규칙 구성** 페이지의 **규칙 유형 선택** 단계에서 **클레임 규칙 이름** 아래에 클레임 규칙의 이름을 입력합니다. **ActiveDirectoryUserSID**와 같이 클레임 규칙을 설명하는 이름을 사용합니다. **사용자 지정 규칙**에 이 규칙에 대한 다음 클레임 규칙 언어 구문을 입력합니다.
    
    ```powershell
    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);
    ```

7.  **규칙 구성** 페이지에서 **마침**을 클릭합니다.

8.  **클레임 규칙 편집** 창의 **발급 변환 규칙** 탭에서 **규칙 추가**를 클릭하여 변환 클레임 규칙 추가 마법사를 시작합니다.

9.  **규칙 서식 파일 선택** 페이지의 **클레임 규칙 서식 파일**에 있는 목록에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택한 후 **다음**을 클릭합니다.

10. **규칙 구성** 페이지의 **규칙 유형 선택** 단계에서 **클레임 규칙 이름** 아래에 클레임 규칙의 이름을 입력합니다. **ActiveDirectoryUPN**과 같이 클레임 규칙을 설명하는 이름을 사용합니다. **사용자 지정 규칙**에 이 규칙에 대한 다음 클레임 규칙 언어 구문을 입력합니다.
    
    ```powershell
    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);
    ```

11. **마침**을 클릭합니다.

12. **클레임 규칙 편집** 창에서 **적용**과 **확인**을 차례로 클릭합니다.

13. 신뢰 당사자 트러스트 EAC에 대해이 절차의 3-12 단계를 반복 합니다.

또는 릴레이 당사자 트러스트를 만들고 Windows PowerShell을 사용 하 여 클레임 규칙 수 있습니다.

1.  .txt 파일 두 개(IssuanceAuthorizationRules.txt 및 IssuanceTransformRules.txt)를 만듭니다.

2.  파일의 내용을 두 변수로 가져옵니다.

3.  다음의 두 cmdlet을 실행하여 신뢰 당사자 트러스트를 만듭니다. 이 예에서는 cmdlet을 실행하면 클레임 규칙도 구성됩니다.

**IssuanceAuthorizationRules.txt에는 다음 내용이 포함되어 있습니다.**

```powershell
@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");
```

**IssuanceTransformRules.txt에는 다음 내용이 포함되어 있습니다.**

```powershell
@RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 

@RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);
```

**다음 명령을 실행 합니다.**

```powershell
[string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt

[string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt

Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
```

## 4 단계-웹 응용 프로그램 프록시 역할 서비스 (선택 사항)를 설치 합니다.


> [!NOTE]
> 단계 4, 5 단계와 6 단계 되어 사용자가 Exchange OWA를 게시 하려면에 대 한 웹 응용 프로그램 프록시 및 AD FS 인증을 수행 하는 웹 응용 프로그램 프록시를 원하는 사용자를 사용 하 여 ECP입니다. 그러나 웹 응용 프로그램 프록시를 사용 하지 않는 하 고 자체 AD FS 인증을 수행 하는 Exchange 않으려는 경우 7 단계를 건너뛸 수 있으므로 웹 응용 프로그램 프록시와 게시 Exchange, 필요 하지 않습니다.



웹 응용 프로그램 프록시는 Windows Server 2012 r 2에서에서 새 원격 액세스 역할 서비스입니다. 웹 응용 프로그램 프록시는 회사 네트워크 외부에서 액세스할 수 있는 많은 장치에서 사용자를 허용 하려면 회사 네트워크 내부 웹 응용 프로그램에 대 한 역방향 프록시 기능을 제공 합니다. 웹 응용 프로그램 프록시 Active Directory Federation Services (AD FS)를 사용 하 여 웹 응용 프로그램에 대 한 액세스를 사전 인증 및 AD FS 프록시도도 기능을 수행 합니다. 웹 응용 프로그램 프록시 필요 하지 않지만 AD FS 외부 클라이언트에 액세스할 수 있는 경우 것이 좋습니다. 그러나 Outlook Web App 에서 오프 라인 액세스는 웹 응용 프로그램 프록시를 통해 AD FS 인증을 사용 하는 경우 지원 되지 않습니다. [설치 하 고 내부 응용 프로그램을 게시에 대 한 웹 응용 프로그램 프록시 구성](https://go.microsoft.com/fwlink/?linkid=392705) 를 표시 하 여 웹 응용 프로그램 프록시를 통합 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다.

> [!CAUTION]
> AD FS가 설치되어 있는 것과 같은 서버에는 웹 응용 프로그램 프록시를 설치할 수 없습니다.


웹 응용 프로그램 프록시를 배포하려면 웹 응용 프로그램 프록시 서버로 사용할 서버에 웹 응용 프로그램 프록시 역할 서비스가 포함된 원격 액세스 서버 역할을 설치해야 합니다. 웹 응용 프로그램 프록시 역할 서비스를 설치하려면 다음을 수행합니다.

1.  웹 응용 프로그램 프록시 서버의 **Server Manager**에서 **관리**와 **역할 및 기능 추가**를 차례로 클릭합니다.

2.  역할 및 기능 추가 마법사에서 **다음**을 세 번 클릭하여 **서버 역할** 페이지로 이동합니다.

3.  **서버 역할** 페이지의 목록에서 **원격 액세스**를 선택하고 **다음**을 클릭합니다.

4.  **기능** 페이지에서 **다음**을 클릭합니다.

5.  **원격 액세스** 페이지에서 정보를 확인하고 **다음**을 클릭합니다.

6.  **역할 서비스** 페이지에서 **웹 응용 프로그램 프록시**를 선택합니다. 그런 다음 **역할 및 기능 추가 마법사** 창에서 **기능 추가**와 **다음**을 차례로 클릭합니다.

7.  **확인** 창에서 **설치**를 클릭합니다. **필요한 경우 자동으로 대상 서버 다시 시작**을 선택할 수도 있습니다.

8.  **설치 진행률** 대화 상자에서 설치가 정상적으로 수행되었는지 확인한 후 **닫기**를 클릭합니다.

다음 Windows PowerShell cmdlet은 위의 단계와 동일한 작업을 수행합니다.

```powershell
Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools
```

## 5 단계-웹 응용 프로그램 프록시 역할 서비스 (선택 사항) 구성

AD FS 서버에 연결하도록 웹 응용 프로그램 프록시를 구성해야 합니다. 웹 응용 프로그램 프록시 서버로 배포할 모든 서버에 대해 이 절차를 반복합니다.

웹 응용 프로그램 역할 서비스를 구성하려면 다음을 수행합니다.

1.  웹 응용 프로그램 프록시 서버의 **Server Manager**에서 **도구**와 **원격 액세스 관리**를 차례로 클릭합니다.

2.  **구성** 창에서 **웹 응용 프로그램 프록시**를 클릭합니다.

3.  **원격 액세스 관리** 콘솔의 가운데 창에서 **웹 응용 프로그램 프록시 구성 마법사 실행**을 클릭합니다.

4.  웹 응용 프로그램 프록시 구성 마법사의 **시작** 대화 상자에서 **다음**을 클릭합니다.

5.  **페더레이션 서버** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.
    
      - **페더레이션 서비스 이름** 상자에 AD FS 서버의 FQDN(정규화된 도메인 이름)을 **adfs.contoso.com**과 같이 입력합니다.
    
      - **사용자 이름** 및 **암호** 상자에 AD FS 서버의 로컬 관리자 계정 자격 증명을 입력합니다.

6.  **AD FS 프록시 인증서** 대화 상자의 웹 응용 프로그램 프록시 서버에 현재 설치되어 있는 인증서 목록에서 AD FS 프록시 기능을 위해 웹 응용 프로그램 프록시에서 사용하도록 할 인증서를 선택하고 **다음**을 클릭합니다. **adfs.contoso.com**과 같은 페더레이션 서비스 이름이 제목인 인증서를 선택해야 합니다.

7.  **확인** 대화 상자에서 설정을 검토합니다. 필요한 경우 Windows PowerShell cmdlet을 복사하여 추가 설치를 자동화할 수 있습니다. **구성**을 클릭합니다.

8.  **결과** 대화 상자에서 구성이 정상적으로 완료되었는지 확인한 후 **닫기**를 클릭합니다.

다음 Windows PowerShell cmdlet은 위의 단계와 동일한 작업을 수행합니다.

```powershell
Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com
```

## 6 단계-웹 응용 프로그램 프록시 (선택 사항)를 사용 하 여 Outlook Web App 및 EAC를 게시

3 단계에서 Outlook Web App 및 EAC에 대 한 당사자 트러스트를 릴레이 클레임을 만든 하 고 이러한 응용 프로그램을 모두를 게시 해야 합니다. 하지만이 작업을 수행 하 여 신뢰 당사자 트러스트를 만들어진을 확인 하 고 Outlook Web App 및 EAC에 대해 적합 한 웹 응용 프로그램 프록시 서버의 인증서가 있는지 확인 합니다. AD FS 관리 콘솔에서 웹 응용 프로그램 프록시를 게시 하는 데 필요한 모든 AD FS 끝점에 대 한 **프록시를** 사용할 끝점을 설정 해야 합니다.

웹 응용 프로그램 프록시를 사용하여 Outlook Web App을 게시하려면 다음 단계를 수행합니다. EAC에 대해서도 이러한 단계를 반복합니다. EAC를 게시할 때는 이름, 외부 URL, 외부 인증서 및 백 엔드 URL을 변경해야 합니다.

웹 응용 프로그램 프록시를 사용하여 Outlook Web App 및 EAC를 게시하려면 다음을 수행합니다.

1.  웹 응용 프로그램 프록시 서버의 **원격 액세스 관리** 콘솔 **탐색** 창에서 **웹 응용 프로그램 프록시**를 클릭하고 **작업** 창에서 **게시**를 클릭합니다.

2.  새 응용 프로그램 게시 마법사의 **시작** 페이지에서 **다음**을 클릭합니다.

3.  **사전 인증** 페이지에서 <strong>AD FS(Active Directory Federation Services)</strong>를 클릭하고 **다음**을 클릭합니다.

4.  **신뢰 당사자** 페이지의 신뢰 당사자 목록에서 게시할 응용 프로그램의 신뢰 당사자를 선택하고 **다음**을 클릭합니다.

5.  **게시 설정** 페이지에서 다음 작업을 수행한 후 **다음**을 클릭합니다.
    
    1.  **이름** 상자에 응용 프로그램의 이름을 입력합니다. 이 이름은 **원격 액세스 관리 콘솔**의 게시된 응용 프로그램 목록에서만 사용됩니다. 이름으로 **OWA** 및 **EAC**를 사용할 수 있습니다.
    
    2.  **외부 URL** 상자에이 응용 프로그램에 대 한 외부 URL을 입력- Outlook Web App 및 EAC에 대 한 **https://external.contoso.com/ecp/https://external.contoso.com/owa/** 을 예입니다.
    
    3.  **외부 인증서** 목록에서 주체 이름이 외부 URL의 호스트 이름과 일치하는 인증서를 선택합니다.
    
    4.  **백엔드 서버 URL** 상자에 백엔드 서버의 URL을 입력 합니다. 외부 URL을 입력 하 고 백엔드 서버 URL이 다른 경우에 변경 해야 하는 경우이 값을 입력은 자동으로- Outlook Web App 및 EAC에 대 한 **https://mail.contoso.com/ecp/https://mail.contoso.com/owa/** 을 예입니다.
    

    > [!NOTE]
    > 웹 응용 프로그램 프록시는 URL의 호스트 이름은 변환할 수 있지만 경로는 변환할 수 없습니다. 따라서 다른 호스트 이름을 입력할 수는 있지만 경로는 동일하게 입력해야 합니다. 예를 들어 외부 URL <EM>https://external.contoso.com/app1/</EM> 및 백 엔드 서버 URL <EM>https://mail.contoso.com/app1/</EM>을 입력할 수 있습니다. 그러나 외부 URL <EM>https://external.contoso.com/app1/</EM> 및 백 엔드 서버 URL <EM>https://mail.contoso.com/internal-app1/</EM>을 입력할 수는 없습니다.



6.  **확인** 페이지에서 설정을 검토하고 **게시**를 클릭합니다. Windows PowerShell 명령을 복사하여 게시되는 응용 프로그램을 추가로 설정할 수 있습니다.

7.  **결과** 페이지에서 응용 프로그램이 정상적으로 게시되었는지 확인하고 **닫기**를 클릭합니다.

다음 Windows PowerShell cmdlet은 위의 Outlook Web App용 절차와 동일한 작업을 수행합니다.

```powershell
Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'
```

다음 Windows PowerShell cmdlet은 위의 EAC용 절차와 동일한 작업을 수행합니다.

```powershell
Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'
```

다음이 단계를 완료 한 후 웹 응용 프로그램 프록시는 Outlook Web App 및 EAC 클라이언트에 대 한 AD FS 인증을 수행 합니다를 강조 표시 됩니다 또한 프록시 자신을 대신해 Exchange에 연결 합니다. AD FS 인증을 위해 Exchange 자체 구성, 구성을 테스트 하려면 10 단계로 이동 하므로 필요가 없습니다.

## 단계 7-AD FS 인증을 사용 하도록 Exchange 2013 구성

Exchange 2013에서 Outlook Web App 및 EAC에 대해 클레임 기반 인증에 사용되도록 AD FS를 구성할 때는 Exchange 조직에 대해 AD FS를 사용하도록 설정해야 합니다. [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) cmdlet을 사용하여 조직의 AD FS 설정을 구성해야 합니다.

  - <strong>Https://adfs.contoso.com/adfs/ls/</strong>을 AD FS 발급자를 설정 합니다.

  - AD FS Uri를 <strong>https://mail.contoso.com/owa/</strong> 및 <strong>https://mail.contoso.com/ecp/</strong>.설정 합니다.

  - 인증서 지문을 Windows PowerShell을 사용 하 여 AD FS 서버에서 열고 `Get-ADFSCertificate -CertificateType "Token-signing"`를 입력 하 여 서명 AD FS 토큰을 소개 합니다. 찾을 수 있는 토큰 서명 인증서 지문을 할당 합니다. AD FS 토큰 서명 인증서가 만료 된 경우 새 AD FS 토큰 서명 인증서의 지문은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) cmdlet을 사용 하 여 업데이트 되어야 합니다.

Exchange 관리 셸에서 다음 명령을 실행 합니다.

```powershell
$uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"
```


> [!NOTE]
> <EM>-AdfsEncryptCertificateThumbprint</EM> 매개 변수는 이러한 시나리오에 대해 지원 되지 않습니다.



자세한 내용 및 구문에 대 한 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) 및 [Get ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706)를 참조 하십시오.

## 단계 8-OWA 및 ECP 가상 디렉터리에서 인증을 사용 AD FS

OWA 및 ECP 가상 디렉터리에 대해 유일한 인증 방법으로 AD FS 인증을 사용하도록 설정하고 기타 모든 인증 형식은 사용하지 않도록 설정합니다.


> [!WARNING]
> OWA 가상 디렉터리를 구성하기 전에 ECP 가상 디렉터리를 구성해야 합니다.



Exchange 관리 셸을 사용 하 여 ECP 가상 디렉터리를 구성 합니다. 셸 창에서 다음 명령을 실행 합니다.

```powershell
Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false
```

Exchange 관리 셸을 사용 하 여 OWA 가상 디렉터리를 구성 합니다. 셸 창에서 다음 명령을 실행 합니다.

```powershell
Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false
```


> [!NOTE]
> 조직에서 모든 클라이언트 액세스 서버에서 OWA 및 ECP 가상 디렉터리를 구성 하는 앞의 Exchange 관리 셸 명령 합니다. 모든 클라이언트 액세스 서버에 이러한 설정을 적용 하려면 않으려면 <EM>-Identity</EM> 매개 변수를 사용 하 고 클라이언트 액세스 서버를 지정 합니다. 조직에서 인터넷에 있는 클라이언트 액세스 서버에만 이러한 설정을 적용 하려는 것 같습니다 직면 합니다.



자세한 내용과 구문은 [Get-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/aa998588\(v=exchg.150\)) 및 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\)) 또는 [Get-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd351058\(v=exchg.150\)) 및 [Set-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd297991\(v=exchg.150\))를 참조하세요.

## 단계 9-다시 시작 또는 재활용 인터넷 정보 서비스 (IIS)

Exchange 가상 디렉터리 변경을 비롯하여 필수 단계를 모두 완료한 후에는 인터넷 정보 서비스를 다시 시작해야 합니다. 이렇게 하려면 다음 방법 중 하나를 사용하면 됩니다.

  - Windows PowerShell 사용:
    
    ```powershell
    Restart-Service W3SVC,WAS -noforce
    ```

  - 명령줄 사용: **시작** 및 **실행**을 차례로 클릭하고 `IISReset /noforce`를 입력한 다음 **확인**을 클릭합니다.

  - IIS(인터넷 정보 서비스) 관리자 사용: **Server Manager** \> **IIS**에서 **도구**를 클릭하고 **IIS(인터넷 정보 서비스) 관리자**를 클릭합니다. **IIS(인터넷 정보 서비스) 관리자** 창의 작업 창에 있는 **서버 관리**에서 **다시 시작**을 클릭합니다.

## 10 단계-Outlook Web App 및 EAC에 대해 AD FS 클레임을 테스트 합니다.

Outlook Web App에 대 한 AD FS 클레임을 테스트 합니다.

  - 웹 브라우저에서 Outlook Web App에 로그인- **https://mail.contoso.com/owa** 예

  - 브라우저 창에서 인증서 오류가 표시 되어도 계속 Outlook Web App 웹사이트에 로그온 합니다. 경우에 ADFS 리디렉션해야 로그인 페이지 또는 고 ADFS 자격 증명을 요청 합니다.

  - 사용자 이름 (도메인 \\ 사용자) 및 암호를 입력 한 다음 **로그인** 을 클릭 합니다.

Outlook Web App 창에 로드 됩니다.

EAC에 대해 AD FS 클레임을 테스트하려면 다음을 수행합니다.

1.  웹 브라우저에서 <strong>https://mail.contoso.com/ecp</strong>로 이동합니다.

2.  브라우저 창에서 인증서 오류가 표시 되어도 계속 ECP 웹사이트에 로그온 합니다. 경우에 ADFS 리디렉션해야 로그인 페이지 또는 고 ADFS 자격 증명을 요청 합니다.

3.  사용자 이름 (도메인 \\ 사용자) 및 암호를 입력 한 다음 **로그인** 을 클릭 합니다.

4.  EAC가 창에 로드됩니다.

## 알고 있으면 유용한 추가 정보

**다단계 인증**

온-프레미스 Exchange 2013 SP1 배포의 경우 클레임을 사용하여 AD FS(Active Directory Federation Services) 2.0을 배포 및 구성하면 Exchange 2013 SP1의 Outlook Web App 및 EAC가 인증서 기반 인증, 인증 또는 보안 토큰, 지문 인증 등의 다단계 인증 방법을 지원할 수 있습니다. 2단계 인증을 다른 인증 형식과 혼동하는 경우가 많습니다. 다단계 인증을 사용하려면 세 가지 인증 단계 중 두 가지를 사용해야 합니다. 이러한 단계는 다음과 같습니다.

  - 암호, PIN, 패턴 등 사용자만 알고 있는 요소

  - ATM 카드, 보안 토큰, 스마트 카드, 휴대폰 등 사용자만 가지고 있는 요소

  - 지문 등의 생체 인식 특성과 같이 사용자에게만 있는 요소

Windows Server 2012 r 2의에서 다단계 인증에 대 한 자세한 내용은 참조 하십시오. [개요: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 통해 위험 관리](https://go.microsoft.com/fwlink/?linkid=392707) 및 [연습 가이드:와 위험 관리 중요 한 응용 프로그램에 대 한 추가 다단계 인증](https://go.microsoft.com/fwlink/?linkid=392708)합니다.

Windows Server 2012 R2 AD FS 역할 서비스를에서 페더레이션 서비스 기능을 보안 토큰 서비스, 클레임을 함께 사용 되는 보안 토큰을 제공 하며 다단계 인증을 지원 하기 위한 기능을 제공 합니다. 페더레이션 서비스는 제공 되는 자격 증명을 기초로 하는 토큰을 발행 합니다. 계정 저장소에 사용자의 자격 증명을 확인 한 후에 대 한 클레임 사용자에 대 한 트러스트 정책 규칙에 따라 생성 되며 그런 다음 클라이언트에 대 한 발생 하는 보안 토큰에 추가 됩니다. 클레임에 대 한 자세한 내용은 [클레임 이해](https://go.microsoft.com/fwlink/?linkid=392709)을 참조 하십시오.

**다른 버전의 Exchange와 함께**

둘 이상의 버전의 Exchange 조직에 배포 된 경우 Outlook Web App 및 EAC에 대해 AD FS 인증을 사용 하는 것이 불가능 합니다. 이 시나리오는 Exchange 2010 및 Exchange 2013 배포에 대해서만 지원 하 고 이러한 Exchange 2013 서버 AD FS 인증을 위해 구성 된 모든 클라이언트를 통해 Exchange 2013 서버와 연결 하는 경우에 있습니다.

Exchange 2010 서버에 사서함이 있는 사용자가 AD FS 인증을 위해 구성 된 Exchange 2013 서버를 통해 자신의 사서함에 액세스할 수 있습니다. Exchange 2013 서버는 초기 클라이언트 연결 AD FS 인증을 사용 합니다. 그러나 Exchange 2010 서버로 프록시 된 연결 Kerberos를 사용 합니다. 직접 AD FS 인증을 위해 Exchange Server 2010을 구성 하는 지원 되는 방법은 없습니다.


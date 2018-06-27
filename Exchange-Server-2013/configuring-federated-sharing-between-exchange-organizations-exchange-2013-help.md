---
title: 'Exchange 조직 간의 페더레이션 공유 구성: Exchange 2013 Help'
TOCTitle: Exchange 조직 간의 페더레이션 공유 구성
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50483712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 조직 간의 페더레이션 공유 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

페더레이션 공유를 사용하면 온-프레미스 Exchange 조직의 사용자가 역시 페더레이션 공유에 대해 구성된 다른 Exchange 조직의 받는 사람과 약속 있음/없음 일정 정보를 공유할 수 있습니다. 약속 있음/없음 공유는 Exchange 2013을 실행 중인 두 조직 간에 가능하며 혼합된 Exchange 배포가 있는 조직 간에도 가능합니다. 페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md) 항목을 참조하십시오.

이 항목에서는 다음과 같은 일반적인 Exchange 배포의 서로 다른 유형 간에 약속 있음/없음 공유를 사용할 수 있도록 설정하기 위해 필요한 구성 단계와 요구 사항에 대한 요약을 제공합니다.

  - 두 개의 Exchange 2013조직

  - Exchange 2013조직 및 Exchange 2010 SP2 조직

  - Exchange 2007 조직(또는 혼합된 Exchange 2007 및 Exchange 2010 SP2 조직) 및 Exchange 2013 조직

  - Exchange 2003 조직(또는 혼합된 Exchange 2003 및 Exchange 2010 SP2 조직) 및 Exchange 2013 조직

페더레이션 공유와 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md) 항목을 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2시간

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차를 수행하기 전에 Exchange 조직 간에 약속 있음/없음 정보를 공유하는 데 관련된 제한 사항을 알고 있어야 합니다. 자세한 내용은 [Limitations of free/busy sharing](sharing-exchange-2013-help.md) 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## Exchange 2013 조직 간에 약속 있음/없음 공유 구성

두 조직에 대해 [페더레이션 공유 구성](configure-federated-sharing-exchange-2013-help.md)의 단계를 완료합니다.

## Exchange 2013 및 Exchange 2010 SP2 조직 간에 약속 있음/없음 공유 구성

  - Exchange 2013 조직에 대한 페더레이션 공유를 구성합니다. [페더레이션 공유 구성](configure-federated-sharing-exchange-2013-help.md)의 단계를 완료합니다.

  - Exchange 2010 SP2 조직에 대 한 페더레이션된 위임 (페더레이션 공유에 대 한 이전 이름)을 구성 합니다. [Configure 페더레이션 위임이](https://go.microsoft.com/fwlink/p/?linkid=268410)의 단계를 완료 합니다.

## Exchange 2013 및 Exchange 2007 조직 간에 약속 있음/없음 공유 구성

  - Exchange 2013 조직에 대한 페더레이션 공유를 구성합니다. [페더레이션 공유 구성](configure-federated-sharing-exchange-2013-help.md)의 단계를 완료합니다.

  - Exchange 2007 조직에서 다음 단계를 완료합니다.
    
    1.  **Exchange 2010 SP2 서버 추가**
        
        Exchange 2007 조직에서 클라이언트 액세스 서버 역할을 가진 Exchange 2010 SP2 서버를 설치 해야 합니다. 기존 Exchange 2010 서버를 사용 하는 경우 이러한도 업데이트 해야 Exchange 2010 s p 2로 합니다. Exchange 2007 조직에서 Exchange 2010을 설치 하는 방법에 대 한 정보를 [Exchange 2007-업그레이드 및 동시 사용 계획 로드맵](https://go.microsoft.com/fwlink/p/?linkid=268411)을 참조 하십시오.
    
    2.  **페더레이션 위임 구성**
        
        Exchange 2007 조직에 대 한 페더레이션된 위임 구성. Exchange 2007 조직에 Exchange 2010 SP2 서버를 [구성 페더레이션 위임이](https://go.microsoft.com/fwlink/p/?linkid=268410)의 단계를 완료 합니다.
    
    3.  **Active Directory 동기화 구성**
        
        조직 간에 약속 있음/없음 정보를 공유해야 하는 모든 사용자에 대해 Active Directory 동기화를 구성해야 합니다. 수동으로 Active Directory 동기화를 구성하거나 자동화된 Active Directory 동기화 서비스를 사용할 수 있습니다. Active Directory 동기화를 구성하려면 다음 단계를 참조하십시오.
        
          - **필수 구성 요소**   조직이 Active Directory 동기화 설치 요구 사항을 충족하는지 확인합니다.
            
            자세한 내용은 [Active Directory 동기화를 위한 준비](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **계획**   Microsoft Online Services 디렉터리 동기화 도구와 설치 로드맵을 숙지합니다.
            
            자세한 내용은 [Active Directory 동기화: 로드맵](http://go.microsoft.com/fwlink/p/?linkid=203007)을 참조하십시오.
        
          - **설치 및 구성**   온-프레미스 조직과 Office 365 테넌트 서비스 조직 간에 Active Directory 동기화를 구성합니다.
            
            자세한 내용을 보려면, 설치 및 업그레이드 Microsoft Online Services 디렉터리 동기화 도구[](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **가용성 주소 공간 만들기**
        
        Exchange 2007 사서함 사용자의 가용성 요청을 Exchange 2007 조직의 Exchange 2010 SP2 클라이언트 액세스 서버로 전달하는 원격 Exchange 2013 조직의 가용성 주소 공간을 만듭니다. 이 설정을 사용하면 원격 Exchange 2013 조직의 사용자에 대한 Exchange 2007 사용자의 사용자 가용성 요청이 Exchange 2007 조직의 Exchange 2010 클라이언트 액세스 서버를 통해 프록시됩니다. Exchange 2007 조직의 Exchange 2010 클라이언트 액세스 서버는 페더레이션 트러스트 및 조직 관계를 사용하여 원격 Exchange 2013 조직 포리스트 가용성 끝점으로 가용성 요청을 보냅니다.
        
        가용성 주소 공간을 구성하려면 Exchange 2007 조직의 Exchange 2010 클라이언트 액세스 서버에서 Exchange 관리 셸을 통해 다음 명령을 실행합니다.
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        자세한 구문 및 매개 변수 정보에 대 한 [Add-availabilityaddressspace](https://go.microsoft.com/fwlink/p/?linkid=268413)

## Exchange 2013 및 Exchange 2003 조직 간에 약속 있음/없음 공유 구성

  - Exchange 2013 조직에 대한 페더레이션 공유를 구성합니다. [페더레이션 공유 구성](configure-federated-sharing-exchange-2013-help.md)의 단계를 완료합니다.

  - Exchange 2003 조직에서 다음 단계를 완료합니다.
    
    1.  **Exchange 2010 SP2 서버 추가**.
        
        Exchange 2003 조직에서 클라이언트 액세스 서버 역할을 가진 Exchange 2010 SP2 서버를 설치 해야 합니다. 기존 Exchange 2010 서버가 자신이 업데이트 해야 Exchange 2010 s p 2로 합니다. Exchange 2003 조직에 Exchange 2010을 설치 하는 방법에 대 한 정보를 [Exchange 2003-업그레이드 및 동시 사용 계획 로드맵](https://go.microsoft.com/fwlink/?linkid=268414)을 참조 하십시오.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Exchange 2013 및 Exchange 2003 조직 간에 약속 있음/없음 공유가 제대로 작동하려면 공유 폴더 계층에 <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 공유 폴더가 있어야 합니다. Exchange 2010 설치 중 Outlook 2003 지원을 위한 클라이언트 설정 구성의 일부로 공용 폴더를 만드는 옵션을 선택하는 경우에만 Exchange 2003 조직의 Exchange 2010 사서함 서버에 이 폴더가 자동으로 생성됩니다. 또한 이 옵션은 Exchange 2010 사서함 서버가 조직에 설치된 첫 번째 사서함 서버인 경우에만 설치 프로세스 중에 표시됩니다. 설치 중에 <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 공용 폴더가 만들어지지 않으면 이 폴더를 수동으로 만들어야 합니다. 이 공용 폴더를 만드는 방법에 대한 자세한 내용은 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2555008">엔터프라이즈 환경용 Microsoft Office 365에서 Exchange 페더레이션을 사용하는 경우 약속 있음/없음 문제를 해결하는 방법</a>을 참조하십시오.</td>
        </tr>
        </tbody>
        </table>
    
    2.  **페더레이션 위임 구성**.
        
        Exchange 2003 조직에 대 한 페더레이션된 위임 구성. Exchange 2003 조직에서 Exchange 2010 SP2 서버를 [구성 페더레이션 위임이](https://go.microsoft.com/fwlink/p/?linkid=268410)의 단계를 완료 합니다.
    
    3.  **Active Directory 동기화 구성**.
        
        조직 간에 약속 있음/없음 정보를 공유 하는 모든 사용자에 대 한 active Directory 동기화를 구성 해야 합니다. Active Directory 동기화를 수동으로 구성으로 수행 하거나 자동화 된 Active Directory 동기화 서비스를 사용 합니다. Active Directory 동기화 하는 방법에 대 한 자세한 내용은, [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645)를 참조 하십시오.
        
          - **필수 구성 요소**   조직이 Active Directory 동기화 설치 요구 사항을 충족하는지 확인합니다.
            
            자세한 내용은 [Active Directory 동기화를 위한 준비](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **계획**   Microsoft Online Services 디렉터리 동기화 도구와 설치 로드맵을 숙지합니다.
            
            자세한 내용은 [Active Directory 동기화: 로드맵](http://go.microsoft.com/fwlink/p/?linkid=203007)을 참조하십시오.
        
          - **설치 및 구성**   온-프레미스 조직과 Office 365 테넌트 서비스 조직 간에 Active Directory 동기화를 구성합니다.
            
            자세한 내용을 보려면, 설치 및 업그레이드 Microsoft Online Services 디렉터리 동기화 도구[](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Exchange 2003 조직에서 약속 있음/없음 공유를 위한 공용 폴더 구성.**
        
        Exchange 2003 서버에서 다음 단계를 완료합니다.
        
          - Exchange System Manager의 콘솔 트리에서 **관리 그룹** \> **기본 관리 그룹** \> **서버**로 이동합니다.
        
          - Exchange 2003 서버를 선택하고 **기본 저장소 그룹** \> **공용 폴더 저장소** \> **공용 폴더** \> **Schedule+ 약속 있음/없음**으로 이동합니다.
        
          - 작업 창에서 **기본 관리 그룹**에 대해 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 폴더를 선택합니다.
        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT)** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.
        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT) 속성**에서 **복제** 탭을 선택합니다.
        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT)** 폴더를 Exchange 2010 클라이언트 액세스/사서함 서버에 복제하려면 **추가**를 클릭합니다.
        
          - **공용 폴더 저장소 선택**에서 Exchange 2010 클라이언트 액세스/사서함 서버에 대한 **공용 폴더 데이터베이스**를 선택한 다음 **확인**을 클릭합니다.
            

            > [!NOTE]
            > 기본적으로 Exchange는 공용 폴더 데이터베이스에 설정된 복제 일정을 사용합니다.

        
          - **확인**을 클릭하여 **OU=EXTERNAL (FYDIBOHF25SPDLT) 속성**을 닫고 변경 사항을 저장합니다.
        
          - **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 폴더에 대해 위의 단계와 동일한 단계를 완료합니다.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>공용 폴더의 크기에 따라 이 복제를 완료하는 데 몇 시간이 걸릴 수 있습니다.</td>
            </tr>
            </tbody>
            </table>
        
          - **OU=EXTERNAL (FYDIBOHF25SPDLT)** 및 **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 공용 폴더를 Exchange 2010 클라이언트 액세스/사서함 서버에 복제한 후에는 Exchange 2003 서버에서 이러한 공용 폴더의 복제본을 제거해야 합니다.
    
    5.  **LegacyExchangeDN 매개 변수 수정**
        
        원격 Exchange 2013 조직을 참조하는 Exchange 2003 조직에서 메일 사용이 가능한 모든 개체에 대한 *LegacyExchangeDN* 매개 변수를 수정합니다. 메일 사용이 가능한 개체의 기존 OU(조직 구성 단위) 값을 **External (FYDIBOHF25SPDLT)**로 변경합니다. 예를 들어 **LegacyExchangeDN=/o=First Organization/ou=External (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name**입니다.
        
        Exchange 2003 조직에서 메일 사용이 가능한 개체를 수정 하려면 [Active Directory 서비스 인터페이스 편집기 (ADSI 편집) 도구](https://go.microsoft.com/fwlink/?linkid=294644) 또는 [Microsoft Exchange Server LegacyDN 유틸리티](http://go.microsoft.com/fwlink/?linkid=294643)중 하나를 사용할 수 있습니다.


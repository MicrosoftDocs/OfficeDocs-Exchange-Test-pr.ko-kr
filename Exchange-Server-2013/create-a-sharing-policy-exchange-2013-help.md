---
title: '공유 정책 만들기: Exchange 2013 Help'
TOCTitle: 공유 정책 만들기
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50484156
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공유 정책 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

공유 정책을 사용하여 Exchange 조직의 사용자가 조직 외부의 사용자와 일정 정보를 공유하는 방법을 제어할 수 있습니다. 공유 정책을 사용하면 일정 정보를 여러 유형의 외부 사용자와 함께 사용자가 설정한 대로 사용자 간에 공유할 수 있습니다. 공유 정책으로 Office 365 또는 기타 온-프레미스 Exchange 조직과 같은 외부 페더레이션 조직, 외부 비페더레이션 조직 및 인터넷 액세스 권한이 있는 개인과의 일정 정보 공유가 지원됩니다. 특정 공유 정책을 사용자에게 적용하려면 [사서함에 공유 정책 적용](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md)을 참조하십시오.


> [!IMPORTANT]
> 공유 정책 만들기 (영문) Exchange 조직에서 페더레이션 공유를 설정 하는 여러 단계 중 하나입니다. 다른 페더레이션 Exchange 조직과 일정 정보를 공유 하려면 먼저 온-프레미스 Exchange 조직에 대 한 Azure Active Directory 인증 시스템과 페더레이션 트러스트를 설정 해야 합니다. 페더레이션 트러스트는 인터넷 공유 정책에 대 한 필요 하지 않습니다.



페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

페더레이션과 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "일정 및 공유 권한? [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 섹션입니다.

  - 페더레이션 Exchange 조직 간의 공유 정책에는 다음 조건이 필요합니다.
    
      - 각 Exchange 조직에는 Exchange 2013 클라이언트 액세스 서버가 있어야합니다. 여기서 한 조직에 Exchange 2013 클라이언트 액세스 서버가 하 고 다른 하나 조직 Exchange 2010 SP3 또는 이후 클라이언트 액세스 서버에 Exchange 조직 간의 공유 정책도 지원 됩니다.
    
      - 각 Exchange 조직의 Azure AD 인증 시스템과 페더레이션 트러스트를 만들었습니다. 자세한 내용은 [페더레이션 트러스트를 구성 합니다.](configure-a-federation-trust-exchange-2013-help.md)를 참조 합니다.
    
      - 각 Exchange 조직의 페더레이션 조직 식별자를 구성해야 합니다. 사용자의 전자 메일 주소 생성에 사용된 도메인이 조직 식별자에 추가되어 있어야 합니다.
    
      - 사용자 사서함이 Exchange 2013 사서함 서버 또는 각 Exchange 조직에 Exchange 2010 사서함 서버에 배치 됩니다.
    
      - Outlook 2010 이상 버전 및 Outlook Web App 사용자만 공유 초대를 만들 수 있습니다.

  - 비 페더레이션 Exchange 조직 또는 개인에 대한 공유 정책에는 다음 조건이 필요합니다.
    
      - 사용자의 일정 정보를 공유하는 Exchange 조직에 Exchange 2013 클라이언트 액세스 서버가 있어야 합니다.
    
      - 사용자 일정 정보를 공유하는 Exchange 조직의 Exchange 2013 사서함 서버에 사용자 사서함이 있어야 합니다.
    
      - Exchange 2013 클라이언트 액세스 서버가 Outlook Web App 액세스를 허용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공유 정책 만들기

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **개별 공유**에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **새 공유 정책**의 **정책 이름** 상자에 공유 정책의 이름을 입력합니다.

4.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 공유 정책에 공유 규칙을 지정합니다.

5.  **공유 규칙**에서 다음 옵션 중 하나를 선택하여 공유할 도메인을 지정합니다.
    
      - **모든 도메인과 공유**
    
      - **특정 도메인과 공유**

6.  **특정 도메인과 공유** 선택하면 공유할 도메인의 이름을 입력합니다. 이 공유 정책에 대해 도메인을 두 개 이상 입력해야 하는 경우 첫 번째 도메인의 설정을 저장한 다음 공유 규칙을 편집하여 도메인을 더 추가합니다.

7.  정책에 적용할 일정 공유 수준을 정의하려면 **일정 폴더 공유** 확인란을 선택한 후 다음 옵션 중 하나를 선택합니다.
    
      - **약속 있음/없음 일정 정보(시간만 포함)**
    
      - **시간, 제목, 위치가 있는 약속 있음/없음 일정 정보**
    
      - **시간, 주제, 위치 및 제목을 비롯하여 모든 일정 약속 정보**

8.  **저장**을 클릭하여 공유 정책에 대한 규칙을 설정합니다.

9.  이 공유 정책을 Exchange 조직의 사용자에 대한 기본 공유 정책으로 만들려면 **이 정책을 내 기본 공유 정책으로 설정** 확인란을 클릭합니다.

10. **저장**을 클릭하여 공유 정책을 만듭니다.

## EAC를 사용하여 모든 사용자가 전체 일정 세부 사항을 공유하도록 허용

모든 사용자가 조직 외부 사용자와 전체 일정 세부 정보를 공유하도록 기본 공유 정책을 편집할 수 있습니다.

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **개별 공유**에서 **기본 공유 정책**을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **공유 정책** 대화 상자에서 **모든 도메인과 공유**를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **공유 규칙** 대화 상자의 **공유할 정보 지정**에서 **시간, 주제, 위치 및 제목을 비롯하여 모든 일정 약속 정보**를 선택하고 **저장**을 클릭합니다.

5.  **공유 정책** 대화 상자에서 **저장**을 클릭하여 공유 정책에 대한 규칙을 설정합니다.

## 셸을 사용하여 공유 정책 만들기

  - 이 예에서는 외부 페더레이션 도메인 contoso.com에 대한 공유 정책 Contoso를 만듭니다. 이 정책을 사용하여 contoso.com 도메인의 사용자가 사용자의 자세한 일정 약속 있음/없음 정보를 볼 수 있습니다. 기본적으로 이 정책은 사용할 수 있습니다.
    
    ```powershell
    New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail
    ```

  - 이 예에서는 두 가지 다른 페더레이션된 도메인(contoso.com 및 woodgrovebank.com)에 대해 다른 공유 작업을 각 도메인에 구성한 공유 정책 ContosoWoodgrove를 만듭니다. 정책은 사용하지 않도록 설정되어 있습니다.
    
      ```powershell
      New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false
      ```

  - 이 예에서는 제한된 일정 약속 있음/없음 정보에 대해 공유 작업이 구성된 클라이언트 액세스 서버 CAS01 및 사서함 서버 MAIL01이 있는 Exchange 조직에 대한 익명 공유 정책을 만듭니다. 이 정책을 사용하는 경우 Exchange 조직의 사용자가 인터넷에 액세스할 수 있는 사용자를 초대하고 링크를 전송하여 일정 약속 있음/없음 정보를 볼 수 있습니다. 정책은 사용하도록 설정되어 있습니다.
    
    1.  MAIL01의 웹 프록시 URL을 설정합니다.
        
        ```powershell
        Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
        ```
    
    2.  CAS01에서 게시 가상 디렉터리를 사용하도록 설정합니다.
      
          ```powershell
          Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
          ```
    
    3.  익명 공유 정책을 만들고 제한된 일정 정보 공유를 구성합니다.
        
          ```powershell
          New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
          ```

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [New-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/ko-kr/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

공유 정책이 만들어졌는지 확인하려면 다음 셸 명령을 실행하여 공유 정책 정보를 확인합니다.

```powershell
Get-SharingPolicy <policy name> | format-list
```


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



---
title: '인터넷 일정 게시를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 인터넷 일정 게시를 사용 하도록 설정
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50556067
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 인터넷 일정 게시를 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-08-22_

**요약:**  이러한 절차를 사용 하 여 OWA 사용자가 Exchange 2013 조직에서 외부 조직과 일정 약속 있음/없음 정보를 공유할 수 있도록 합니다.

Microsoft Exchange Server 2013 조직의 사용자는 Exchange를 사용하지 않는 조직의 사용자나 인터넷에 액세스할 수 있는 다른 개인과 일정 약속 있음/없음 정보를 공유할 수 있습니다. 인터넷을 통해 일정을 게시하면 유연성이 향상되고 더 많은 사용자와 일정 약속 있음/없음 정보를 공유할 수 있습니다.

인터넷 일정 게시를 사용하도록 설정하려면 다음과 같이 일반적인 세 단계를 거쳐야 합니다.

1.  사서함 서버 (이 단계는만 필요 하면 조직에서 이미 존재 하는 URL의 웹 프록시 그렇지 않은 경우 2 단계로 이동 하는 경우)에 대 한 웹 프록시 URL을 구성 합니다.

2.  클라이언트 액세스 서버의 게시 가상 디렉터리를 사용하도록 설정합니다.

3.  인터넷 일정 게시 전용의 공유 정책을 만들거나 **익명** 도메인을 지원하도록 기본 공유 정책을 업데이트합니다. 어떤 방법을 사용하든 Exchange 조직의 사용자는 인터넷에 액세스할 수 있는 다른 사용자가 게시된 URL에 액세스하여 제한된 일정 약속 있음/없음 정보를 볼 수 있도록 초대할 수 있습니다.


> [!IMPORTANT]
> 3 단계를 완료 하면 사용자가 다음 Outlook에서 자신의 일정을 게시 해야 합니다. 일정 게시 사용자가 조직 외부의 사용자에 게 수 있는 Url을 만듭니다. 하나의 URL 구독 일정을 Outlook 또는 Outlook Web App과 다른 사용을 사용 하 여 받는 사람 보기 웹 브라우저에서 일정 한 받는 사람 수 있습니다. 각 사용자는 다른 사용자가 볼 수 있는 정보의 양을 제어할 수 있습니다.



공유 정책과 관련된 추가 관리 작업에 대한 자세한 내용은 [공유 정책](sharing-policies-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "일정 및 권한 공유" 항목

  - 사용자의 일정 정보를 공유하는 Exchange 조직에 Exchange 2013 클라이언트 액세스 서버가 있어야 합니다.

  - 사용자의 일정 정보를 공유하는 Exchange 조직의 Exchange 2013 사서함 서버에 사용자 사서함이 있어야 합니다.

  - Outlook 2010 이상 버전 및 Outlook Web App 사용자만 공유 초대를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 셸을 사용하여 웹 프록시 URL 구성


> [!NOTE]
> 이 단계는 웹 프록시 URL을 조직에 이미 존재 하는 경우에 합니다. 그렇지 않은 경우에 2 단계로 건너뜁니다.<BR>웹 프록시 URL을 구성하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다.



이 예에서는 MAIL01 사서함 서버에서 웹 프록시 URL을 구성합니다.

```powershell
Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ExchangeServer](https://technet.microsoft.com/ko-kr/library/bb123716\(v=exchg.150\))를 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

웹 프록시 URL이 구성되었는지 확인하려면 다음 셸 명령을 실행하고 *InternetWebProxy* 매개 변수 정보를 확인합니다.

```powershell
Get-ExchangeServer | format-list
```

## 2단계: 셸을 사용하여 게시 가상 디렉터리를 사용하도록 설정


> [!NOTE]
> 게시 가상 디렉터리를 사용하도록 설정하는 데 EAC를 사용할 수 없습니다.



이 예에서는 CAS01 클라이언트 액세스 서버에서 게시 가상 디렉터리를 사용하도록 설정합니다.

```powershell
Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true
```

여기서 `CAS01\owa (Default Web Site)` identity 서버 이름 및 Outlook Web App 가상 디렉터리를 모두입니다.

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))를 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

게시 가상 디렉터리를 사용하도록 설정되었는지 확인하려면 다음 셀 명령을 실행하고 *ExternalURL* 매개 변수 정보를 확인합니다.

```powershell
Get-OwaVirtualDirectory | format-list
```

## 3 단계: 만들기 또는 인터넷 일정 게시를 위한 공유 정책 구성


> [!NOTE]
> 3 단계에서에서 다음 옵션 Exchange Online 환경에만 적용 됩니다.



인터넷에 대 한 공유 정책 만들기 (영문) 중에서 선택할 수 있습니다 (선택 사항 1) 일정 게시 또는 기본 인터넷 일정 게시 (선택 사항 2)에 대 한 공유 정책을 구성 합니다. 두 옵션으로 EAC 또는 셸을 사용 하 여 선택할을 수 있습니다.

## 옵션 1: 인터넷 일정 게시를 위한 공유 정책 만들기

인터넷 일정 게시를 위한 공유 정책을 만들려면 다음 단계를 수행합니다.

## EAC를 사용하여 다음을 수행합니다.

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **개별 공유**에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **공유 정책**에서 **정책 이름** 필드에 공유 정책의 이름(예: **인터넷**)을 입력합니다.

4.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 공유 정책의 공유 규칙을 정의합니다.

5.  **공유 규칙**에서 **특정 도메인과 공유**를 클릭하고 해당 상자에 **Anonymous**를 입력합니다.

6.  공유 정책에 적용할 일정 공유 수준을 지정하려면 **일정 폴더 공유** 확인란을 선택하고 다음 중 하나를 선택합니다.
    
      - **약속 있음/없음 일정 정보(시간만 포함)**
    
      - **약속 있음/없음 일정 정보(시간, 제목, 위치 포함)**
    
      - **시간, 주제, 위치 및 제목을 비롯하여 모든 일정 약속 정보**

7.  **저장**을 클릭하여 공유 정책에 대한 규칙을 설정합니다.

8.  **공유 정책**에서 **저장**을 클릭하여 정책을 만듭니다.

## 셸 사용

이 예에서는 인터넷이라는 이름의 인터넷 일정 게시 공유 정책을 만들고 약속 있음/없음 정보만 공유하도록 정책을 구성합니다 정책은 사용하도록 설정되어 있습니다.

```powershell
New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```

이 예에서는 인터넷 공유 정책을 사용자 사서함에 추가합니다.

```powershell
Set-Mailbox -Identity <user name> -SharingPolicy "Internet"
```

이 예에서는 인터넷 공유 정책을 조직 단위(OU)에 추가합니다.

```powershell
Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"
```

구문과 매개 변수에 대한 자세한 내용은 [New-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd298186\(v=exchg.150\)) 및 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))을 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

공유 정책이 만들어졌는지 확인하려면 다음 셸 명령을 실행하여 공유 정책 정보를 확인합니다.

```powershell
Get-SharingPolicy <policy name> | format-list
```

## 옵션 2: 기본 공유 인터넷 일정 게시에 대 한 정책 구성

인터넷 일정 게시를 위한 기본 공유 정책을 구성하려면 다음 단계를 수행합니다.

## EAC를 사용하여 다음을 수행합니다.

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **개별 공유**에서 기본 공유 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **공유 정책**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 정책에 공유 규칙을 추가합니다.

4.  **공유 규칙**에서 **특정 도메인과 공유**를 클릭하고 해당 상자에 **Anonymous**를 입력합니다.

5.  공유 정책에 적용할 일정 공유 수준을 지정하려면 **일정 폴더 공유** 확인란을 선택하고 다음 중 하나를 선택합니다.
    
      - **약속 있음/없음 일정 정보(시간만 포함)**
    
      - **약속 있음/없음 일정 정보(시간, 제목, 위치 포함)**
    
      - **시간, 주제, 위치 및 제목을 비롯하여 모든 일정 약속 정보**

6.  **저장**을 클릭하여 공유 정책에 대한 규칙을 설정합니다.

7.  **공유 정책**에서 **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸 사용

이 예에서는 기본 공유 정책을 업데이트하고 약속 있음/없음 정보만 공유하도록 정책을 구성합니다. 정책은 사용하도록 설정되어 있습니다.

```powershell
Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

기본 공유 정책이 업데이트되었는지 확인하려면 다음 셸 명령을 실행하여 공유 정책 정보를 확인합니다.

```powershell
Get-SharingPolicy <policy name> | format-list
```


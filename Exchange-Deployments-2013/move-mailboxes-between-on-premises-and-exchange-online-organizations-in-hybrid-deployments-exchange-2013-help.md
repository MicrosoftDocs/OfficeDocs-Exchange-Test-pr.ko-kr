---
title: '하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동: Exchange 2013 Help'
TOCTitle: 하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51407773
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동

 

_<strong>적용 대상:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2017-10-02_

Exchange 기반 하이브리드 배포에서는 온-프레미스 Exchange 사서함을 Exchange Online 조직으로 이동하거나 Exchange Online 사서함을 Exchange 조직으로 이동할 수 있습니다. 온-프레미스와 Exchange Online 조직 간에 사서함을 이동할 때 마이그레이션 일괄 처리를 사용하여 원격 사서함 이동 요청을 수행할 수 있습니다. 이 방법을 사용하면 새 사용자 사서함을 만들고 사용자 정보를 가져오는 대신 기존 사서함을 이동할 수 있습니다. 이 방법은 클라우드로의 전체 Exchange 마이그레이션의 일부로 온-프레미스 Exchange 조직에서 Exchange Online으로 다른 사용자 사서함을 마이그레이션하는 것과 다릅니다. 이 항목에서 설명하는 사서함 이동은 온-프레미스 Exchange와 Exchange Online 조직 간의 장기적인 공존 관계에서 Exchange를 관리하는 작업에 속합니다.

Exchange Online으로늬 온-프레미스 Exchange 조직 마이그레이션에 대한 자세한 내용은 [여러 전자 메일 계정을 Office 365로 마이그레이션하는 방법](https://go.microsoft.com/fwlink/p/?linkid=524030)을 참조하세요.


> [!IMPORTANT]
> 이 항목의 사서함 이동 절차를 완료하려면 온-프레미스와 Exchange Online 조직 간의 하이브리드 배포를 구성해야 합니다. 하이브리드 배포에 대한 자세한 내용은 <A href="exchange-server-hybrid-deployments-exchange-2013-help.md">Exchange Server 하이브리드 배포</A>를 참조하세요.<BR><BR>UM(통합 메시징) 사용이 가능한 사서함을 Exchange Online으로 이동하기 전에 온-프레미스 비즈니스용 Skype 2015, 비즈니스용 Skype Online 및 Exchange Online이 <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">하이브리드 배포 필수 구성 요소</A>에 지정된 요구 사항을 모두 충족하는지 확인해야 합니다. 온-프레미스 UM 사서함 정책을 Exchange Online의 정책에 매핑하는 방법에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 마이그레이션 일괄 처리를 구성하는 10분이 걸리지만 마이그레이션을 완료하는 데 소요되는 총 시간은 각 마이그레이션 일괄 처리에 포함된 사서함 수에 따라 다릅니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[받는 사람에 게 사용 권한](https://technet.microsoft.com/ko-kr/library/dd638132\(v=exchg.150\))의 "사서함 이동 및 마이그레이션 권한" 섹션

  - 하이브리드 배포는 온-프레미스와 Exchange Online 조직 간에 구성됩니다.

  - Exchange 2013을 실행하는 경우 사서함 복제 프록시 서비스(MRSProxy)가 온-프레미스 Exchange 2013 클라이언트 액세스 서버에서 사용되도록 설정되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](https://technet.microsoft.com/ko-kr/library/jj150484\(v=exchg.150\))을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 1단계: 마이그레이션 끝점 만들기

Exchange 하이브리드 배포에서 온보드 및 오프보드 원격 이동 마이그레이션을 수행하기 전에 Exchange 원격 마이그레이션 끝점을 만드는 것이 좋습니다. 마이그레이션 끝점에는 MRS 프록시 서비스를 실행하는 온-프레미스 Exchange 서버에 대한 연결 설정이 포함됩니다. 이 설정은 Exchange Online과의 원격 이동 마이그레이션을 수행하는 데 필요합니다.

단계별 절차는 마이그레이션 끝점 만들기를 참조하세요.

## 2단계: MRSProxy 서비스 사용

온-프레미스 Exchange 2013 클라이언트 액세스 서버에서 MRSProxy 서비스를 사용하지 않는 경우 EAC(Exchange 관리 센터)에서 다음 단계를 따르세요.

1.  EAC를 열고 **서버** \> **가상 디렉터리**로 이동합니다.

2.  클라이언트 액세스 서버를 선택하고 **EWS** 가상 디렉터리를 선택한 다음 **편집**![편집 아이콘](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **MRS 프록시 사용** 확인란을 선택하고 **저장**을 클릭합니다.

## 3단계: EAC를 사용하여 사서함 이동

Exchange 서버의 EAC에서 **Office 365** 탭의 원격 이동 마이그레이션 마법사를 사용하여 온-프레미스 조직의 기존 사용자 사서함을 Exchange Online 조직으로 이동하거나, Exchange Online 사서함을 온-프레미스 조직으로 이동할 수 있습니다. 다음 절차 중 하나를 선택합니다.

## 온-프레미스 사서함을 Exchange Online으로 이동

Exchange 서버의 EAC에서 **Office 365** 탭의 원격 이동 마이그레이션 마법사를 사용하여 온-프레미스 조직의 기존 사용자 사서함을 Exchange Online 조직으로 이동할 수 있습니다. 다음 단계를 따릅니다.

1.  EAC를 열고 **Office 365** \> **받는 사람** \> **마이그레이션**으로 이동합니다.

2.  **추가** ![아이콘 추가](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 **Exchange Online으로 마이그레이션**을 선택합니다.

3.  **마이그레이션 유형 선택** 페이지에서 **원격 이동 마이그레이션**을 선택하고 **다음**을 클릭합니다.

4.  **사용자 선택** 페이지에서 **추가** ![아이콘 추가](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 Office 365로 이동할 온-프레미스 사용자를 선택한 다음 **추가**, **확인**을 차례로 클릭합니다. **다음**을 클릭합니다.

5.  **Windows 사용자 계정 자격 증명 입력** 페이지의 **온-프레미스 관리자 이름** 텍스트 필드에 온-프레미스 관리자 계정 이름을 입력하고 **온-프레미스 관리자 암호** 텍스트 필드에 이 계정과 연결된 암호를 입력합니다. 예를 들어 "corp\\administrator"와 암호를 입력합니다. **다음**을 클릭합니다.
    

    > [!NOTE]
    > 마이그레이션 끝점을 이미 만든 경우 이 단계에 대한 끝점 확인 프롬프트가 나타납니다. 두 개 이상의 마이그레이션 끝점을 만든 경우 마이그레이션 끝점 드롭다운 메뉴에서 끝점을 선택해야 합니다.



6.  마법사가 마이그레이션 끝점을 확인할 때 **마이그레이션 끝점 확인** 페이지에 온-프레미스 Exchange 서버의 FDQN이 나열되는지 확인합니다. 예를 들어 "mail.contoso.com"과 같습니다. **다음**을 클릭합니다.
    

    > [!NOTE]
    > Exchange 서버의 MRSProxy 서비스는 Exchange Online으로 이동할 사서함을 여러 개 선택한 경우 자동으로 사서함 이동 요청을 제한합니다. 사서함 이동을 완료하기 위한 전체 시간은 선택한 사서함의 전체 수와 사서함의 크기 그리고 MRSProxy의 구성에 따라 다릅니다. MRSProxy 사용자 지정에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/bb232205(v=exchg.150)">메시지 제한</A>을 참조하세요.



7.  **이동 구성** 페이지의 **새 마이그레이션 일괄 처리 이름** 텍스트 필드에 마이그레이션 일괄 처리 이름을 입력합니다. 아래쪽 화살표 ![아래쪽 화살표 아이콘](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "아래쪽 화살표 아이콘")를 사용하여 **Office 365로 마이그레이션하는 사서함의 대상 배달 도메인**을 선택합니다. 대부분의 하이브리드 배포에서 이는 Exchange Online 조직 사서함에 사용되는 기본 SMTP 도메인입니다. 예를 들면 contoso.mail.onmicrosoft.com과 같습니다. **보관 사서함과 함께 기본 사서함 이동** 옵션을 선택하고 **다음**을 클릭합니다.

8.  **일괄 처리 시작** 페이지에서 일괄 처리 완료 보고서를 수신할 받는 사람을 하나 이상 선택합니다. **자동으로 일괄 처리 시작** 옵션이 선택되어 있는지 확인하고 **자동으로 마이그레이션 일괄 처리 완료** 확인란을 선택합니다. **새로 만들기**를 클릭합니다.

## 온-프레미스 조직으로 Exchange Online 사서함 이동

Exchange 서버의 EAC에서 **Office 365** 탭의 원격 이동 마이그레이션 마법사를 사용하여 온-프레미스 조직의 기존 사용자 사서함을 Exchange Online 조직으로 이동할 수 있습니다.

1.  EAC를 열고 **Office 365** \> **받는 사람** \> **마이그레이션**으로 이동합니다.

2.  **추가** ![아이콘 추가](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 **Exchange Online에서 마이그레이션**을 선택합니다.

3.  **사용자 선택** 페이지에서 **이동할 사용자 선택**을 선택하고 **다음**을 클릭합니다.

4.  **사용자 선택** 페이지에서 **추가** ![아이콘 추가](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 온-프레미스 조직으로 이동할 Exchange Online 사용자를 선택한 다음 **추가**, **확인**을 차례로 클릭합니다. **다음**을 클릭합니다.

5.  마법사가 마이그레이션 끝점을 확인할 때 **마이그레이션 끝점 확인** 페이지에 온-프레미스 Exchange 서버의 FDQN이 나열되는지 확인합니다. 예를 들어 "mail.contoso.com"과 같습니다. **다음**을 클릭합니다.
    

    > [!NOTE]
    > Exchange 서버의 MRSProxy 서비스는 Exchange Online으로 이동할 사서함을 여러 개 선택한 경우 자동으로 사서함 이동 요청을 제한합니다. 사서함 이동을 완료하기 위한 전체 시간은 선택한 사서함의 전체 수와 사서함의 크기 그리고 MRSProxy의 속성에 따라 다릅니다. MRSProxy 사용자 지정에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/bb232205(v=exchg.150)">메시지 제한</A>을 참조하세요.



6.  **이동 구성** 페이지의 **새 마이그레이션 일괄 처리 이름** 텍스트 필드에 마이그레이션 일괄 처리의 이름을 입력합니다. **Office 365로 마이그레이션할 사서함의 대상 배달 도메인** 필드에 대상 배달 도메인을 입력합니다. 대부분의 하이브리드 배포에서 이 도메인은 온-프레미스 및 Exchange Online 조직 사서함 둘 다에 사용되는 기본 SMTP 도메인이 됩니다. 예를 들면 contoso.com과 같습니다.

7.  선택한 사용자의 보관 사서함도 이동할지 여부를 선택하고 **대상 데이터베이스** 텍스트 필드에 이 사서함을 이동할 데이터베이스 이름을 입력합니다. 예를 들면 사서함 데이터베이스 123456789와 같습니다. **다음**을 클릭합니다.

8.  **일괄 처리 시작** 페이지에서 일괄 처리 완료 보고서를 수신할 받는 사람을 하나 이상 선택합니다. **자동으로 일괄 처리 시작**가 선택되어 있는지 확인하고 **자동으로 마이그레이션 일괄 처리 완료** 확인란을 선택합니다. **새로 만들기**를 클릭합니다.

## 4단계: 완료된 마이그레이션 일괄 처리 제거

사서함 이동이 완료된 후에는 동일한 사용자를 다시 이동할 경우 오류가 발생할 가능성을 최소화하기 위해 완료된 마이그레이션 일괄 처리를 제거하는 것이 좋습니다.

완료된 마이그레이션 일괄 처리를 제거하려면

1.  EAC를 열고 **Office 365** \> **받는 사람** \> **마이그레이션**으로 이동합니다.

2.  완료된 마이그레이션 일괄 처리를 클릭하고 **삭제** ![삭제 아이콘](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  삭제 경고 확인 대화 상자에서 **예**를 클릭합니다.

## 5단계: 웹에서 Outlook에 대한 오프라인 액세스 다시 설정

웹에서 Outlook(이전의 Outlook Web App)의 오프라인 액세스를 통해 사용자는 네트워크에 연결되어 있지 않은 경우에도 자신의 사서함에 액세스할 수 있습니다. Exchange 사서함을 Exchange Online으로 마이그레이션하는 경우 사용자는 브라우저에서 오프라인 액세스 설정을 다시 설정해야 오프라인으로 웹에서 Outlook을 사용할 수 있습니다. 웹에서 Outlook의 오프라인 액세스, 오프라인 액세스를 지원하는 브라우저 및 오프라인 액세스를 설정하는 방법에 대한 자세한 내용은 [오프라인으로 Outlook Web App 사용](https://go.microsoft.com/fwlink/p/?linkid=286942)을 참조하세요.

## 작동 여부는 어떻게 확인합니까?

온-프레미스와 Exchange Online 조직 간에 기존 사용자 사서함을 이동할 때 원격 이동 마법사가 성공적으로 완료되면 사서함 이동이 예상대로 완료되었음을 나타냅니다.

사서함 이동 프로세스를 완료하는 데 몇 분 정도 걸리므로 EAC를 열고 **Office 365** \> **받는 사람** \> **마이그레이션**을 선택하여 원격 이동 마법사에서 선택한 사서함의 이동 상태를 표시하는 방법을 통해 이동이 제대로 작동하는지 확인할 수도 있습니다. **상태** 값은 사서함이 이동되는 동안에는 **동기화 중**이고, 사서함이 온-프레미스 또는 Exchange Online 조직으로 성공적으로 이동된 경우에는 **완료됨**입니다.

사서함 이동이 완료된 후 사서함 속성 확인을 통해 온-프레미스 또는 Exchange Online 조직에 있는 원격 사서함이 성공적으로 이동되었음을 확인할 수 있습니다. 이렇게 하려면 온-프레미스 조직 또는 Exchange Online 조직에 대한 EAC에서 **받는 사람** \> **사서함**으로 이동합니다. 사용자 사서함의 **사서함 유형**이 Exchange Online 사서함의 경우 **Office 365**, 온-프레미스 사서함의 경우 **사용자**로 표시되어야 합니다.

Exchange 관리 셸에서 다음 cmdlet을 실행하여 마이그레이션 일괄 처리의 상태를 확인할 수도 있습니다.

    Get-MigrationBatch -Identity <batch name>

문제가 있는 경우 Office 365 포럼에서 도움을 요청하세요. 포럼에 액세스하려면 클라우드 기반 서비스에 대한 관리자 액세스가 승인된 계정을 사용하여 로그인해야 합니다. 포럼 주소는 다음과 같습니다. [Office 365 포럼](https://go.microsoft.com/fwlink/p/?linkid=201915)

## Office 365의 새로운 기능


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning용 단축 아이콘" alt="LinkedIn Learning용 단축 아이콘" /> <strong>Office 365를 처음 사용하시나요?</strong><br />
LinkedIn Learning에서 제공하는 <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>의 무료 비디오 과정을 확인해보세요.</p></td>
</tr>
</tbody>
</table>


---
title: '하이브리드 배포에서 온-프레미스 Exchange 서버를 제거하는 경우 및 방법: Exchange 2013 Help'
TOCTitle: 하이브리드 배포에서 온-프레미스 Exchange 서버를 제거하는 경우 및 방법
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 65059983
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 하이브리드 배포에서 온-프레미스 Exchange 서버를 제거하는 경우 및 방법

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2017-07-27_

Exchange 하이브리드 배포에서 전체 클라우드 구현으로 이동할 준비가 되면 이 문서를 읽어보세요.

[Exchange 하이브리드 배포 및 Office 365를 사용 하 여 마이그레이션](https://msdn.microsoft.com/en-us/library/ff633682\(v=exchsrvcs.149\).aspx)에 설명 된 하이브리드 배포 방법을 사용 하 여은 Exchange Online 에 회사를 가져오기 위한 더 눈에 띄는 옵션 중 하나입니다. 이를 쉽게 온보드 하 고 보드 오프 사서함 (다른 모든 기본 옵션은 온보드만) 수 있는 유일한 옵션입니다. 하는 기능 보드 오프 하이브리드 구성에는 다음과 같은 주요 옵션이 있습니다.

이 항목은 Exchange 하이브리드를 해제 하는 것에 대 한 옵션을 이해 하도록 도와줍니다 및 옵션 이러한 각를 구현 해야 합니다. 시기 및 Exchange 하이브리드 서버를 해제 하는 방법에 많은 차이가 없습니다. 의미를 이해 하 고 제대로 온-프레미스 서버의 전체 또는 부분 폐기를 계획 하는 시간 라인으로 전환 하는 것이 중요 합니다.

  - **크로스-프레미스 가용성**. 이를 통해 회의를 예약하는 동안 해당 사서함 프레미스에 관계없이 사용자의 약속 없음/있음 정보를 볼 수 있습니다.

  - **크로스-프레미스 보관**. 이를 통해 고객은 사용자의 보관 사서함만 클라우드로 이동할 수 있습니다. 이는 종종 고객이 Office 365, 특히 Exchange Online을 시도하는 첫 번째 단계입니다.

  - **크로스-프레미스 검색**. 이를 통해 고객은 두 프레미스 모두에서 사서함 및 보관 파일을 크롤링할 전자 검색을 수행할 수 있습니다.(OAuth 인증을 구성해야 함).

  - **Outlook Web App URL 리디렉션**. 이를 통해 사용자를 Outlook Web App 액세스에 적절한 프레미스로 리디렉션할 수 있습니다.

  - **이동 후 프로필을 다시 만들 필요가 없음**. 다른 마이그레이션 옵션과 달리 사서함 GUID가 변경되지 않습니다. 따라서 사서함 이동 후 프로필을 다시 만들거나 OST를 다시 다운로드할 필요가 없습니다.

조직의 요구 사항에 따라 하이브리드 배포는 가장 원활한 사용자 및 공존 환경을 제공하는 최상의 옵션입니다.

## Exchange Online으로 마이그레이션하는 다른 방법

모든; 없는 하이브리드 배포 실제로 일반적으로 더 나은 옵션이 있습니다. 하이브리드 구성을 배포 하도록 선택 했을 하는 테 넌 트의 대부분은 50 개 미만 시트입니다. 하이브리드 배포의 장점 목록이 눈에 띄는 들릴 수, 하는 동안 복잡성 작업과 관련 하 여 물게 가격 함께 제공 됩니다. 하이브리드 배포의 기능을 필요로 더 작은 테 넌 트의 일부 있지만 대부분 테 넌 트에 대 한는 것이 훨씬 더 나은 환경 중 하나를 단독 사용 하 여 미리 구성 된, 또는 IMAP 마이그레이션 옵션. 적용할 마이그레이션 방법을 결정할 때 사용할 수는 FastTrack을 호출 하는 프로그램 방법이 있습니다. FastTrack 대 한 정보는 [Office 365 FastTrack 페이지](https://go.microsoft.com/fwlink/?linkid=846696)에 설명 되어있습니다.

다음 표를 사용 하 여 조직에 대해 작동 하는 마이그레이션 유형을 결정 합니다. (자세한 내용은 [Office 365에 여러 전자 메일 계정으로 마이그레이션하는 방법](https://support.office.com/en-us/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=en-us%26rs=en-sg%26ad=sg)참조)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>기존 조직</th>
<th>마이그레이션할 사서함 수</th>
<th>온-프레미스 조직에서 사용자 계정을 관리할지 여부</th>
<th>마이그레이션 유형</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013, Exchange 2010, Exchange 2007 또는 Exchange 2003</p></td>
<td><p>2,000개 미만</p></td>
<td><p>아니요</p></td>
<td><p>단독형 Exchange 마이그레이션</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 또는 Exchange 2003</p></td>
<td><p>2,000개 미만</p></td>
<td><p>아니요</p></td>
<td><p>미리 구성된 Exchange 마이그레이션</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 또는 Exchange 2003</p></td>
<td><p>2, 000 개 이상의 사서함*</p></td>
<td><p>예</p></td>
<td><p>Exchange 하이브리드 배포의 원격 이동 마이그레이션 또는 미리 구성된 Exchange 마이그레이션</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 또는 Exchange 2010</p></td>
<td><p>2, 000 개 이상의 사서함*</p></td>
<td><p>예</p></td>
<td><p>Exchange 하이브리드 배포의 원격 이동 마이그레이션</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server 또는 이전 버전</p></td>
<td><p>최대값 없음</p></td>
<td><p>예</p></td>
<td><p>IMAP 마이그레이션</p></td>
</tr>
<tr class="even">
<td><p>Exchange가 아닌 온-프레미스 메시징 시스템</p></td>
<td><p>최대값 없음</p></td>
<td><p>예</p></td>
<td><p>IMAP 마이그레이션</p></td>
</tr>
</tbody>
</table>


\* 2, 000 개 미만의 일부 조직에서는 하이브리드 배포에만 제공 되는 기능과 특징에서 도움이 될 수 있습니다. 것을 소개 하는 복잡성 하이브리드 배포의 이점을 신중 하 게 고려 하는 것이 중요 합니다. 2, 000 개 미만의 사용 하는 고객 단독형를 고려 하는 것이 좋습니다 하이브리드 배포를 진행 하기 전에 마이그레이션 미리 구성 된 또는 합니다.

## 온-프레미스에서 Exchange 서버를 해제하지 않는 것이 좋은 이유

하이브리드 구성을 사용하는 고객은 일정 기간이 지난 후 모든 사서함이 Exchange Online으로 이동된 것을 발견하는 경우가 종종 있습니다. 이때 온-프레미스에서 Exchange 서버를 제거하도록 결정할 수 있습니다. 그러나 더 이상 클라우드 사서함을 관리할 수 없다는 사실을 알게 됩니다.

테넌트에 대해 디렉터리 동기화가 설정되고 사용자가 온-프레미스에서 동기화된 경우에는 대부분의 특성을 Exchange Online에서 관리할 수 없으며 온-프레미스에서 관리해야 합니다. 이는 하이브리드 구성으로 인한 것이 아니라 디렉터리 동기화 때문에 발생합니다. 또한 하이브리드 구성 마법사를 실행하지 않고 직접 디렉터리 동기화를 설정한 경우에도 대부분의 받는 사람 작업을 클라우드에서 관리할 수 없습니다. 자세한 내용은 [TechNet 블로그](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx)를 참조하세요.

## 타사 관리 도구를 사용할 수 있나요?

타사 관리 도구 또는 ADSIEDIT를 사용할 수 있는지 여부에 대한 질문을 자주 받습니다. 사용할 수 있지만 지원되지는 않습니다. Exchange 받는 사람 및 개체를 관리하는 데 사용할 수 있는 도구는 Exchange 관리 콘솔, EAC(Exchange 관리 센터) 및 Exchange 관리 셸뿐입니다. 타사 관리 도구를 사용하기로 결정하면 모든 위험 부담은 사용자가 감수해야 합니다. 타사 관리 도구는 올바르게 작동하는 경우가 많지만 Microsoft는 이러한 도구의 유효성을 검사하지 않습니다.

## 일반적인 시나리오

하이브리드 구성에서 클라우드로 이동하는 것은 단순한 작업이 아닙니다. 하이브리드 구성으로 전환하는 프로세스에는 많은 시간이 걸립니다. 문제가 있기만 하지만, Microsoft는 거의 불가능해 보이던 하이브리드로의 변환 작업을 마법사 기반의 매우 쉬운 프로세스로 만드는 작업에 성공했습니다.

그러나 하이브리드 구성에서 클라우드로 전환하는 방법에는 거의 노력을 들이지 않았습니다. 즉각적인 목표에 따라 이 프로세스는 몇 가지 지침만 따르면 되는 매우 간단한 과정일 수 있습니다. 다음은 고객의 최종 목표를 적절히 실현하는 방법에 대한 권장 사항과 함께 세 가지 일반적인 하이브리드 시나리오입니다.

하이브리드 고객층은 매우 다양하기 때문에 모든 고객을 "일반적인" 시나리오에 맞추기는 어렵습니다. 아래에서는 온-프레미스 Exchange Server 해제에 대한 몇 가지 대략적인 시나리오를 제공하기 때문에 이러한 시나리오를 읽어보고 해제 계획을 수립할 때 요구 사항에 가장 적합한 시나리오를 결정해야 합니다.

## 시나리오 1

**문제:** 하이브리드 구성에서 실행 되 고 내 조직 및 Exchange Online 에서 내 사서함의 일부를 I 합니다. I 필요가 없습니다 온-프레미스에서 내 사용자를 관리 하 고 디렉터리 동기화 또는 암호 동기화에 대 한 필요 나타나지 않습니다.

**해결 방법:** 모든 사용자가 Office 365에서 관리되고 추가적인 디렉터리 동기화 요구 사항이 없으므로 디렉터리 동기화를 안전하게 해제하고 온-프레미스 환경에서 Exchange를 제거할 수 있습니다.

![온-프레미스 환경에서 Exchange 제거](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "온-프레미스 환경에서 Exchange 제거") 디렉터리 동기화를 비활성화하고 Exchange 하이브리드를 제거하려면

1.  `Get-OrganizationConfig |fl PublicFoldersEnabled` 를 실행 하 고 원격으로 설정 되지 않았는지 확인 합니다. 원격 ","로 설정 하는 경우 공용 폴더에 대해 액세스를 계속 하려면 자료 Exchange Online 를 마이그레이션할 해야 합니다. 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션](https://technet.microsoft.com/ko-kr/library/dn874017\(v=exchg.150\))을 참조 하십시오.

2.  모든 사서함을 Exchange Online으로 이미 이동한 경우에는 MX 및 자동 검색 DNS 레코드를 온-프레미스 대신 Exchange Online을 가리키도록 할 수 있습니다. 자세한 내용은 [참조: Office 365에 대한 외부 도메인 이름 시스템 레코드](http://technet.microsoft.com/ko-kr/library/hh852557.aspx)를 참조하세요.
    

    > [!IMPORTANT]
    > 내부 DNS와 외부 DNS를 모두 업데이트해야 합니다. 그렇지 않으면 클라이언트 연결 동작이 일치하지 않을 수 있습니다.



3.  이제 Exchange 서버에서 SCP(서비스 연결 지점) 값을 제거해야 합니다. 이렇게 하면 반환되는 SCP가 없으므로 클라이언트에서 자동 검색에 DNS 메서드를 대신 사용합니다. 아래에 예제가 나와 있습니다.
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Exchange 2007 서버가 환경에 있는 경우 설정을 null 처리하기 위해 Exchange 2007 서버에서 유사한 명령을 실행해야 합니다.



4.  하이브리드 구성 마법사에서 만든 것 중 삭제하려는 인바운드 및 아웃바운드 커넥터가 있습니다. 다음 단계를 사용하여 이 작업을 수행합니다.
    
    1.  [Office 365 관리 포털](http://portal.office.com)에 테넌트 관리자로 로그인합니다.
    
    2.  **Exchange** 관리 옵션을 선택합니다.
    
    3.  **메일 흐름** -\> **연결** 로 이동합니다.
    
    4.  이제 인바운드 및 아웃바운드 커넥터를 해제하거나 삭제할 수 있습니다. HCW는 아래 그림과 같이 **인바운드 출처\<고유 식별자\>** 및 **아웃바운드 대상\<고유 식별자\>** 라는 고유한 네임스페이스를 사용하여 커넥터를 만듭니다.
        
        ![하이브리드 구성 마법사에서 네임스페이스가 고유한 커넥터를 만듭니다.](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "하이브리드 구성 마법사에서 네임스페이스가 고유한 커넥터를 만듭니다.")  

5.  하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다. 다음 단계를 사용하여 이 작업을 수행합니다.
    
    1.  [Office 365 관리 포털](http://portal.office.com)에 테넌트 관리자로 로그인합니다.
    
    2.  Exchange 관리 옵션을 선택합니다.
    
    3.  **조직** 으로 이동합니다.
    
    4.  아래 그림과 같이 **조직 공유** 에서 **O365를 온-프레미즈로 - \<고유 식별자\>** 라는 조직을 제거합니다.
        
        ![하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다.")  

6.  Exchange 하이브리드 배포에 대해 OAuth가 구성된 경우 온-프레미스와 Office 365 모두에서 이 구성을 해제할 수 있습니다. 대부분의 환경에서는 소수의 고객만 OAuth를 구성하기 때문에 이러한 단계를 건너뛸 수 있습니다.
    
    온-프레미스 구성을 해제하려면
    
    1.  Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.
    
    2.  다음 명령을 실행합니다.
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Exchange Online 구성을 해제하려면
    
    1.  Windows PowerShell을 Exchange Online에 연결합니다.
    
    2.  다음 명령을 실행합니다.
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        *Identity* 매개 변수는 하이브리드 구성 마법사를 사용하여 OAuth를 구성한 것으로 가정합니다. 그렇지 않은 경우 커넥터 ID에 대해 지정한 값을 조정해야 할 수 있습니다.

7.  테넌트에 대한 디렉터리 동기화를 해제합니다. 이 단계를 완료하면 모든 사용자 관리 작업이 Office 365 관리 도구를 통해 수행됩니다. 즉, Exchange 관리 콘솔 또는 EAC(Exchange 관리 센터)를 더 이상 사용하지 않습니다. 디렉터리 동기화를 해제하는 방법에 대한 자세한 내용은 [디렉터리 동기화 비활성화](https://technet.microsoft.com/ko-kr/library/dn144760.aspx)를 참조하세요.

8.  이제 온-프레미스 서버에서 Exchange을 안전하게 제거할 수 있습니다.

## 시나리오 2

**문제:** 조직이 약 1년 동안 하이브리드 구성에서 운영되며 이제 드디어 마지막 사서함을 클라우드로 이동했습니다. Exchange Online 사서함의 사용자 인증을 위해 AD FS(Active Directory 페더레이션 서비스)를 유지할 계획입니다. 이 시나리오는 디렉터리 동기화를 유지하려는 고객에게 적용됩니다.

**해결 방법:** 해결 방법: 고객이 AD FS를 유지할 계획이므로 이의 전제 조건인 디렉터리 동기화도 유지해야 합니다. 따라서 온-프레미스 환경에서 Exchange 서버를 완전히 제거할 수 없습니다. 그러나 대부분의 Exchange 서버를 해제하고 사용자 관리용 서버 몇 개만 남겨 둘 수 있습니다. 작업이 거의 완전히 Exchange Online으로 전환되었기 때문에 실행 상태가 유지되는 서버를 가상 컴퓨터에서 실행할 수 있습니다.

아래 그림에서는 바람직한 최종 상태를 설명합니다.

![일부 남아 있는 Exchange 서버 제거](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "일부 남아 있는 Exchange 서버 제거")

아래 그림에서는 실제 최종 상태를 설명합니다.

![Exchange 서버를 제거하기 전의 상태](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "Exchange 서버를 제거하기 전의 상태") AD FS 및 디렉터리 동기화를 유지하고 대부분의 Exchange 서버를 해제하려면

1.  `Get-OrganizationConfig |fl PublicFoldersEnabled`를 실행하여 Remote로 설정되어 있지 않은 것을 확인합니다. Remote로 설정되어 있는 경우 공용 폴더에 계속 액세스하려면 Exchange Online으로 마그레이션해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션](https://technet.microsoft.com/ko-kr/library/dn874017\(v=exchg.150\))을 참조하세요.
    

    > [!IMPORTANT]
    > 공용 폴더를 Exchange Online으로 마이그레이션하는 것이 옵션이 아닌 경우 사용자를 위해 계속 필요하므로 이동해서는 안 됩니다.



2.  모든 사서함을 Exchange Online으로 이동한 후 대부분의 Exchange 서버를 해제하기 위해 첫 번째로 할 일은 MX 및 자동 검색 DNS 레코드를 온-프레미스 대신 Exchange Online을 가리키도록 설정하는 것입니다. 자세한 내용은 [참조: Office 365에 대한 외부 도메인 이름 시스템 레코드](http://technet.microsoft.com/ko-kr/library/hh852557.aspx)를 참조하세요.
    

    > [!IMPORTANT]
    > 내부 DNS와 외부 DNS를 모두 업데이트해야 합니다. 그렇지 않으면 클라이언트 연결 및 메일 흐름 동작이 일치하지 않을 수 있습니다.



3.  이제 Exchange 서버에서 SCP(서비스 연결 지점) 값을 제거해야 합니다. 이렇게 하면 반환되는 SCP가 없으므로 클라이언트에서 자동 검색에 DNS 메서드를 대신 사용합니다. 아래에 예제가 나와 있습니다.
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Exchange 2007 서버가 환경에 있는 경우 설정을 null 처리하기 위해 Exchange 2007 서버에서 유사한 명령을 실행해야 합니다.



4.  나중에 하이브리드 구성 개체가 다시 만들어지지 않도록 하려면 Active Directory에서 하이브리드 구성 개체를 제거해야 합니다. 이렇게 하려면 Exchange 관리 셸을 열고 다음을 실행합니다.
    
        Remove-HybridConfiguration

5.  사용자 관리 및 만들기를 위해 유지할 서버를 제외하고 모든 Exchange 서버를 제거합니다. 하나로도 가능하지만 사용자 관리용 서버는 두 개만 있으면 충분합니다. 또한 데이터베이스 가용성 그룹 또는 기타 가용성 옵션이 필요 없습니다.

6.  Exchange 하이브리드 배포에 대해 OAuth가 구성된 경우 온-프레미스와 Office 365 모두에서 이 구성을 해제할 수 있습니다. 대부분의 환경에서는 소수의 고객만 OAuth를 구성하기 때문에 이러한 단계를 건너뛸 수 있습니다.
    
    온-프레미스 구성을 해제하려면
    
    1.  Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.
    
    2.  다음 명령을 실행합니다.
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Exchange Online 구성을 해제하려면
    
    1.  Windows PowerShell을 Exchange Online에 연결합니다.
    
    2.  다음 명령을 실행합니다.
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        Identity 매개 변수는 하이브리드 구성 마법사를 사용하여 OAuth를 구성한 것으로 가정합니다. 그렇지 않은 경우 커넥터 ID에 대해 지정한 값을 조정해야 할 수 있습니다.

7.  하이브리드 구성 마법사에서 만든 것 중 삭제하려는 인바운드 및 아웃바운드 커넥터가 있습니다. 다음 단계를 사용하여 이 작업을 수행합니다.
    
    1.  [Office 365 관리 포털](http://portal.office.com)에 테넌트 관리자로 로그인합니다.
    
    2.  **Exchange** 관리 옵션을 선택합니다.
    
    3.  **메일 흐름** -\> **커넥터** 로 이동합니다.
    
    4.  이제 인바운드 및 아웃바운드 커넥터를 해제하거나 삭제할 수 있습니다. HCW는 아래 그림과 같이 **인바운드 출처\<고유 식별자\>** 및 **아웃바운드 대상\<고유 식별자\>** 라는 고유한 네임스페이스를 사용하여 커넥터를 만듭니다.
        
        ![하이브리드 구성 마법사에서 네임스페이스가 고유한 커넥터를 만듭니다.](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "하이브리드 구성 마법사에서 네임스페이스가 고유한 커넥터를 만듭니다.")  

8.  하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다. 다음 단계를 사용하여 이 작업을 수행합니다.
    
    1.  [Office 365 관리 포털](http://portal.office.com)에 테넌트 관리자로 로그인합니다.
    
    2.  **Exchange** 관리 옵션을 선택합니다.
    
    3.  **조직**으로 이동합니다.
    
    4.  아래 그림과 같이 **조직 공유** 에서 **O365를 온-프레미즈로 - \<고유 식별자\>** 라는 조직을 제거합니다.
        
        ![하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "하이브리드 구성 마법사에서 만든 조직 관계를 제거합니다.")  

## 시나리오 3

**문제:** 모든 사서함을 Exchange Online으로 이동한 후 온-프레미스에서 Exchange 서버를 제거하려고 합니다. 그러나 해당 서버에서 응용 프로그램의 SMTP(Simple Mail Transfer Protocol) 릴레이, 공용 폴더 액세스 등의 다른 용도에 Exchange를 사용하고 있는 것을 알았습니다. 조직의 현재 요구 사항을 충족하기 위해 온-프레미스에 Exchange 서버가 필요한 경우 온-프레미스 서버를 제거하지 않는 것이 좋습니다.

**해결 방법:** 이 시점에서는 Exchange 및 하이브리드 구성을 제거하지 않는 것이 좋습니다. 자동 검색 레코드가 Exchange Online을 가리키도록 설정하는 프로세스만 시작해도 하이브리드 공용 폴더 액세스와 같은 일부 기능이 즉시 중단될 수 있습니다. MX 레코드를 Exchange Online Protection을 가리키도록 변경할 수 있으며, 일부 온-프레미스 Exchange 서버를 제거할 수도 있습니다. 그러나 나머지 하이브리드 기능을 처리하기에 충분히 정도를 유지해야 합니다. 이렇게 하면 일반적으로 온-프레미스 설치 공간이 매우 작아집니다.


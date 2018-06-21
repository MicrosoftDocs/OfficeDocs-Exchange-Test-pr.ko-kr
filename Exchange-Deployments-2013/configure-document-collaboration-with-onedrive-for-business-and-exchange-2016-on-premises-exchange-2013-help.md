---
title: '비즈니스용 OneDrive 및 2016 Exchange 온-프레미스로 최신 첨부 파일 구성: Exchange 2013 Help'
TOCTitle: 비즈니스용 OneDrive 및 2016 Exchange 온-프레미스로 최신 첨부 파일 구성
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70319584
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 비즈니스용 OneDrive 및 2016 Exchange 온-프레미스로 최신 첨부 파일 구성

 

_<strong>적용 대상:</strong>Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2016-12-09_

**요약:** 온-프레미스 Exchange Server 2016 사용자가 하이브리드 구성에서 비즈니스용 OneDrive 및 SharePoint Online을 통해 문서 공동 작업을 수행하도록 하는 방법입니다.

최근에 Office 365에서 새로운 첨부 파일 옵션을 사용할 수 있게 되었습니다. Exchange 2016에서 *문서 공동 작업*이라는 이 옵션을 사용하여 온-프레미스 사용자는 비즈니스용 OneDrive에 저장된 첨부 파일을 웹용 Outlook에 직접 통합할 수 있습니다.


> [!NOTE]
> Exchange Server 2016 출시부터 Outlook Web App을 웹용 Outlook이라고 합니다.



기존에 사용자는 파일을 메시지에 첨부하여 다른 사람에게 보냅니다. 한 명 이상의 받는 사람이 파일의 사본을 변경하게 되면 결과적으로 모든 사본을 특정 시점에 병합해야 합니다. 또한 이러한 첨부 파일은 각 사용자의 사서함 저장 공간을 차지합니다. 문서 공동 작업을 사용하면 사용자는 대신에 비즈니스용 OneDrive 계정에 저장된 파일에 링크를 삽입하여 같은 원본 위치에 있는 여러 사람들이 추가 저장소 없이도 파일을 편집할 수 있도록 할 수 있습니다.

Exchange 2016 환경이 문서 공동 작업에 맞게 적절히 구성되기 전에는 웹용 Outlook 사용자의 기본 첨부 파일 대화 상자가 다음과 같습니다.

![일반 첨부 파일 대화 상자](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "일반 첨부 파일 대화 상자")

아래 지침에 따라 사용자 환경을 구성하면 웹용 Outlook 첨부 파일 대화 상자는 다음과 같습니다.

![사용하는 최신 첨부 파일이 있는 첨부 파일 대화 상자](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "사용하는 최신 첨부 파일이 있는 첨부 파일 대화 상자")

조직에 온-프레미스 사서함이 있고 Office 365에 비즈니스용 OneDrive 계정이 있는 사용자는 최신 첨부 방법을 사용하여 비즈니스용 OneDrive에 저장된 문서를 여러 받는 사람과 공유할 수 있습니다. 받는 사람의 위치(온-프레미스 및 온라인)는 중요하지 않습니다.

하이브리드 배포에 대한 자세한 내용은 [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 검토하고, 하이브리드 배포 구성의 영향을 받게 될 영역을 파악합니다.

  - [하이브리드 배포 필수 구성 요소](hybrid-deployment-prerequisites-exchange-2013-help.md)에 설명된 모든 하이브리드 배포 요구 사항을 검토하고 완료합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](https://technet.microsoft.com/ko-kr/library/jj150484\(v=exchg.150\))을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 하이브리드 환경에서 문서 공동 작업을 수행할 수 있게 Exchange 2016 구성

다음 필수 단계를 완료한 후 이어지는 절차에 따라 문서 공동 작업을 사용하도록 설정합니다.

**필수 구성 요소**

  - [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)(HCW)를 사용하여 Exchange 하이브리드 환경을 구성합니다.

  - Exchange 2016을 온-프레미스 조직에 설치해야 합니다. Exchange 2016은 이전 버전의 Exchange와 함께 사용할 수 있지만 문서 공동 작업은 Exchange 2016의 사서함 서버에만 작동됩니다.

  - 모든 사용자가 동기화된 상태로 인증 서버를 설치해야 합니다. [Get-AuthServer](https://technet.microsoft.com/ko-kr/library/jj218613\(v=exchg.150\)) cmdlet을 사용하여 인증 서버를 찾을 수 있습니다. Exchange 2016 서버의 HCW를 사용하여 필요한 OAuth 구성을 수행하는 것이 좋습니다.
    

    > [!IMPORTANT]
    > Exchange 2016과 Office 365 간에 OAuth가 제대로 구성되어야 합니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/dn594521(v=exchg.150)">Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성</A>을 참조하세요.



  - 사용자에게 적절한 라이선스가 있어야 합니다. 비즈니스용 OneDrive 계정이 있는 사용자는 SharePoint Online 또는 비즈니스용 OneDrive에 대한 사용이 허가되어야 합니다. Office 365 포털에서 사용자를 선택하고 **편집** 단추를 선택하여 사용자의 라이선스를 확인할 수 있습니다.
    

    > [!NOTE]
    > 자세한 내용은 <A href="http://go.microsoft.com/fwlink/p/?linkid=627455">Office 365에서 비즈니스용 OneDrive 설정</A>을 참조하세요.



다음 단계를 수행하십시오.

1.  비즈니스용 OneDrive 호스트 URL을 설정하는 기본 웹용 Outlook 사서함 정책을 구성합니다.
    

    > [!NOTE]
    > Office 365 SharePoint Online 테넌트 관리로 이동하여 비즈니스용 OneDrive 호스트 URL을 검색할 수 있습니다. 예를 들어 https://contoso-my.sharepoint.com은 Contoso의 O365 테넌트에 있는 내 사이트 호스트 URL입니다.<BR>Exchange 2016에 제공되는 웹용 Outlook 사서함 정책을 "기본 정책"이라고 하지만, 기본 정책으로 만들거나 사서함에 직접 할당하지 않으면 자동으로 사서함에 적용되지 않습니다.

    
    다음 예제를 참조하여 Exchange 관리 셸를 통해 기본 웹용 Outlook 사서함 정책에서 내부 및 외부 내 사이트 URL을 구성합니다.
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  다음에는 방금 구성한 정책을 기본 정책으로 설정하여 모든 사서함에 적용되도록 하거나 개별 사용자에게 정책을 할당합니다.
    
    정책을 기본 웹용 Outlook 사서함 정책으로 지정하려면 Exchange 관리 셸에서 다음 명령을 입력합니다.
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    각 사용자의 사서함에 정책을 할당하려면 Exchange 관리 셸에서 다음 명령을 입력합니다.
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (선택 사항) 각 Exchange 2016 서버에서 **OWAApplicationPool**을 다시 시작하여 구성을 즉시 적용합니다. 이 명령을 실행하지 않으면 Exchange 2016 서버에서 업데이트된 사서함 정책을 적용하는 데 몇 분 정도 소요됩니다. Exchange 관리 셸에서 다음을 실행합니다.
    
        Restart-WebAppPool MSExchangeOWAAppPool

일단 구성되면 웹용 Outlook 사용자에게는 메시지에 적용하려는 첨부 파일 형식(기존 또는 최신) 선택 옵션이 제공됩니다.

![OneDrive에 공유 또는 첨부 파일로 보내기가 있는 첨부 파일 옵션 대화 상자](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "OneDrive에 공유 또는 첨부 파일로 보내기가 있는 첨부 파일 옵션 대화 상자")


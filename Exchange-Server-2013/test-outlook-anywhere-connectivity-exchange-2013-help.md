---
title: '외부에서 Outlook 사용 연결 테스트: Exchange 2013 Help'
TOCTitle: 외부에서 Outlook 사용 연결 테스트
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50555940
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 외부에서 Outlook 사용 연결 테스트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

셸 또는 ExRCA(Exchange Remote Connectivity Analyzer)를 사용하여 종단 간 클라이언트 Outlook Anywhere 연결을 테스트할 수 있습니다. 여기에는 자동 검색 서비스를 통한 연결 테스트, 사용자 프로필 만들기, 사용자 사서함 로그인 등이 포함됩니다. 필요한 모든 값은 자동 검색 서비스에서 검색됩니다.

Outlook Anywhere과 관련된 추가 관리 작업에 대한 자세한 내용은 [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Anywhere" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 외부에서 Outlook 사용 연결 테스트

셸을 사용하여 Outlook Anywhere 연결을 테스트하려면 **Test-OutlookConnectivity** cmdlet을 사용합니다.

다음 명령을 실행합니다.

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com


> [!NOTE]
> <EM>OutlookMailboxDeepTestProbe</EM> 매개 변수 값은 사서함 서버에서 연결을 테스트합니다. 클라이언트 액세스 서버에서 연결을 테스트하려면<EM>ProbeIdentity</EM> 매개 변수 값에 <EM>OutlookMailboxCTPProbe</EM>를 사용하십시오.



## Exchange Remote Connectivity Analyzer를 사용하여 Outlook Anywhere 연결 테스트

Exchange 원격 연결 분석기 (ExRCA)는 다양 한 Exchange 프로토콜와의 연결을 테스트할 웹 기반 도구입니다. ExRCA [여기](https://go.microsoft.com/fwlink/p/?linkid=167905)에 액세스할 수 있습니다.

1.  ExRCA 웹 사이트의 **Microsoft Office Outlook 연결 테스트**에서 **Outlook Anywhere**를 선택하고 페이지 아래쪽에 있는 다음을 선택합니다.

2.  다음 화면에 전자 메일 주소, 도메인 및 사용자 이름, 비밀번호를 비롯하여 필요한 정보를 입력합니다.

3.  자동 검색을 사용하여 서버 설정을 검색할지, 아니면 수동으로 서버 설정을 지정할지 선택합니다.

4.  고지 사항에 동의하고 확인 코드를 입력한 다음 **확인**을 선택합니다.

5.  **테스트 수행**을 선택합니다.

## 작동 여부는 어떻게 확인합니까?

ExRCA 테스트가 완료되면 웹 페이지에 출력이 표시됩니다. 오류가 있으면 모두 나열됩니다.


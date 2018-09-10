---
title: 'Exchange UM 문제해결 도구를 사용 하 여 자격 증명 설정: Exchange 2013 Help'
TOCTitle: Exchange UM 문제해결 도구를 사용 하 여 자격 증명 설정
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56270326
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange UM 문제해결 도구를 사용 하 여 자격 증명 설정

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2010 UM 문제 해결 도구는 **Test-ExchangeUMCallFlow**라는 Exchange 관리 셸 cmdlet입니다. 이 cmdlet을 사용하여 전화 응답 시나리오와 관련된 구성 오류를 진단하고 온-프레미스 및 크로스-프레미스 Microsoft Exchange Server 2010 SP1(서비스 팩 1) 이상의 UM 배포에서 음성 사서함이 제대로 작동하는지 테스트할 수 있습니다. 이 cmdlet은 Microsoft Office Microsoft Lync Server 2010 이상이 배포된 환경 또는 Vo IP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)가 포함된 UM 배포 환경에서 사용할 수 있습니다.

기본적으로 UM 문제 해결 도구를 실행 중인 경우 이 도구는 컴퓨터에 로그온할 때 사용되는 자격 증명을 사용합니다. 사용되는 자격 증명은 발신자에 대해 지정된 자격 증명입니다. `SIPClient` 모드에서 UM 문제 해결 도구를 실행 중인 경우 사용할 자격 증명을 설정하거나 지정해야 합니다. 하지만 `Gateway` 모드에서 UM 문제 해결 도구를 실행 중인 경우에는 자격 증명을 설정할 필요가 없습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "UM 서버" 또는 "UM 서비스? [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 의 항목입니다.

  - Exchange 2010 또는 Exchange 2013 조직에는 다음 요구 사항을 만족 하는지 확인 합니다.
    
      - UM 다이얼 플랜이 만들어졌습니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)를 참조하십시오.
    
      - UM 사서함 정책이 만들어졌습니다. 자세한 단계는 [UM 사서함 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)를 참조하세요.
    
      - UM IP 게이트웨이가 만들어졌습니다. 자세한 단계는 [UM IP 게이트웨이 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)를 참조하십시오.
    
      - Exchange 2010 UM 서버를 UM 다이얼 플랜에 추가 되었습니다. Lync Server와 Exchange 2013을 사용 중인 경우 SIP URI 다이얼 플랜에 모든 클라이언트 액세스 서버와 사서함 서버를 추가 합니다. 자세한 단계는 [다이얼 플랜에 UM 서버 추가](https://go.microsoft.com/fwlink/p/?linkid=313051) 또는 [SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)를 참조 하십시오.

  - UM 문제 해결 도구를 설치합니다. 자세한 단계는 [Exchange UM 문제 해결 도구 설치](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)를 참조하십시오.
    

    > [!IMPORTANT]
    > 사용할 UM 문제해결 도구 <CODE>SIPClient</CODE> 모드에서를 하는 경우 여러 다른 Office Communications Server 2007 R2 또는 Microsoft Lync Server 요구 사항 및 필수 구성 요소가 있습니다. 자세한 내용은 참조 <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">검사 목록: Office Communications Server 2007 R2 배포 및 Exchange 2010 통합 메시징</A> 또는 <A href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">검사 목록: Lync Server와 Exchange 2013 UM 통합</A>합니다.



  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## UM 문제 해결 도구에서 사용할 자격 증명 설정

1.  **시작** 메뉴에서 **Microsoft Exchange 2010 UM 문제 해결 도구**를 엽니다.

2.  **Microsoft Exchange 2010 UM 문제 해결 도구** 창의 프롬프트에 다음을 입력하고 Enter 키를 누릅니다.
    
        $cred=Get-Credential

3.  **Windows PowerShell 자격 증명 요청** 창에서 도메인\\사용자 이름과 암호를 입력한 다음 **확인**을 클릭합니다.

4.  **Microsoft Exchange 2010 UM 문제 해결 도구** 창에서 호출 흐름 테스트에 필요한 cmdlet 매개 변수를 지정합니다. 예를 들면 다음과 같습니다.
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred


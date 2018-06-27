---
title: 'Windows 7 또는 Windows 8에서 Exchange UM 문제 해결 도구 실행: Exchange 2013 Help'
TOCTitle: Windows 7 또는 Windows 8에서 Exchange UM 문제 해결 도구 실행
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56270331
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows 7 또는 Windows 8에서 Exchange UM 문제 해결 도구 실행

 

_**적용 대상:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange 2010 UM 문제 해결 도구는 **Test-ExchangeUMCallFlow**라는 Exchange 관리 셸 cmdlet입니다. 이 cmdlet을 사용하여 전화 응답 시나리오와 관련된 구성 오류를 진단하고 온-프레미스 및 크로스-프레미스 Microsoft Exchange Server 2010 SP1(서비스 팩 1) 이상의 UM 배포에서 음성 사서함이 제대로 작동하는지 테스트할 수 있습니다. 이 cmdlet은 Microsoft Office Microsoft Lync Server 2010 이상이 배포된 환경 또는 Vo IP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)가 포함된 UM 배포 환경에서 사용할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "UM 서버" 또는 "UM 서비스? [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 의 항목입니다.

  - Exchange 2010 또는 Exchange 2013 조직에는 다음 요구 사항을 만족 하는지 확인 합니다.
    
      - UM 다이얼 플랜이 만들어졌습니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.
    
      - UM 사서함 정책이 만들어졌습니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.
    
      - UM IP 게이트웨이가 만들어졌습니다. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)를 참조하십시오.
    
      - Exchange 2010 UM 서버를 UM 다이얼 플랜에 추가 되었습니다. Exchange 2013 Lync server를 사용 하는 경우 SIP URI 다이얼 플랜에 모든 클라이언트 액세스 서버와 사서함 서버를 추가 합니다. 자세한 단계는 [다이얼 플랜에 UM 서버 추가](https://go.microsoft.com/fwlink/p/?linkid=313051) 또는 [SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)를 참조 하십시오.

  - 경우 Exchange 2010 SP1와 로컬 UM 서버에서 UM 문제해결 도구를 실행 중인 나 아래에 나열 된 모든 필수 구성 요소를 설치 하려면 필요 하지 수 나중에 또는 Exchange 2013 사서함 서버의 합니다. 이미 설치 되었을 수도 UM 서버 역할은 함께 합니다. 그러나 UM 서버 역할을 실행 하는 서버가 아닌 다른 64 비트 컴퓨터에서 UM 문제해결 도구를 설치 하는 경우에 다음 구성 요소를 설치 해야 합니다.
    
      - Microsoft .NET Framework 3.5 서비스 팩 1 (SP1). [Microsoft.NET Framework 3.5 서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=152380)를 참조 하십시오.
    
      - Windows Vista 또는 Windows Server 2008 컴퓨터에서 도구를 실행 하는 경우 [Windows Server 2008 x64 및 Windows Vista x64, 용 Microsoft.NET Framework 3.5 제품군 업데이트](https://go.microsoft.com/fwlink/p/?linkid=178998)를 참조 하십시오.
    
      - WinRM(Windows 원격 관리) 2.0 및 Windows PowerShell V2(Windows6.0-KB968930.msu). Microsoft 기술 자료 문서 968930, [Windows 관리 프레임워크 핵심 패키지(Windows PowerShell 2.0 및 WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930)를 참조하세요.
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi). [Unified Communications Managed API 2.0, Core Runtime (64 비트)](https://go.microsoft.com/fwlink/p/?linkid=198175)를 참조 하십시오.

  - UM 문제 해결 도구를 다운로드하여 설치합니다.
    
      - Microsoft 다운로드 센터에서 [통합 메시징 문제해결 도구](https://go.microsoft.com/fwlink/p/?linkid=182625) 를 다운로드 합니다.
    
      - 도구를 설치합니다. 자세한 내용은 [Exchange UM 문제 해결 도구 설치](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)를 참조하십시오.
        

        > [!IMPORTANT]
        > 사용할 UM 문제해결 도구 <CODE>SIPClient</CODE> 모드에서를 하는 경우 여러 다른 Office Communications Server 2007 R2 또는 Microsoft Lync 서버 요구 사항 및 필수 구성 요소를 충족 해야 있습니다. 자세한 내용은 참조 <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">검사 목록: Office Communications Server 2007 R2 배포 및 Exchange 2010 통합 메시징</A>합니다.



  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Windows Vista, Windows 7 또는 Windows 8에서 UM 문제 해결 도구 실행

1.  **시작** \> **모든 프로그램** \> **보조프로그램** \> **Windows PowerShell**을 클릭합니다.

2.  **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 팝업 메뉴에서 **관리자 권한으로 실행**을 선택합니다.

3.  Windows PowerShell 명령 프롬프트에서 UM 문제 해결 도구가 설치된 폴더로 이동하여 다음을 실행합니다.
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  UM 문제 해결 도구를 Windows Vista, Windows 7 또는 Windows 8에서 실행하는 경우 Windows PowerShell 명령 프롬프트에서 다음을 실행합니다.
    
        Set-ExecutionPolicy RemoteSigned

5.  **시작** 메뉴에서 **Microsoft Exchange 2010 UM 문제 해결 도구**를 엽니다.

6.  **Microsoft Exchange 2010 UM 문제 해결 도구** 창의 프롬프트에 다음을 입력하고 Enter 키를 누릅니다.
    
        $cred=Get-Credential

7.  **Windows PowerShell 자격 증명 요청** 창에서 도메인\\사용자 이름과 암호를 입력한 다음 **확인**을 클릭합니다.

8.  **Microsoft Exchange 2010 UM 문제 해결 도구** 창에서 호출 흐름 테스트에 필요한 cmdlet 매개 변수를 지정합니다. 예를 들면 다음과 같습니다.
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred


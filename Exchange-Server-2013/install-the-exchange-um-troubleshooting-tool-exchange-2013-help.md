---
title: 'Exchange UM 문제 해결 도구 설치: Exchange 2013 Help'
TOCTitle: Exchange UM 문제 해결 도구 설치
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56270330
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange UM 문제 해결 도구 설치

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2010 UM 문제 해결 도구는 **Test-ExchangeUMCallFlow**라는 Exchange 관리 셸 cmdlet입니다. 이 cmdlet을 사용하여 전화 응답 시나리오와 관련된 구성 오류를 진단하고 온-프레미스 및 크로스-프레미스 Microsoft Exchange Server 2010 SP1(서비스 팩 1) 이상의 UM 배포에서 음성 사서함이 제대로 작동하는지 테스트할 수 있습니다. 이 cmdlet은 Microsoft Office Microsoft Lync Server 2010 이상이 배포된 환경 또는 Vo IP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)가 포함된 UM 배포 환경에서 사용할 수 있습니다.

UM 문제 해결 도구는 로컬 통합 메시징 서버, Exchange 2013 사서함 서버 또는 다른 64비트 컴퓨터에 설치할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - UM 문제 해결 도구를 설치하려면 Windows Vista, Windows 7, Windows 8, 64비트 버전 Windows Server 2008 또는 Windows Server 2012 이상을 실행하는 컴퓨터에 다음 구성 요소가 설치되어 있어야 합니다.
    
      - Microsoft .NET Framework 3.5 서비스 팩 1 (SP1) [Microsoft.NET Framework 3.5 서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=152380)를 참조 하십시오.
    
      - Windows Vista 또는 Windows Server 2008 컴퓨터에서 도구를 실행 하는 경우 [Windows Server 2008 x64 및 Windows Vista x64, 용 Microsoft.NET Framework 3.5 제품군 업데이트](https://go.microsoft.com/fwlink/p/?linkid=178998)를 참조 하십시오.
    
      - WinRM(Windows 원격 관리) 2.0 및 Windows PowerShell V2(Windows6.0-KB968930.msu). Microsoft 기술 자료 문서 968930, [Windows 관리 프레임워크 핵심 패키지(Windows PowerShell 2.0 및 WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930)를 참조하세요.
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi). [Unified Communications Managed API 2.0, Core Runtime (64 비트)](https://go.microsoft.com/fwlink/p/?linkid=198175)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## UM 문제 해결 도구 설치

1.  [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=182625)에서 통합 메시징 문제해결 도구를 다운로드 하 고 MicrosoftExchange2010UMTroubleshootingTool.msi 설치 폴더를 두번클릭 합니다.

2.  **Microsoft Exchange 2010 UM 문제 해결 도구 설치 마법사 시작** 페이지에서 **다음**를 클릭합니다.

3.  **최종 사용자 사용권 계약** 페이지에서 소프트웨어 사용 조건을 검토하고 동의하면 **사용권 계약에 동의함**를 클릭하고 **다음**를 클릭합니다.

4.  **설치 폴더 선택** 페이지에서 설치 폴더의 경로를 확인하고 **다음**를 클릭합니다.

5.  **설치 확인** 페이지에서 **다음**를 클릭하여 설치를 시작합니다.

6.  **설치 완료** 페이지에서 **닫기**를 클릭합니다.


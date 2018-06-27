---
title: '테스트 및 UM 문제해결 도구와 문제해결: Exchange 2013 Help'
TOCTitle: 테스트 및 UM 문제해결 도구와 문제해결
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56270323
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 테스트 및 UM 문제해결 도구와 문제해결

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange 2010 UM 문제 해결 도구는 **Test-ExchangeUMCallFlow**라는 Exchange 관리 셸 cmdlet입니다. 이 cmdlet을 사용하여 전화 응답 시나리오와 관련된 구성 오류를 진단하고 온-프레미스 및 크로스-프레미스 Microsoft Exchange Server 2010 SP1(서비스 팩 1) 이상의 UM 배포에서 음성 사서함이 제대로 작동하는지 테스트할 수 있습니다. 이 cmdlet은 Microsoft Office Microsoft Lync Server 2010 이상이 배포된 환경 또는 Vo IP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)가 포함된 UM 배포 환경에서 사용할 수 있습니다.

## 개요

이 cmdlet는 통화를 에뮬레이션 하 고 일련의 온-프레미스 관리자가 전화 통신 장비, Exchange 2010 SP1 또는 이후 통합 메시징 설정을 및 온-프레미스 및 Exchange 2010 s p 1의 크로스-프레미스 배포 또는 이후 통합 메시징 간의 연결 문제가 구성 오류를 식별 하는 데 도움이 되는 진단 테스트를 실행 합니다.

여기에서는 cmdlet을 실행할 때 검색된 문제의 원인과 가능한 해결 방법을 알려줍니다. 또한 지터나 평균 패킷 손실 같이 네트워크 연결과 관련된 오디오 품질 문제를 진단하기 위한 일반 오디오 품질 메트릭을 출력합니다. **Test-ExchangeUMCallFlow** cmdlet은 `Secured`, `SIP Secured` 및 `Unsecured` 호출 시 UM 구성 요소 테스트를 지원하며, `Gateway` 또는 `SIPClient` 모드에서 실행 가능합니다.

UM 문제해결 도구를 실행 하는 경우 기본적으로 컴퓨터에 로그온 할 때 사용 되는 자격 증명을 사용 합니다. 사용 되는 자격 증명은 발신자에 대해 지정 된 것입니다. 설정 하거나 `SIPClient` 모드에서 UM 문제해결 도구를 실행 하는 경우 사용할 자격 증명을 지정 해야 합니다. 그러나 `Gateway` 모드에서 UM 문제해결 도구를 실행할 때 자격 증명을 설정할 필요가 없습니다. 사용할 UM 문제해결 도구 `SIPClient` 모드로, 여러 다른 Office Communications Server 2007 R2 또는 Lync 서버 요구 사항 및 필수 구성 요소 충족 해야 합니다. 자세한 내용은 참조 [검사 목록: Office Communications Server 2007 R2 배포 및 Exchange 2010 통합 메시징](https://go.microsoft.com/fwlink/p/?linkid=311961) 또는 [검사 목록: Lync Server와 Exchange 2013 UM 통합](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)합니다.


> [!IMPORTANT]
> Microsoft Exchange 2013 또는 Microsoft Exchange Server 2010 통합 메시징 서버를 Exchange 2010 서비스 팩 1 (SP1)이 설치 되어 있는의 음성 메일 기능을 테스트 하는 <STRONG>Test-ExchangeUMCallFlow</STRONG> cmdlet은 사용 해야 합니다.



**Test-ExchangeUMCallFlow** cmdlet은 로컬 Exchange 2010 통합 메시징 서버, Exchange 2013 사서함 서버 또는 다음 운영 체제를 실행하는 다른 64비트 컴퓨터에 설치할 수 있습니다.

  - Windows 7 또는 Windows 8 운영 체제

  - Windows Server 2008 또는 Windows Server 2008 R2 운영 체제

  - Windows Server 2012 또는 Windows Server 2012 R2 운영 체제

**Test-ExchangeUMCallFlow** cmdlet은 다음의 구성 요소를 Windows 7, Windows 8, Windows Server 2008 또는 Windows Server 2012 64비트 컴퓨터에 설치한 후에 cmdlet을 설치해야 합니다.

  - Microsoft .NET Framework 3.5 서비스 팩 1 (SP1). 서비스 팩을 다운로드 하려면 [Microsoft.NET Framework 3.5 서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=152380)를 참조 하십시오.

  - Microsoft .NET Framework 3.5 제품군 업데이트 Windows Vista x64 및 Windows Server 2008 x64 Windows Vista 또는 Windows Server 2008 컴퓨터에서 도구를 실행 하는 경우를 업데이트 합니다. 업데이트를 다운로드 하려면 [Windows Server 2008 x64 및 Windows Vista x64, 용 Microsoft.NET Framework 3.5 제품군 업데이트](https://go.microsoft.com/fwlink/p/?linkid=178998)를 참조 하십시오.

  - Windows Remote Management(WinRM) 2.0 및 Windows PowerShell V2(Windows6.0-KB968930.msu). 자세한 내용은 Microsoft 기술 자료 문서 968930, [Windows 관리 프레임워크 핵심 패키지(Windows PowerShell 2.0 및 WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930)를 참조하세요.

  - Unified Communications Managed AP1 2.0, Core Runtime (64 비트)입니다. UcmaRuntimeWebDownloadX64.msi 프로그램 파일을 다운로드 하려면 [Unified Communications Managed API 2.0, Core Runtime (64 비트)](https://go.microsoft.com/fwlink/p/?linkid=198175)를 참조 하십시오.

**Test-ExchangeUMCallFlow** cmdlet은 Exchange 2010 SP1 DVD, Exchange 2010 SP1 전용 다운로드 또는 Exchange 2013 설치 미디어;에 포함 되지 않습니다. 그러나 cmdlet은 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=182625)에서 다운로드할 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Test-ExchangeUMCallFlow](https://technet.microsoft.com/ko-kr/library/ff630913\(v=exchg.150\))를 참조하세요.


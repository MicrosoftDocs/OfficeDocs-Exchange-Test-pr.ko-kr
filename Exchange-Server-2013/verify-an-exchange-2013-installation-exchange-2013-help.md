---
title: 'Exchange 2013 설치를 확인 합니다.: Exchange 2013 Help'
TOCTitle: Exchange 2013 설치를 확인 합니다.
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50484602
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 설치를 확인 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Microsoft Exchange Server 2013 를 설치한 후에 **Get-ExchangeServer** cmdlet을 실행 하 고 설치 로그 파일을 검토 하 여 설치를 확인 하는 것이 좋습니다. 설치 프로세스가 실패 또는 설치 중에 오류가 발생 하는 경우에 문제의 원인을 추적 하기가 설치 로그 파일을 사용할 수 있습니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

## Get-ExchangeServer 실행

Exchange 2013이 설치되었는지 확인하려면 Exchange 관리 셸에서 **Get-ExchangeServer** cmdlet을 실행합니다. 이 cmdlet을 실행하면 지정된 서버에 설치되어 있는 모든 Exchange 2013 서버 역할의 목록이 표시됩니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-ExchangeServer](https://technet.microsoft.com/ko-kr/library/bb123873\(v=exchg.150\))를 참조하세요.

## 설치 로그 파일 검토

설치 프로세서 중에 만든 설치 로그 파일을 검토하여 Exchange 2013의 설치 및 구성에 대해 자세히 알아볼 수도 있습니다.

설치 중에 Exchange 설치 프로그램은 Exchange R2 SP1(서비스 팩 1) 및 Windows Server 2012가 실행되는 컴퓨터에서 **이벤트 뷰어**의 **응용 프로그램** 로그에 있는 이벤트를 기록합니다. 이에 따라 **응용 프로그램** 로그를 검토하고 Windows Server 2008 설치와 관련해서 경고나 오류 메시지가 없는지 확인합니다. 이러한 로그 파일에는 Exchange 2013 설치 중에 시스템이 수행하는 각 작업에 대한 기록과 발생했을 수도 있는 오류 정보가 저장됩니다. 기본적으로 로깅 방법은 `Verbose`로 설정됩니다. 설치된 각 서버 역할에 대한 정보가 제공됩니다.

*\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log에서 설치 로그 파일을 찾을 수 있습니다. *\<system drive\>* 변수는 운영 체제가 설치되어 있는 드라이브의 루트 디렉터리를 나타냅니다.

설치 로그 파일은 Exchange 2013 설치 및 구성 중에 수행되는 모든 작업의 진행을 추적합니다. 이 파일에는 설치를 시작하기 전에 수행되는 선행 조건 및 시스템 준비 검사 상태, 응용 프로그램 설치 진행률 및 시스템 구성 변경 내용에 대한 정보가 들어 있습니다. 서버 역할이 예상대로 설치되었는지 확인하려면 이 로그 파일을 검토하십시오.

오류를 검색하여 설치 로그 파일을 검토하는 것이 좋습니다. 오류가 발생했음을 나타내는 항목을 찾으면 관련 텍스트를 읽어 오류의 원인을 확인할 수 있습니다.


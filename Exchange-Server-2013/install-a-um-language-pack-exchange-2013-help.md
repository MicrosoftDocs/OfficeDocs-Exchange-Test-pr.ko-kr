---
title: 'UM 언어 팩 설치: Exchange 2013 Help'
TOCTitle: UM 언어 팩 설치
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50484479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 언어 팩 설치

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

언어를 UM 다이얼 플랜 또는 UM 자동 전화 교환에서 통합 메시징을 사용할 수 있는 언어의 목록에서 사용할 수 있도록 하려면 먼저 적절 한 UM 언어팩을 설치 해야 합니다. 특정 언어 관련 자동 압축풀기 실행 파일 또는 **setup.exe /AddUmLanguagePack** 명령을 사용 하 여 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버에 언어팩을 설치 합니다. UM 언어팩을 설치 하기 전에 먼저 다운로드 해야 사서함 서버에서 로컬 폴더에 있습니다. [Exchange Server 2013 UM 언어팩](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 UM 언어팩을 다운로드할 수 있습니다. 각 언어에 대 한 별도 실행 파일 방법이 있습니다.

적절 한 UM 언어팩을 설치한 후에 UM 다이얼 플랜 또는 UM 자동 전화 교환의 **일반** 페이지에서 **자동화 된 음성 인터페이스에 대 한 언어** 드롭다운 목록 **설정** 페이지에 드롭다운 목록을 확인 하 여 설치 된 UM 언어팩의 목록은 볼 수 있습니다. UM 다이얼 플랜 및 자동 전화 교환에서 영어 (EN-US) 아닌 언어를 기본 언어를 구성할 수도 있습니다.


> [!WARNING]
> Microsoft Exchange Server 2007 또는 Exchange 2007 서비스 팩 1 (SP1), s p 2에서 또는 SP3 또는 Exchange 2010 서비스 팩 1 SP1, SP2 또는 s p 3에 대 한 UM 언어팩 Exchange 2013 사서함 서버에서 사용할 수 없습니다.



UM 언어와 관련된 추가 작업에 대한 자세한 내용은 [UM 언어, 프롬프트 및 인사말 절차](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5 분입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "사서함 서버 (UM 서비스)" 항목.

  - 사서함 서버는 클라이언트 액세스 서버와 다른 컴퓨터에 설치 되어 있는지 또는 클라이언트 액세스 및 사서함 서버는 동일한 하드웨어 있지 않은지 확인 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## UM 언어 팩 설치 (.exe) 파일을 사용 하 여 UM 언어팩을 설치 하려면

1.  [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 사서함 서버에서 로컬 폴더에 특정 언어 관련 UM 언어 팩 (.exe) 파일을 다운로드 합니다.

2.  UMLanguagePack를 두번클릭 합니다. *\<CultureCode\>.exe* 파일입니다. 예, 독일어 UM 언어팩 UMLanguagePack.de DE.exe 라는 파일을 다운로드 합니다.

3.  
    
    Exchange 2013 설치 마법사의 **사용권 계약** 페이지에서 계약 약관을 읽어 **사용권 계약에 동의** 선택한 후 **다음** 을 클릭 합니다.

4.  
    
    **통합 메시징 언어 팩** 페이지의 **다음 통합 메시징 언어 팩이 설치됩니다.** 창에 올바른 언어가 나와 있는지 확인한 다음 **설치**를 클릭합니다.

5.  **마침**을 클릭하여 UM 언어 팩 설치를 완료합니다.

## Setup.exe를 사용 하 여 UM 언어팩 설치

이 예제에서는 설치 일본어 (JA-JP) UM 사서함 서버에서 D:\\Exchange\\UMLanguagePacks 폴더로 다운로드 된 하는 언어 팩 합니다.

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

이 예제에서는 설치 스페인어 (멕시코) (ES-MX) 및 독일어 (DE-DE) UM 사서함 서버에 있는 D:\\Exchange\\UMLanguagePacks 폴더에 다운로드 한 언어팩 합니다.

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>/IAcceptExchangeServerLicenseTerms 매개 변수를 사용 하지 않으면 다음과 같은 오류를 볼 수 있습니다: Microsoft Exchange Server 2013 무인 설치를 시작 합니다. Microsoft Exchange Server 2013을 설치 하려면 사용 조건에 동의 해야 합니다. 사용권 계약을 읽고, http://go.microsoft.com/fwlink/p/?LinkId=150127를 방문 합니다. 사용권 계약에 동의 하려면를 실행 중인 명령 /IAcceptExchangeServerLicenseTerms 매개 변수를 추가 합니다. 자세한 내용은 설치 프로그램을 실행 /?.</td>
</tr>
</tbody>
</table>


사용 가능한 UM 언어 및 문화권 코드에 대 한 자세한 내용은 [UM 언어, 프롬프트 및 인사말](um-languages-prompts-and-greetings-exchange-2013-help.md)을 참조 하십시오.


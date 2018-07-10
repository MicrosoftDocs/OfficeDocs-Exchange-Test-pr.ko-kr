---
title: 'UM 언어, 프롬프트 및 인사말: Exchange 2013 Help'
TOCTitle: UM 언어, 프롬프트 및 인사말
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50484230
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 언어, 프롬프트 및 인사말

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

언어 팩을 설치 및 구성하여 UM(통합 메시징) 환경에서 여러 언어를 지원할 수 있습니다.

UM 언어 팩을 사용하면 발신자와 Outlook Voice Access 사용자가 여러 언어로 음성 메일 시스템과 상호 작용할 수 있습니다. 사서함 서버에 추가 언어를 설치한 후에는 발신자와 Outlook Voice Access 사용자가 해당 언어로 전자 메일 메시지를 듣고 음성 메일 시스템과 상호 작용할 수 있습니다.

사용자와 발신자가 통합 메시징과 여러 언어로 효율적으로 상호 작용할 수 있도록 UM 언어 팩을 사용하는 몇 가지 주요 구성 요소가 있습니다. 각 UM 언어 팩에는 특정 언어에 대한 TTS(텍스트 음성 변환) 엔진, 사전 녹음 음성 안내, ASR(자동 음성 인식) 및 음성 메일 미리 보기 지원이 포함되어 있습니다. 이 항목에서는 UM 언어 팩, UM 언어 팩을 사용하는 UM 구성 요소, 설치된 후 UM 언어 팩을 사용하여 다른 언어를 사용하도록 UM 다이얼 플랜 및 UM 자동 전화 교환을 구성하는 방법 등에 대해 설명합니다.

Exchange 통합된 메시징 언어팩은 버전별 및 플랫폼별입니다. Exchange Server 2007 이후에 여러 버전에 대 한 UM 언어팩을 Exchange 2007, Exchange 2007 SP1, s p 2와 s p 3, Exchange Server 2010, Exchange 2010 SP1 및 SP2 및 Exchange 2013 의 RTM 버전의 RTM 버전을 포함 한 있었습니다. 이 버전의 일부에 대 한 32 비트 및 64 비트 모두 다운로드를 사용할 수 있지만 64 비트 다운로드는 사용할 수 있는 다른 릴리스에 대 한 합니다.

UM 언어 팩의 올바른 버전과 플랫폼을 사서함 서버에 설치해야 합니다. 이전 버전의 Exchange를 실행 중이거나 32비트 플랫폼용으로 설계된 사서함 서버에는 UM 언어 팩을 설치하지 마십시오.

**목차**

Overview of UM language packs

UM language components and features

Voice Mail Preview

Unified Messaging languages

Unified Messaging language packs

UM dial plan languages

UM auto attendant languages

Client language selection process

## UM 언어 팩 개요

통합 메시징 언어 팩을 사용하면 발신자가 ASR을 사용하거나 음성 메시지가 기록될 경우 사서함 서버가 더 많은 언어로 말하고 인식할 수 있습니다. UM 언어 팩에는 다음이 포함되어 있습니다.

  - UM 언어 팩의 언어로 사전 녹음된 음성 안내. 예: "신호음이 들린 후에 메시지를 녹음하여 주십시오. 녹음이 끝나면 전화를 끊거나 우물 정자를 눌러 다른 옵션을 사용할 수 있습니다."

  - 사서함 서버가 디렉터리에서 지정된 사용자의 이름을 조회하는 데 사용하는 UM 언어 팩 언어의 문법 파일

  - 발신자에게 UM 언어 팩 언어로 콘텐츠(전자 메일, 일정, 연락처 정보 등)를 읽어주기 위한 TTS(텍스트 음성 변환) 번역

  - 발신자가 UM 언어 팩 언어로 VUI(음성 사용자 인터페이스)를 사용하여 UM과 상호 작용할 수 있도록 하는 ASR(자동 음성 인식) 지원

  - 사용자가 Outlook 또는 Outlook Web App 등, 지원되는 전자 메일 클라이언트에서 특정 언어로 된 음성 메일 메시지의 텍스트 사본을 읽을 수 있도록 하는 음성 메일 미리 보기 지원

UM 언어 팩은 사전 녹음 음성 안내와 특정 언어에 대한 TTS 변환 지원을 제공하며 경우에 따라 ASR 지원도 제공합니다. 다국어 환경에서는 일부 발신자가 다른 언어로 음성 안내를 받기를 원하거나 여러 언어로 전자 메일을 수신하기 때문에 추가 UM 언어 팩을 설치해야 합니다. 사서함 서버에서 여러 언어가 포함된 전자 메일 메시지를 읽을 수 있도록 지원하려면 여러 UM 언어 팩을 설치해야 합니다. 이는 읽으려는 메시지의 텍스트를 기반으로 선택할 언어를 TTS 변환 시스템에 알려야 하기 때문입니다. 통합 메시징 언어 팩이 설치되어 있지 않은 경우 사용자에게 전자 메일 메시지를 읽어줄 때 앞뒤가 맞지 않고 알아 들을 수 없게 됩니다. 적절한 언어 팩을 설치하면 TTS 엔진이 올바른 언어를 사용하여 Outlook Voice Access 사용자에 대한 전자 메일 및 일정 항목을 읽고 통합 메시징에 대한 언어별 사전 녹음 음성 안내도 제공할 수 있습니다. 경우에 따라 ASR 지원이 제공될 수도 있습니다.


> [!NOTE]
> TTS 엔진은 텍스트를 음성으로 변환하지만 음성을 텍스트로 변환하지는 않습니다. UM 사용 가능 사용자는 음성 파일이 첨부된 전자 메일 메시지를 다른 사용자에게 보낼 수 있지만 텍스트로 전자 메일 메시지를 작성하여 다른 사용자에게 보낼 수는 없습니다.



언어 팩을 설치할 때 설치 프로그램은 다음을 수행합니다.

1.  UM 다이얼 플랜 및 자동 전화 교환을 구성하는 데 사용되는 언어 프롬프트를 복사합니다.

2.  Outlook Voice Access 사용자가 받은 편지함에 액세스할 때 TTS 엔진에서 메시지를 읽을 수 있도록 합니다.

3.  설치된 언어의 음성 사용 가능 UM 다이얼 플랜 및 자동 전화 교환에 대해 ASR을 사용하도록 설정합니다.

4.  다른 언어로 된 클라이언트에서 음성 사서함 미리 보기를 사용할 수 있도록 합니다.

**Setup.exe** 명령을 사용 하 여 또는 [Exchange Server 2013 UM 언어팩](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 UM 언어팩을 다운로드 한 후 *\<UMLanguagePack\>*.exe 설치 프로그램을 실행 하 여 UM 언어팩을 추가할 수 있습니다. 그러나 Setup.exe 명령을 사용 하 여 UM 언어팩을 제거 해야 합니다. 없는 Exchange 관리 셸 cmdlet에 언어 추가 또는 제거: 사서함 서버에서에서 사용할 수 있는 방법이 있습니다. UM 언어팩을 설치 하는 방법에 대 한 자세한 내용은 [UM 언어 팩 설치](install-a-um-language-pack-exchange-2013-help.md)을 참조 하십시오. UM 언어팩을 제거 하는 방법에 대 한 자세한 내용은 [UM 언어팩 제거](remove-a-um-language-pack-exchange-2013-help.md)을 참조 하십시오.


> [!NOTE]
> 기본적으로 사서함 서버를 설치하면 미국 영어(EN-US)가 설치됩니다. 컴퓨터에서 사서함 서버를 제거해야만 언어를 제거할 수 있습니다.



맨 위로 이동

다음 표에는 현재 사용할 수 있는 통합 메시징 언어 팩 목록이 나와 있습니다. 또한 각 UM 언어 팩의 설치 파일 이름과 UM 언어의 문화권 ID 목록도 나와 있습니다.

### UM 언어 팩 설치 파일 이름 및 문화권 ID

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>언어</th>
<th>국가/지역</th>
<th>문화권 ID</th>
<th>설치 파일 이름</th>
<th>사용 가능 여부</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>카탈로니아어</p></td>
<td><p>스페인</p></td>
<td><p>ca ES</p></td>
<td><p>UMLanguagePack. ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>중국어(홍콩)</p></td>
<td><p>중국</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack. zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>중국어(간체)</p></td>
<td><p>중국</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>중국어(번체)</p></td>
<td><p>대만</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>덴마크어</p></td>
<td><p>덴마크</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>네덜란드어</p></td>
<td><p>네덜란드</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>오스트레일리아</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>영어</p></td>
<td><p>캐나다</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>인도</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack. en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>영어</p></td>
<td><p>영국</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>미국</p></td>
<td><p>en-US</p></td>
<td><p>사서함 서버의 설치에 포함</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>핀란드어</p></td>
<td><p>핀란드</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>프랑스어</p></td>
<td><p>캐나다</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>프랑스어</p></td>
<td><p>프랑스</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>독일어</p></td>
<td><p>독일</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>이탈리아어</p></td>
<td><p>이탈리아</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>일본어</p></td>
<td><p>일본</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>한국</p></td>
<td><p>한국어</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>노르웨이어(복말)</p></td>
<td><p>노르웨이</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>폴란드어</p></td>
<td><p>폴란드</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>포르투갈어</p></td>
<td><p>브라질</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>포르투갈어</p></td>
<td><p>포르투갈</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>러시아어</p></td>
<td><p>러시아</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack. ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>스페인어</p></td>
<td><p>스페인</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>스페인어</p></td>
<td><p>멕시코</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>스웨덴어</p></td>
<td><p>스웨덴</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">사용 가능한 다운로드</a></p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## UM 언어 구성 요소 및 기능

통합 메시징에는 사용자와 발신자가 다국어 음성 메일 시스템과 상호 작용할 수 있도록 하는 여러 주요 구성 요소와 기능이 있습니다. 이러한 구성 요소와 기능이 올바르게 작동하고 발신자가 여러 언어로 시스템과 상호 작용할 수 있으려면 UM 언어 팩을 사서함 서버에 올바르게 설치해야 합니다.

## 사전 녹음 음성 안내

사서함 서버 역할은 기본 오디오 음성 안내 파일 집합과 함께 설치됩니다. 이러한 오디오 파일에는 Outlook 통합 메시징에 사용되는 Exchange Voice Access 메뉴, 음성 사서함 인사말 및 숫자에 대한 녹음이 포함되어 있습니다. 사서함 서버는 내부 및 외부의 수신 전화 발신자에게 오디오 파일을 재생합니다. 오디오 파일의 대부분은 TUI(전화 사용자 인터페이스) 및 Outlook Voice Access 사용자에게 TUI와 VUI(음성 사용자 인터페이스)를 탐색하는 데 필요한 정보를 제공하는 기본 음성 안내로, \<*Program Files*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<언어\>에 있습니다. 발신자의 메뉴 탐색을 돕기 위해 사서함 서버에 사용되는 음성 안내는 대체하거나 변경하면 안 됩니다.

추가 UM 언어 팩이 설치될 경우 해당 언어에 대한 사전 녹음 음성 안내도 설치됩니다. UM 언어 팩이 설치된 후에 UM 다이얼 플랜 및 자동 전화 교환에서 해당 언어에 대한 사전 녹음 음성 안내를 사용할 수 있습니다.

## TTS 언어

통합 메시징은 TTS(텍스트 음성 변환) 엔진을 사용합니다. TTS 기능은 Microsoft 음성 서버 서비스에 의해 제공됩니다. TTS 엔진은 작성된 텍스트를 읽어서 발신자가 들을 수 있는 출력으로 변환합니다. TTS 엔진은 사용자의 사서함에 있는 다음 항목을 읽고 변환합니다.

  - 전자 메일 및 음성 메일 메시지 본문, 제목 및 이름

  - 일정 항목 본문, 제목, 위치 및 이름

  - 개인 연락처 이름

  - 사용자의 기본 음성 사서함 인사말


> [!NOTE]
> 사용자가 개인 설정 음성 사서함 인사말을 녹음하면 이후 TTS 버전의 음성 인사말은 더 이상 사용되지 않습니다.



## 자동 음성 인식

TTS 외에도 통합 메시징에는 ASR 지원이 포함되어 있습니다. ASR 기능은 Microsoft Speech Server 서비스를 통해 제공됩니다. ASR을 사용하면 발신자가 메뉴를 탐색하고 메시지, 개인 연락처 및 일정을 포함하는 개별 사서함의 항목과 상호 작용할 수 있습니다. ASR 지원은 각 언어 팩에 포함됩니다.

맨 위로 이동

## 음성 사서함 미리 보기

또한 UM 언어 팩은 음성 메일 미리 보기를 지원합니다. 지원되는 전자 메일 클라이언트(예: Outlook 또는 Outlook Web App)에서 텍스트 사본을 읽어 음성 메시지를 신속하게 선별합니다.

발신자가 UM 사용 가능 사용자에게 음성 메시지를 남기면 음성 메시지 파일과 이 음성 메일 메시지의 텍스트 사본이 사용자의 사서함으로 전송되는 음성 메시지 본문에 들어갑니다.

모든 UM 언어 팩은 다운로드가 가능한 단일 파일입니다. 이들 언어 팩에는 사전 녹음 음성 안내, 문법 파일, TTS(텍스트 음성 변환) 번역 및 ASR이 포함되어 있습니다. 그러나 음성 사서함 미리 보기는 일부 UM 언어 팩에서만 지원됩니다.

다음 UM 언어 팩에는 음성 사서함 미리 보기를 비롯하여, 모든 구성 요소와 기능에 대한 지원이 포함되어 있습니다.

  - 영어(미국) - (en-US)

  - 영어(캐나다) - (en-CA)

  - 프랑스어(프랑스) - (fr-FR)

  - 이탈리아어 - (it-IT)

  - 폴란드어(pl-PL)

  - 포르투갈어(포르투갈) - (pt-PT)

  - 스페인어(스페인) - (es-ES)

기본적으로 사서함 서버를 설치하면 서버는 지원되는 UM 언어 팩을 설치하고 UM 사용 가능 사용자에게 음성 메일 미리 보기를 전송합니다.

음성 메일 미리 보기 기능을 위한 향상된 녹음 서비스를 지원하는 통합 메시징 음성 메일 미리 보기 파트너가 있습니다. 이러한 파트너는 ASR을 사용하여 만들어진 음성 메일 기록을 수정할 인력을 고용하며, 요구 사항을 준수하여 통합 메시징과의 상호 운용을 보장해야 합니다.

음성 메일 미리 보기를 보내지는지 확인 하는 경우에 사용자에 게 충분히 정확 하지, 수요일를 사람들과 추가 비용이 듭니다 로그인과 [통합 메시징에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=261951) 페이지에 나열 되는 인증 된 음성 메일 미리 보기 파트너 중 하나에 문의할 수 있습니다.

[Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 UM 언어팩을 다운로드할 수 있습니다. 자세한 내용은 [UM 언어 팩 설치](install-a-um-language-pack-exchange-2013-help.md)를 참조 합니다.

## 통합 메시징 언어

통합 메시징에 있는 다국어 기능을 발신자가 사용할 수 있게 하려면 먼저 UM 언어 팩을 설치해야 합니다. 그런 다음 다른 UM 구성 요소를 구성할 수 있습니다.

  - 조직의 사서함 서버에 UM 언어 팩을 설치합니다.

  - 필요한 경우 UM 다이얼 플랜에 대한 기본 언어를 구성합니다. 이렇게 하면 UM 다이얼 플랜과 연결된 Outlook Voice Access 사용자가 사서함에 액세스할 때 새 언어를 사용할 수 있습니다. 그러나 사용자는 Outlook Web App 옵션에서 언어 설정을 구성할 수 있습니다.

  - 자동 전화 교환에서 여러 언어를 사용해야 하면 UM 자동 전화 교환에 언어 설정을 구성합니다. 기본적으로 UM 자동 전화 교환은 UM 다이얼 플랜 언어를 사용합니다. 그러나 이 설정을 변경하여 인증되지 않은 발신자가 조직에 연결하고 UM 자동 전화 교환에 지정된 언어로 자동 전화 교환 메뉴를 탐색하도록 허용할 수 있습니다.

## 통합 메시징 언어 팩

Setup.exe를 사용하여 UM 언어 팩을 사서함 서버에 설치합니다. 새 언어 팩을 설치하고 나면 언어 팩과 연관된 언어가 사용할 수 있는 사용 가능 언어 팩 목록에 추가됩니다. Exchange 관리 셸에서 [Get-UMService](https://technet.microsoft.com/ko-kr/library/jj552407\(v=exchg.150\)) cmdlet을 사용하여 설치한 언어를 볼 수 있습니다.

UM 언어를 설치 하면 팩, TTS 엔진에 의해 사용 되는 파일 및 선택한 언어에 대 한 미리 녹음 된 메시지는 복사 하 고 음성 메일 시스템에 연결 하는 사용자에 대해 사용할 수 있습니다. [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 UM 언어팩을 다운로드할 수 있습니다. 자세한 내용은 [UM 언어 팩 설치](install-a-um-language-pack-exchange-2013-help.md)를 참조 합니다.

## UM 다이얼 플랜 언어

작성된 각 UM 다이얼 플랜에는 기본 언어 설정이 포함되어 있습니다. UM 다이얼 플랜 언어 설정은 Outlook Voice Access 사용자가 자신의 사서함에 액세스할 때 해당 사용자에 대한 표준 오디오 음성 안내를 재생하거나 TTS 변환을 사용해야 하는 경우가 있으므로 필요합니다. 기본 다이얼 플랜 언어를 선택할 필요는 없습니다.

처음 Exchange를 설치할 경우 미국 영어가 기본 언어이며 다이얼 플랜에 사용할 수 있는 유일한 언어 옵션입니다. 사서함 서버에 UM 언어 팩을 설치한 후 다이얼 플랜에 대한 기본 언어를 구성할 때 해당 언어 팩에 연결된 언어가 사용 가능한 옵션으로 나열됩니다.

기본 언어는 발신자에게 중요합니다. Outlook Voice Access 사용자가 음성 메일 시스템에 전화를 걸 때 사용되는 언어는 사용자가 사서함에 처음 로그인할 때 설정된 Outlook Web App의 언어 설정을 기반으로 합니다. 그런 다음 통합 메시징은 Outlook Web App에 설정된 언어를 사용자와 연관된 다이얼 플랜에서 사용 가능한 언어 목록과 비교합니다. 적절한 일치 항목이 없을 경우 기본 UM 다이얼 플랜 언어가 사용됩니다. 예를 들어 다이얼 플랜에 프랑스 사용자만 포함된 경우 다이얼 플랜의 기본 언어 설정을 프랑스어로 변경하고자 할 수 있습니다.

## UM 자동 전화 교환 언어

기본적으로 UM 자동 전화 교환을 만들 때 UM 다이얼 플랜에 연결되기 때문에 UM 자동 전화 교환은 연결된 UM 다이얼 플랜의 기본 언어 설정을 사용합니다. 그러나 UM 자동 전화 교환을 만든 후에 이 설정을 변경할 수 있습니다.

통합 메시징에서 TTS 변환을 사용하거나 표준 오디오 음성 안내를 발신자에게 재생해야 할 수 있으므로 UM 자동 전화 교환 언어 설정이 필요합니다. 통합 메시징은 자동 전화 교환을 위한 사용자 지정 음성 안내의 언어가 자동 전화 교환의 언어 설정과 일치하는지 여부를 검사하지 않습니다. 그러나 자동 전화 교환의 언어 설정이 사용자 지정 음성 안내 언어와 일치하는지 확인하는 것이 좋습니다. 그렇지 않을 경우 발신자가 듣는 언어가 한 언어에서 다른 언어로 전환될 수 있습니다.

또한 발신자에 대한 여러 다른 언어별 자동 전화 교환이 필요한 경우 UM 자동 전화 교환 언어 설정을 변경할 수 있는 기능이 유용합니다.

## 클라이언트 언어 선택 프로세스

UM 언어 팩을 사용하면 발신자 및 Outlook Voice Access 사용자는 여러 언어로 통합 메시징 시스템과 상호 작용할 수 있습니다. 사서함 서버에 추가 언어 팩을 설치하고 나면 발신자 및 Outlook Voice Access 사용자가 전자 메일 메시지를 듣고 음성 메일 시스템과 상호 작용할 수 있으며, Outlook Web App 및 Outlook 2010 이상 버전 사용자는 특정 언어로 된 음성 메일 미리 보기를 사용하여 음성 메시지의 기록을 볼 수 있습니다.

특정 언어를 지원하려면 해당 언어에 대한 UM 클라이언트 언어 팩이 각 사서함 서버에 설치되어야 합니다.

특정 언어에 대한 UM 언어 팩이 설치되어 있지 않아 사용할 수 없을 때 경우에 따라 클라이언트 대체 언어가 사용될 수 있습니다. 일부 언어에서는 대체 UM 클라이언트 언어를 사용할 수 있지만 그 외 언어에서는 대체 언어를 사용할 수 없습니다. 특정 언어에 대해 설치된 UM 언어 팩이 없고 해당 언어에 대한 대체 언어를 사용할 수 없는 경우 en-US(미국 영어)가 사용됩니다.

다음 표에는 클라이언트 언어의 목록 및 사서함 서버에 특정 UM 언어 팩이 설치되어 있지 않은 경우 사용되는 대체 언어의 목록이 나와 있습니다.

### UM에 대한 클라이언트 대체 언어

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>언어</th>
<th>국가/지역</th>
<th>문화권 ID</th>
<th>선택된 첫 번째 언어(설치된 경우)</th>
<th>선택된 두 번째 언어(설치된 경우)</th>
<th>선택된 세 번째 언어(설치된 경우)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>카탈로니아어</p></td>
<td><p>스페인</p></td>
<td><p>ca ES</p></td>
<td><p>ca ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>중국어(홍콩)</p></td>
<td><p>중국</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>중국어(간체)</p></td>
<td><p>중국</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>중국어(번체)</p></td>
<td><p>대만</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>덴마크어</p></td>
<td><p>덴마크</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>네덜란드어</p></td>
<td><p>네덜란드</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>오스트레일리아</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>영어</p></td>
<td><p>캐나다</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>인도</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>영어</p></td>
<td><p>영국</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>영어</p></td>
<td><p>미국</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>핀란드어</p></td>
<td><p>핀란드</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>프랑스어</p></td>
<td><p>캐나다</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>프랑스어</p></td>
<td><p>프랑스</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>독일어</p></td>
<td><p>독일</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>이탈리아어</p></td>
<td><p>이탈리아</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>일본어</p></td>
<td><p>일본</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>한국어</p></td>
<td><p>한국</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>노르웨이어(복말)</p></td>
<td><p>노르웨이</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>폴란드어</p></td>
<td><p>폴란드</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>포르투갈어</p></td>
<td><p>브라질</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>포르투갈어</p></td>
<td><p>포르투갈</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>러시아어</p></td>
<td><p>러시아</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>스페인어</p></td>
<td><p>스페인</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>스페인어</p></td>
<td><p>멕시코</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>스웨덴어</p></td>
<td><p>스웨덴</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


맨 위로 이동


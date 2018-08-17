---
title: 'UM 언어팩 제거: Exchange 2013 Help'
TOCTitle: UM 언어팩 제거
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50483810
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 언어팩 제거

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-14_

EAC 또는 셸을 사용하여 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버의 UM(통합 메시징) 언어를 관리할 수 있습니다. 그러나 UM 다이얼 플랜의 목록에서 언어를 제거하려면 **Setup.exe /RemoveUmLanguagePack** 명령을 사용하여 사서함 서버에서 해당하는 UM 언어 팩을 제거해야 합니다. 사서함 서버에서 UM 언어 팩을 제거한 후 UM 다이얼 플랜 또는 UM 자동 전화 교환을 구성할 때 이 언어를 사용할 수 없습니다. 사서함 서버의 속성을 보거나 **Get-UMService** cmdlet을 사용하여 설치된 UM 언어 팩을 확인할 수 있습니다.

UM 언어와 관련된 추가 작업에 대한 자세한 내용은 [UM 언어, 프롬프트 및 인사말 절차](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "사서함 서버(UM 서비스)" 항목

  - en-US 이외의 UM 언어 팩이 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Setup.exe를 사용하여 UM 언어 팩 제거

명령 프롬프트에서 다음 명령을 실행합니다.

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

이전 명령에서 *\<UmLanguagePackName\>*은 UM 언어 팩의 이름입니다(예: fr-FR).


> [!WARNING]
> 업데이트를 설치한 후에는 \Bin 폴더에 있는 Setup.exe 파일을 사용하여 UM 언어 팩을 제거할 수 없습니다. Exchange 2013 DVD 또는 다운로드한 원본 파일의 Setup.exe 파일을 사용해야 합니다. 그렇지 않으면 '실행 중인 응용 프로그램과 설치된 응용 프로그램 사이에 버전이 일치하지 않습니다.'라는 오류 메시지가 나타납니다.



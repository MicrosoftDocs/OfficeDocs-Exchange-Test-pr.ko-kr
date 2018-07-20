---
title: '메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여: Exchange 2013 Help'
TOCTitle: 메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65210911
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여

 

_**적용 대상:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-10-30_

사용자가 조직의 전자 메일 정책 준수를 위해 특정 단어 또는 패턴을 포함 하는 전자 메일 라우팅되는 방법을 확인 하려면 Exchange 전송 규칙을 사용할 수 있습니다. 단어 또는 구를 몇 명에 대 한 Exchange 관리 센터 를 사용할 수 있습니다. 긴 목록에 대 한 텍스트 파일을 사용 하 여 목록 읽어올 수 ExchangeWindows PowerShell 에 대 한 모듈 사용 하는 것이 좋습니다.

  - 예 1: 허용 되지않는 단어의 간단한 목록 사용

  - 예 2: 허용 되지않는 단어의 목록이 긴를 사용 합니다.

조직에서 데이터 손실 방지 (DLP)를 사용 하는 경우를 식별 하 고 중요 한 정보가 포함 된 전자 메일 라우팅에 대 한 추가 옵션에 대 한 [데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) 참조 하십시오.

## 예 1: 허용 되지않는 단어의 간단한 목록 사용

단어 또는 구를 목록이 짧은 경우 Exchange 관리 센터 를 사용 하 여 규칙을 만들 수 있습니다. 예, 잘못 된 단어 또는 회사 이름, 내부 머리글자어 또는 제품 이름의 맞춤법 오류가 있는 전자 메일을 보내는 아무도 있는지 확인 하려는 경우 메시지를 차단 하 고 보낸 사람에 게 지시 하는 규칙을 만들 수 있습니다. 단어 포함 하는 내용의 구 및 패턴 대/소문자 구분 하지 않습니다.

이 예제에서는 일반적인 오타 있는 메시지를 차단합니다.

![텍스트 패턴 기반의 메시지를 차단함을 보여주는 규칙](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "텍스트 패턴 기반의 메시지를 차단함을 보여주는 규칙")

## 예 2: 허용 되지않는 단어의 목록이 긴를 사용 합니다.

단어, 구 또는 패턴의 목록이 긴 경우 수에 넣으면 각 단어, 구 또는 패턴을 사용 하 여 텍스트 파일을 자체 줄에 있습니다. Windows PowerShell 에 대 한 Exchange 모듈 사용 하 여를 변수 읽어들일 키워드의 목록에서 전송 규칙 만들기 및 전송 규칙 조건에 키워드를 사용 하 여 변수를 지정 합니다. 예, 다음 스크립트 misspelled\_companyname.txt 라는 파일에서 맞춤법 오류 목록을 걸립니다.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## 텍스트 파일에서 구 및 패턴 사용

텍스트 파일은 패턴에 대한 정규식을 포함할 수 있습니다. 이러한 식은 대/소문자를 구분하지 않습니다. 일반적인 정규식은 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>식</strong></p></td>
<td><p><strong>일치 항목</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>임의의 단일 문자</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>임의의 추가 문자</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>임의의 10진수</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p><em>character_group</em>에 포함된 임의의 단일 문자</p></td>
</tr>
</tbody>
</table>


예,이 텍스트 파일 Microsoft 의 일반적인 맞춤법 오류를 포함합니다.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

정규식을 사용 하 여 패턴을 지정 하는 방법을 알아보려면 [일반 식을 참조 (영문)](https://go.microsoft.com/fwlink/p/?linkid=532394)을 참조 하십시오.


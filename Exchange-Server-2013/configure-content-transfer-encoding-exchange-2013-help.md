---
title: '콘텐츠 전송 인코딩을 구성합니다: Exchange 2013 Help'
TOCTitle: 콘텐츠 전송 인코딩을 구성합니다
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50484094
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 콘텐츠 전송 인코딩을 구성합니다

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

*콘텐츠 전송 인코딩*은 이진 전자 메일 메시지 데이터를 US-ASCII 일반 텍스트 형식으로 변환하는 인코딩 방법을 정의합니다. 이러한 변환을 통해 메시지는 US-ASCII 텍스트 메시지만 지원하는 이전 SMTP 메시징 서버를 통해 이동할 수 있습니다. 콘텐츠 전송 인코딩은 RFC 2045에 정의되어 있습니다. 전송 인코딩 방법은 메시지의 **Content-Transfer-Encoding** 헤더 필드에 저장됩니다. Microsoft Exchange Server 2013에서는 다음 콘텐츠 전송 인코딩 방법을 사용할 수 있습니다.

  - **7비트**   이 값은 메시지 본문 데이터가 이미 US ASCII 일반 텍스트 형식이며 메시지에 대한 메시지 인코딩이 수행되지 않았음을 나타냅니다.

  - **QP(Quoted-Printable)**   이 인코딩 방법은 인쇄용 US-ASCII 문자를 사용하여 메시지 본문 데이터를 인코딩합니다. 원본 메시지 텍스트가 대부분 US-ASCII 텍스트인 경우 QP 인코딩을 통해 어느 정도 읽을 수 있는 간결한 메시지를 얻을 수 있습니다. 기본적으로 Exchange 2013에서는 QP를 사용하여 이진 메시지 데이터를 인코딩합니다.

  - **Base64**   이 인코딩 방법은 주로 RFC 1421에 정의된 PEM(Privacy-Enhanced Mail) 표준을 기반으로 합니다. Base64 인코딩은 64자 알파벳 인코딩 방법 및 PEM으로 정의한 출력 패딩 문자를 사용하여 메시지 본문 데이터를 인코딩합니다. 예측 가능하게 메시지 크기를 증가시키는 Base64 인코딩은 이진 데이터와 비 US-ASCII 텍스트에 사용하는 것이 좋습니다.

**Set-OrganizationConfig** 및 **Set-RemoteDomain** cmdlet에 *ByteEncoderTypeFor7BitCharsets* 매개 변수를 사용하여 전송 인코딩 방법을 구성합니다. **Set-OrganizationConfig**를 사용하여 구성한 콘텐츠 전송 인코딩 설정은 Exchange 조직의 모든 메시지에 적용됩니다. **Set-RemoteDomain**을 사용하여 구성한 콘텐츠 전송 인코딩 설정은 원격 도메인의 외부 받는 사람에게 보내는 메시지에만 적용됩니다.

다음 표에는 전송 인코딩 방법을 설정하는 데 사용할 수 있는 값이 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Set-OrganizationConfig</strong>의 매개 변수</th>
<th><strong>Set-RemoteDomain</strong>의 매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>HTML 및 일반 텍스트에 대해 항상 7비트 인코딩을 사용합니다. 이 값은 기본값입니다.</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>HTML 및 일반 텍스트에 대해 QP 인코딩을 항상 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>HTML 및 일반 텍스트에 대해 Base64 인코딩을 항상 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>줄 바꿈을 일반 텍스트에서 사용하도록 설정하지 않은 경우 HTML 및 일반 텍스트에 대해 QP 인코딩을 사용합니다. 줄 바꿈을 사용하도록 설정한 경우 일반 텍스트에 대해 7비트 인코딩을 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>줄 바꿈을 일반 텍스트에서 사용하도록 설정하지 않은 경우 HTML 및 일반 텍스트에 대해 Base64 인코딩을 사용합니다. 줄 바꿈을 일반 텍스트에서 사용하도록 설정한 경우 HTML에는 Base64 인코딩을 사용하고 일반 텍스트에는 7비트 인코딩을 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>HTML에 대해 QP 인코딩을 항상 사용합니다. 일반 텍스트에 대해 7비트 인코딩을 항상 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>HTML에 대해 Base64 인코딩을 항상 사용합니다. 일반 텍스트에 대해 7비트 인코딩을 항상 사용합니다.</p></td>
</tr>
</tbody>
</table>


**Content-Transfer-Encoding** 헤더 필드에 대한 자세한 내용은 [콘텐츠 변환](content-conversion-exchange-2013-help.md)에서 "전자 메일 메시지의 구조 이해"를 참조하십시오.

원격 도메인에 대한 자세한 내용은 [원격 도메인](remote-domains-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "전송 서비스" 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 조직에 대한 콘텐츠 전송 인코딩 방법 구성

조직에 대한 콘텐츠 전송 인코딩 방법을 구성하려면 다음 명령을 실행합니다.

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

예를 들어 콘텐츠 전송 인코딩 방법을 Base64로 설정하려면 다음 명령을 실행합니다.

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## 셸을 사용하여 원격 도메인에 대한 콘텐츠 전송 인코딩 방법 구성

원격 도메인의 모든 받는 사람에 대한 콘텐츠 전송 인코딩 방법을 구성하려면 다음 명령을 실행합니다.

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

예를 들어 콘텐츠 전송 인코딩 방법을 Base64로 설정하려면 다음 명령을 실행합니다.

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## 작동 여부는 어떻게 확인합니까?

콘텐츠 전송 인코딩 방법이 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

1.  US-ASCII 텍스트와 이진 데이터 또는 US-ASCII가 아닌 텍스트가 섞여 있는 테스트 메시지를 내부 또는 외부 테스트 계정에 보냅니다. 내부 계정을 사용하여 조직 설정을 테스트하고 원격 도메인의 외부 계정을 사용하여 원격 도메인 설정을 테스트합니다.

2.  전자 메일 클라이언트에서 메시지의 **Content-Transfer-Encoding** 헤더 필드를 보고, 메시지에 사용된 콘텐츠 전송 인코딩 방법이 자신이 구성한 방법과 일치하는지 확인하십시오.


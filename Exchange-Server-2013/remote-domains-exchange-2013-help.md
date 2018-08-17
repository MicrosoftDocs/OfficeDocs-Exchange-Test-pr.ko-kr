---
title: '원격 도메인: Exchange 2013 Help'
TOCTitle: 원격 도메인
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50482541
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원격 도메인

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

원격 도메인 항목을 만들어 Microsoft Exchange Server 2013 조직과 Exchange 조직 외부에 있는 도메인 간의 메시지 전송에 대한 설정을 정의할 수 있습니다. 원격 도메인 항목을 만들 때 해당 도메인으로 전송되는 메시지 유형을 제어할 수 있습니다. 조직의 사용자가 원격 도메인으로 보낸 메시지에 대해 메시지 형식 정책 및 허용 가능한 문자 집합을 적용할 수도 있습니다. 원격 도메인의 설정은 Exchange 조직에 대한 글로벌 구성 설정입니다.

원격 도메인 설정은 사서함 서버의 전송 서비스에서 분류 중에 메시지에 적용됩니다. 받는 사람이 확인되면 해당 받는 사람 도메인이 구성된 원격 도메인과 비교됩니다. 원격 도메인 구성에서 해당 도메인에 있는 받는 사람에게 특정 메시지 유형이 전송되지 않도록 차단하면 해당 메시지는 삭제됩니다. 원격 도메인에 대해 특정 메시지 형식을 지정하면 메시지 머리글과 콘텐츠가 수정됩니다. 해당 설정은 Exchange 조직에서 처리하는 모든 메시지에 적용됩니다.


> [!NOTE]
> 사용자별로 메시지 설정을 구성하면 사용자별 설정이 조직 구성을 재정의합니다.



기본적으로 한 개의 원격 도메인 항목이 있습니다. 도메인 주소 공간은 별표(\*)로 구성됩니다. 별표는 모든 원격 도메인을 나타냅니다. 추가 원격 도메인 항목을 만들지 않은 경우 모든 원격 도메인의 모든 받는 사람에게 전송되는 모든 메시지에 동일한 설정이 적용됩니다.

원격 도메인을 구성할 때 특정 유형의 메시지가 해당 도메인으로 전송되지 못하게 할 수 있습니다. 이러한 메시지 유형에는 부재 중 메시지, 자동 회신 메시지, NDR(배달 못 함 보고서) 및 모임 전달 알림이 포함됩니다. 다중 포리스트 환경에서는 해당 메시지 유형을 해당 도메인으로 보내도록 할 수 있습니다. 그러나 스팸 메일이 시작된 도메인을 식별하면 해당 메시지 유형을 해당 원격 도메인으로 보내지 못하게 차단할 수 있습니다.

**목차**

Message format

Automatic replies settings

Controlling NDR information

## 메시지 형식

원격 도메인으로 보내는 전자 메일 메시지에 사용할 메시지 형식과 문자 집합을 지정할 수 있습니다. 이러한 설정은 도메인의 보낸 사람이 원격 도메인으로 보낸 전자 메일이 수신 전자 메일 시스템과 호환되도록 하는 데 유용할 수 있습니다. 예를 들어 원격 도메인의 메시징 시스템이 Exchange인 경우 항상 Exchange RTF(서식 있는 텍스트) 형식을 사용하도록 지정할 수 있습니다. 자세한 내용은 [콘텐츠 변환](content-conversion-exchange-2013-help.md) 항목을 참조하십시오.

## 자동 회신 설정

Exchange 2013에서는 사용자가 내부 및 외부의 받는 사람에 대해 서로 다른 자동 회신을 지정할 수 있습니다. 또한 조직에서 사용할 수 있는 자동 회신의 유형은 사용 중인 Microsoft Outlook 버전에 따라 달라집니다.

Exchange 2013에는 두 가지 자동 회신 유형이 있습니다.

  - **외부**   Exchange 2013 및 Exchange 2010에서 지원됩니다. Outlook 2010 또는 Office Outlook 2007에서나 Microsoft Office Outlook Web App를 사용해서만 설정할 수 있습니다.

  - **내부**   Exchange 2013 및 Exchange 2010에서 지원됩니다. Outlook 2010 또는 Outlook 2007에서나 Outlook Web App를 사용해서만 설정할 수 있습니다.

다음 표에서는 다양한 클라이언트 및 서버 조합과 각 시나리오에서 사용할 수 있는 자동 회신 유형에 대해 설명합니다.

**자동 회신에 대한 클라이언트 및 서버 지원**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트 버전</th>
<th>Exchange 버전</th>
<th>지원되는 자동 회신</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 또는 Outlook 2007</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>내부, 외부</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>내부, 외부</p></td>
</tr>
</tbody>
</table>


## NDR 정보 제어

이 항목의 시작 부분에서 언급했듯이 NDR이 원격 도메인으로 전송되지 않도록 할 수 있습니다. 원격 도메인에 NDR이 전송되지 않도록 차단하면 NDR 메시지에 포함된 정보가 조직에서 유출되는 것을 방지하여 악의적인 사용자가 조직에 대해 수집할 수 있는 지식을 제한할 수 있습니다. 하지만 올바른 보낸 사람도 NDR을 받을 수 없게 되므로 혼동이 발생하고 생산성이 저하됩니다.

Exchange 2013에서는 원격 도메인으로 전송되는 NDR의 콘텐츠를 세부적으로 제어할 수 있습니다. Exchange 2013에서는 원격 도메인에 대해 NDR을 허용하되 진단 정보를 모두 제거할 수 있습니다. 이렇게 하면 외부 보낸 사람에게 NDR 알림을 제공하는 동시에 Exchange 배포에 대한 정보가 조직에서 나가지 않도록 할 수 있습니다.

이 기능은 **Set-RemoteDomain** cmdlet의 *NDRDiagnosticInfoEnabled* 매개 변수로 제어됩니다. 각 원격 도메인에 대해 이 설정을 구성할 수 있으므로 필요에 따라 여러 설정을 사용할 수 있습니다. 예를 들어 기본 원격 도메인의 경우 NDR 진단 정보를 제거하지만 파트너를 나타내는 원격 도메인의 경우 전체 NDR 진단 정보를 허용하도록 선택할 수 있습니다.

이 새로운 설정에 대한 자세한 내용은 [Set-RemoteDomain](https://technet.microsoft.com/ko-kr/library/aa997857\(v=exchg.150\))항목을 참조하십시오.


---
title: 'FAQ: Exchange 관리 센터: Exchange 2013 Help'
TOCTitle: 'FAQ: Exchange 관리 센터'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50482926
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# FAQ: Exchange 관리 센터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이 항목에서는 Microsoft Exchange Server 2013의 새로운 EAC(Exchange 관리 센터)에 대한 질문과 대답의 목록을 제공합니다. 여기에서 다루지 않은 EAC에 대한 질문이 더 있으면 [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)으로 전자 메일을 보내십시오.

## EAC는 Exchange Online 전용으로 개발되었습니까?

EAC는 온-프레미스로 배포하거나 Exchange 2013이 있는 클라우드에서 배포하려는 고객과 하이브리드 배포를 원하는 고객을 비롯하여 Exchange Online의 모든 배포 옵션을 처리합니다.

## 주로 중소기업 고객을 위한 인터페이스를 만들기 때문에 EMC(Exchange 관리 콘솔)를 제거한 것입니까?

EAC는 모든 고객에게 직관적인 단일 관리 환경을 제공하기 위해 개발되었으며 가장 일반적인 관리 작업을 보다 간단하게 실행할 수 있도록 설계되었습니다.

Microsoft는 EMC(Exchange 관리 콘솔) 및 ECP(Exchange 제어판)에 대한 모든 시나리오를 제공하고 고객의 주요 과제와 시나리오를 처리하는 단일 인터페이스를 만들었습니다.

또한 모든 규모의 고객에게 의견을 들은 결과 고객의 주요 관심사는 다음과 같았습니다.

  - 관리 도구를 작동하기 위해 패치를 유지 관리하고 다운로드하는 것은 고객에게 운영 오버헤드이며 운영 비용을 증가시킵니다.

  - IT 인력의 이동성이 점차 증가함에 따라 고객은 관리 도구가 설치된 데스크톱과 서버뿐만 아니라 어디에서든 환경을 관리할 수 있기를 원했습니다.

  - 다양한 배포 옵션에 따라 여러 도구를 사용하면 혼란스러워지고 교육 및 운영 비용이 증가합니다.

## PowerShell 로깅 및 cmdlet이 EAC에 다시 도입됩니까?

이에 대해 초기에 고객의 의견을 받았고 향후 업데이트에 이를 처리할 가능성을 평가하고 있습니다.

## 향후 출시될 서비스 팩에 EMC가 다시 도입됩니까?

아니요. Microsoft는 EAC 환경을 완전히 지원합니다.

## Exchange 2010 EMC를 사용하여 Exchange 2013 개체를 관리할 수 있습니까?

아니요. Exchange 2010 EMC를 사용하여 Exchange 2013 개체 및 서버를 관리할 수 없습니다. 고객은 Exchange 2013으로 업그레이드하는 동안 EAC를 사용하여 다음을 수행하는 것이 좋습니다.

1.  Exchange 2013 사서함, 서버 및 해당 서비스 관리

2.  Exchange 2010 사서함과 속성 보기 및 업데이트

3.  Exchange 2007 사서함과 속성 보기 및 업데이트

하고자를 하는 Exchange 2010 EMC를 사용 하 여 Exchange 2010 사서함 만들기 및 관리를 사용 하는 것이 좋습니다.

Exchange 2007 EMC Exchange 2007 사서함 만들기 및 관리를 사용 하 여 고객을 사용 하는 것이 좋습니다.

고객은 계속해서 Exchange 관리 셸 및 스크립트 작업을 사용하여 관리 작업을 수행할 수 있습니다.

## 검색 상자가 표시되지 않을 때도 있는데 왜 그렇습니까?

Exchange 2013에 대한 설계 원칙의 일환으로, 검색 상자가 필요할 때까지 사용자를 방해하지 않으려는 의도입니다. 이러한 단순성은 모든 최종 사용자 환경에 나타나 있습니다(EAC 포함). 아이콘을 클릭하면 검색 상자가 밀려 나옵니다. 검색 상자는 사용자가 텍스트 상자에 쿼리를 입력할 수 있는 충분한 공간을 제공하며 실시간 쿼리 일치가 발생하면 입력 문자열이 완성되어 표시됩니다. 이에 따라 관리 환경을 줄이지 않고 불필요한 복잡성을 숨길 수 있습니다. Microsoft는 고객의 의견에 따라 모든 환경을 계속해서 개선할 것입니다.

## EAC는 태블릿에서 작동합니까?

태블릿과 모바일 장치를 통한 관리는 현재 지원되지 않습니다.

## Exchange 2013 EAC에 액세스하려고 하면 Exchange 2010 ECP가 열리는 이유는 무엇입니까?

사서함이 Exchange 2010 사서함 서버에 있는 경우 Exchange 2010 ECP가 브라우저에 자동으로 로드됩니다. 이는 설계에 따른 것입니다. Exchange 버전을 URL에 추가하면 EAC에 액세스할 수 있습니다. 예를 들어 가상 디렉터리가 클라이언트 액세스 서버 CAS01-NA에 호스트된 EAC에 액세스하려면 `https://CAS01-NA/ecp?ExchClientVer=15`.

## EAC를 사용할 수 있는 위치에 어떻게 제한을 둡니까?

인터넷과 인트라넷 액세스를 제한하기 위해 Exchange는 IIS의 가상 디렉터리 수준으로 분할을 제공합니다. 관리자는 IT 관리 시나리오가 회사 방화벽 내의 도메인에 가입되지 않은 클라이언트 등의 외부 인터넷 클라이언트에서 수행되는 것을 명시적으로 허용하거나 거부할 수 있습니다. 자세한 내용은 [Exchange 관리 센터에 대 한 액세스를 해제](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md) 항목을 참조하십시오.

## Exchange 2013 도구 상자에서는 무엇이 변경되었습니까?

Exchange 2007 및 Exchange 2010에서 EMC에는 Exchange 조직을 관리하기 위해 다양한 도구에 액세스할 수 있는 도구 상자가 포함되어 있습니다. Exchange 2013 도구 상자는 이전 버전에 비해 상당히 축소되었습니다. 세부 항목 템플릿 편집기, 원격 연결 분석기 및 큐 뷰어는 Exchange 2013 도구 상자에서 여전히 사용할 수 있습니다. 나머지 도구는 용도가 변경되었거나 EAC로 이동되었습니다.

다음 표에 Exchange 2013 도구 상자의 변경 내용이 정리되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>도구</th>
<th>현재 상태</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExBPA(Exchange 모범 사례 분석기)</p></td>
<td><p>ExBPA는 더 이상 사용되지 않습니다. 준비 검사에서 Active Directory 포리스트와 Exchange 서버가 Exchange 2013용으로 준비되도록 하기 위해 ExBPA를 교체했습니다. 각 준비 검사 항목에서는 준비 검사가 실행될 때 발견된 문제를 해결하기 위해 취할 수 있는 조치에 대해 설명합니다. 준비 검사 항목에 요약된 단계는 설치 중 그러한 준비 검사가 표시된 경우에만 수행해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>메일 흐름 문제 해결사</p></td>
<td><p>메일 흐름 문제 해결사가 사용 중지되었습니다. 이제 EAC에서 메시지 추적 기능을 사용할 수 있습니다. <strong>메일 흐름</strong> &gt; <strong>배달 보고서</strong>로 이동합니다.</p></td>
</tr>
<tr class="odd">
<td><p>성능 모니터</p></td>
<td><p>성능 모니터가 도구 상자에서 사용 중지되었습니다. Windows Server 2008 및 Windows Server 2012에서는 <strong>관리 도구</strong>에서 성능 모니터를 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>성능 문제 해결사</p></td>
<td><p>성능 문제 해결사가 도구 상자에서 사용 중지되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>라우팅 로그 뷰어</p></td>
<td><p>라우팅 로그 뷰어가 사용 중지되었습니다.</p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리 콘솔</p></td>
<td><p>공용 폴더는 이제 EAC에서 관리됩니다. EAC에서 <strong>공용 폴더</strong>로 이동합니다.</p></td>
</tr>
<tr class="odd">
<td><p>RBAC(역할 기반 액세스 제어) 사용자 편집기</p></td>
<td><p>RBAC는 이제 EAC에서 관리됩니다. EAC에서 <strong>사용 권한</strong>으로 이동합니다.</p></td>
</tr>
</tbody>
</table>


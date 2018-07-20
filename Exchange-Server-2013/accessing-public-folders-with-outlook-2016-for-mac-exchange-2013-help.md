---
title: 'Mac 용 Outlook 2016와 공용 폴더 액세스 (영문): Exchange 2013 Help'
TOCTitle: Mac 용 Outlook 2016와 공용 폴더 액세스 (영문)
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mac 용 Outlook 2016와 공용 폴더 액세스 (영문)

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**마지막으로 수정된 항목:** 2017-05-19_

**요약:**  지원 되는 가장 최근의 사용자가 for mac입니다. Outlook 2016와 공용 폴더에 액세스할 수 있도록 하는 Exchange 토폴로지

Mac 클라이언트에 대 한 버전의 Outlook 2016에 대 한 [2016 년 4 월 업데이트](https://go.microsoft.com/fwlink/?linkid=829202) 에서는 Exchange 2013에 대 한 [누적 업데이트 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) 및 Exchange 2016, Mac 용 Outlook 2016의 사용자에 대 한 [누적 업데이트 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) 이제에 액세스할 수 더 많은 유형의 토폴로지의 공용 폴더 하기 전에 수 있으므로 보다 합니다.

## Mac 제한 사항에 대 한 outlook

모든 버전의 Outlook for Mac Exchange 공용 폴더에 액세스할 수 있지만 최근까지 이러한 클라이언트에 액세스할 수 없습니다는 다음과 같은 배포 시나리오에서 공용 폴더:

  - **레거시 공용 폴더와 동시 사용.** Exchange 2013 / Exchange 2016 서버에 사용자의 사서함이 있는 경우에 사용자는 Exchange 2010 s p 3을 실행 하는 서버에 배포 된 이상 공용 폴더에 액세스 하려면 Outlook for Mac 사용 하지 못했습니다. 다른 클라이언트가이 시나리오에서 이러한 레거시 공용 폴더에 액세스할 수 있습니다.

  - **하이브리드 토폴로지.** Exchange online 기반 사서함이 있는 온-프레미스 사용자가 온-프레미스 현대 공용 폴더에 액세스 하려면 Outlook for Mac 사용 하지 못했습니다. 마찬가지로, Exchange 2013 또는 Exchange 2016 사서함 온-프레미스 사용자가 공용 폴더에 액세스 하는 Mac 배포 Exchange Online에 대 한 Outlook을 사용 하지 못했습니다.

## Mac용 Outlook 2016

년 4 월 2016 업데이트와 Outlook 2016에 대 한, Mac로 Exchange 2013에 대 한 CU14 및 Exchange 2016에 대 한 누적 업데이트 패키지 2에 대 한 위의 시나리오는 이제 Outlook 2016에 대 한 Mac 클라이언트에 대 한 적용 됩니다.

다음 표에서 Exchange 2016 및 Exchange Online 2013, Exchange 공용 폴더에 액세스 하려고 하는 Mac 클라이언트에 대 한 Outlook 2016와 사용자에 대해 지원 되는 토폴로지를 보여줍니다.


> [!NOTE]
> 다음 표에 표시 된 시나리오는 Mac 용 Outlook 2016 년 4 월 2016 업데이트가 모든 클라이언트에 적용 된 가정 합니다.




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
<th>공용 폴더에 배포 되는 중...</th>
<th>사용자 사서함이 Exchange 2010 SP3 이상</th>
<th>사용자 사서함이 Exchange 2013 CU13 이상</th>
<th>사용자 사서함이 Exchange 2016 c u 2 이상</th>
<th>Office 365/Exchange Online 사용자 사서함이</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 이상</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
<td><p>지원되지 않음</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 이상</p></td>
<td><p>지원되지 않음</p></td>
<td><p>지원됨</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 c u 2 이상</p></td>
<td><p>지원되지 않음</p></td>
<td><p>지원됨</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>지원되지 않음</p></td>
<td><p>지원됨</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
</tr>
</tbody>
</table>


다음 문서에서는 동시 사용 또는 하이브리드 토폴로지는 Exchange 조직에서 공용 폴더를 배포 하는 방법에 설명 합니다. Mac 클라이언트에 대 한 사용자 Outlook 2016 년 4 월 2016 업데이트를 설치 하는 있기만 이러한 문서에 자세히 설명 하는 구성의 공용 폴더에 액세스할 수 있습니다.

  - [Exchange 2013 서버에서 사용자 사서함이 있는 레거시 공용 폴더 구성](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [하이브리드 배포에 대 한 Exchange Online 공용 폴더 구성](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)


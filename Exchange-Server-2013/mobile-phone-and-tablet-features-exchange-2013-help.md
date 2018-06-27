---
title: '휴대폰 및 태블릿 기능: Exchange 2013 Help'
TOCTitle: 휴대폰 및 태블릿 기능
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50556064
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 휴대폰 및 태블릿 기능

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

사용자가 Microsoft Exchange ActiveSync를 통해 자신의 전자 메일, 일정, 연락처 및 작업 정보 휴대폰, 태블릿 및 기타 휴대용 장치에 액세스할 수 있습니다. 자신의 서명 및 자동 회신을 설정 하려면 사용할 수 있습니다. 다양 한 휴대폰 및 모바일 장치 Exchange ActiveSync를 사용 합니다.


> [!NOTE]
> 지속적으로 휴대폰으로 Exchange Server 2013 에 액세스 하는 장치에 지칭, 하지만는 다음과 같은 많은 장치 Exchange 2013 에 액세스할 수 있지만 휴대폰 기능 없는입니다. 이 설명서에서 "휴대폰" 이라는 용어는 해당 장치를 가리킵니다.



## Exchange ActiveSync 호환 장치

사용자가 Exchange ActiveSync 과 호환 되는 휴대폰을 선택 하 여 Exchange ActiveSync 의 다양 한 기능 이용할 수 있습니다. 이러한 휴대폰에서 많은 제조업체 및 많은 전화 사업자에서 사용할 수 있습니다. 자세한 내용은 특정 휴대폰 설명서를 참조 하십시오.

Microsoft Exchange 과 호환 되는 휴대폰은 다음과 같습니다.

  - **Apple**   Apple iPhone, iPod Touch 및 iPad 모든 Exchange ActiveSync 를 지원 합니다.

  - **Windows Phone**   Windows Phone 8, Windows Phone 7 및 이전 버전은 모든 Exchange ActiveSync를 지원 합니다.

  - **Android**   다양 한 휴대폰 및 Android 운영 체제 태블릿 Exchange ActiveSync 를 지원 합니다. 그러나 이러한 모바일 장치는 모든 사용 가능한 모바일 장치 사서함 정책을 지원 하지 않습니다. 자세한 내용은 [모바일 장치 사서함 정책](mobile-device-mailbox-policies-exchange-2013-help.md)을 참조 하십시오.

## Windows Phone 소프트웨어 기능

휴대폰 Windows 자신의 운영 체제로 전화 소프트웨어의 버전에 Exchange 2013과 동기화 할 때 가장 큰 기능을 제공 합니다. 다음 표에 Windows Phone 8 및 Windows Phone 7에서 사용할 수 있는 모바일 장치 사서함 정책입니다.

### Windows Phone 7 및 8 기능

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>운영 체제</th>
<th>기능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8에서는 다음과 같은 모바일 장치 사서함 정책을 지원합니다.</p>
<ul>
<li><p>간단한 장치 암호 허용</p></li>
<li><p>영숫자 암호 필요</p></li>
<li><p>장치 암호 사용</p></li>
<li><p>장치 암호 만료</p></li>
<li><p>IRM 사용</p></li>
<li><p>최대 장치 암호 시도 실패 횟수</p></li>
<li><p>최대 비활성 장치 시간 잠금</p></li>
<li><p>최소 장치 암호 복합 문자 수</p></li>
<li><p>최소 장치 암호 길이</p></li>
<li><p>장치 암호화 필요</p></li>
<li><p>원격 지우기</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>조직 다른 모바일 장치 사서함 정책 설정을 사용 하는 경우 <strong>지원 불가 장치 허용</strong> 정책을 true로 설정 해야 합니다. 이 수에 영향을 보안 조직에 대 한 되므로 다른 휴대폰 및 모바일 장치 정책 설정의 모든 요구 사항을 충족 하지 않는 장치를 동기화 할 수 있습니다. 자세한 내용은 <a href="mobile-device-mailbox-policies-exchange-2013-help.md">모바일 장치 사서함 정책</a>을 참조 하십시오.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Windows Phone 7 휴대폰 모든 Exchange ActiveSync 사서함 정책 설정의 하위 집합을 지원합니다.</p>
<ul>
<li><p>암호 필요</p></li>
<li><p>최소 암호 길이</p></li>
<li><p>최대 비활성 시간 잠금</p></li>
<li><p>최대 장치 암호 시도 실패 횟수</p></li>
<li><p>단순 암호 허용</p></li>
<li><p>암호 만료</p></li>
<li><p>암호 기록</p></li>
<li><p>이동식 저장소를 사용 하지 않도록 설정</p></li>
<li><p>IrDA를 사용 하지 않도록 설정</p></li>
<li><p>데스크톱 동기화를 사용 하지 않도록 설정</p></li>
<li><p>원격 데스크톱 차단</p></li>
<li><p>인터넷 공유 차단</p></li>
</ul></td>
</tr>
</tbody>
</table>


---
title: '모바일 장치 사서함 정책: Exchange 2013 Help'
TOCTitle: 모바일 장치 사서함 정책
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50483690
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 모바일 장치 사서함 정책

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-06-16_

Microsoft Exchange Server 2013에서는 모바일 장치 사서함 정책을 만들어 사용자 모음에 공통된 정책이나 보안 설정 집합을 적용할 수 있습니다. Exchange ActiveSync 조직에 Exchange 2013를 배포한 후 새 모바일 장치 사서함 정책을 만들거나 기존 정책을 수정할 수 있습니다. Exchange 2013을 설치할 때 기본 모바일 장치 사서함 정책이 만들어집니다. 모든 사용자에게 자동으로 이 기본 모바일 장치 사서함 정책이 할당됩니다.


> [!IMPORTANT]
> Windows Phone 7 휴대폰은 모든 Exchange ActiveSync 사서함 정책 설정 중 일부만 지원합니다. 전체 목록을 보려면 Windows Phone 7 Synchronization를 참조하십시오.



> [!CAUTION]
> iOS7 지문 판독기는 장치 암호로 지원되지 않습니다. 지문 판독기로 iOS7 장치를 보호하도록 설정하는 경우에도 모바일 장치 사서함 정책에서 암호를 필요로 하는 경우 암호를 만들고 입력해야 합니다.


## 모바일 장치 사서함 정책의 개요

모바일 장치 사서함 정책을 사용하여 서로 다른 여러 설정을 관리할 수 있습니다. 여기에는 다음과 같은 사항이 포함됩니다.

  - 암호 요구

  - 최소 암호 길이 지정

  - 암호에 숫자 또는 특수 문자 필요

  - 사용자에게 암호를 다시 입력하도록 요구하기 전에 장치가 비활성 상태로 유지될 수 있는 시간 지정

  - 지정된 횟수 이상 암호 입력 시도에 실패하는 경우 장치 지우기

구성할 수 있는 모든 설정에 대한 자세한 내용은 모바일 장치 정책 설정을 참조하십시오.

## Exchange ActiveSync 사서함 정책 관리

모바일 장치 사서함 정책은 EAC(Exchange 관리 센터)나 Exchange 관리 셸에서 만들 수 있습니다. EAC에서 정책을 만들면 사용 가능한 설정 중 일부만 구성할 수 있습니다. 나머지 설정은 셸을 사용하여 구성할 수 있습니다.

## Windows Phone 7 동기화

조직에 Windows Phone 7 휴대폰이 있는 경우 특정 Exchange ActiveSync 사서함 정책 속성이 구성되어 있으면 휴대폰에 동기화 문제가 생깁니다. Windows Phone 7 휴대폰이 Exchange 사서함과 동기화되도록 하려면 **AllowNonProvisionableDevices** 속성을 True로 설정하거나 다음과 같은 Exchange ActiveSync 사서함 정책 속성만 구성합니다.

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## 모바일 장치 사서함 정책 설정

다음 표에는 모바일 장치 사서함 정책을 사용하여 지정할 수 있는 설정이 요약되어 있습니다.

### 모바일 장치 사서함 정책 설정

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bluetooth 허용</p></td>
<td><p>이 설정은 모바일 장치에서 Bluetooth 연결을 허용할지 여부를 지정합니다. 사용 가능한 옵션은 사용 안 함, 핸즈프리 전용 및 허용입니다. 기본값은 Allow입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>브라우저 허용</p></td>
<td><p>이 설정은 Pocket Internet Explorer를 모바일 장치에서 허용할지 여부를 지정합니다. 이 설정은 모바일 장치에 설치된 타사 브라우저에는 영향을 주지 않습니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>카메라 허용</p></td>
<td><p>이 설정은 모바일 장치 카메라를 사용할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>사용자 전자 메일 허용</p></td>
<td><p>이 설정은 모바일 장치에는 모바일 장치 사용자를 개인 전자 메일 계정 (POP3 또는 IMAP4)를 구성할 수 있는지 여부를 지정 합니다. 기본값은 <code>$true</code>입니다. 이 설정은 모바일 장치에서 타사 전자 메일 프로그램을 사용 하 고 있는 전자 메일 계정에 대 한 액세스를 제어 하지 않습니다. 이 설정의 값을 변경 하려면 Exchange 엔터프라이즈 클라이언트 액세스 라이선스가 필요 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>데스크톱 동기화 허용</p></td>
<td><p>이 설정은 모바일 장치가 케이블, Bluetooth 또는 IrDA 연결을 통해 컴퓨터와 동기화할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>외부 장치 관리 허용</p></td>
<td><p>이 설정은 외부 장치 관리 프로그램이 모바일 장치를 관리할 수 있는지 여부를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>HTML 전자 메일 허용</p></td>
<td><p>이 설정은 모바일 장치와 동기화된 전자 메일을 HTML 형식으로 사용할 수 있는지 여부를 지정합니다. 이 설정을 <code>$false</code>로 설정할 경우 모든 전자 메일이 일반 텍스트로 변환됩니다.</p></td>
</tr>
<tr class="even">
<td><p>인터넷 공유 허용</p></td>
<td><p>이 설정은 모바일 장치를 데스크톱 또는 휴대용 컴퓨터의 모뎀으로 사용할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>이 설정은 모바일 장치와의 적외선 연결 허용 여부를 지정합니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>모바일 OTA 업데이트 허용</p></td>
<td><p>이 설정은 모바일 장치 사서함 정책 설정을 셀룰러 데이터 연결을 통해 모바일 장치로 전송할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>지원 불가 장치 허용</p></td>
<td><p>이 설정은 모든 정책 설정의 응용 프로그램을 지원 하지 않을 수도 있는 모바일 장치는 Exchange 2013Exchange ActiveSync 를 사용 하 여 연결할 수 있는지 여부를 지정 합니다. 보안 관련 문제는 모바일 지원 불가 장치 허용 합니다. 예, 일부 지원 불가 장치 조직의 암호 요구 사항을 구현 하려면 못할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>POPIMAPEmail 허용</p></td>
<td><p>이 설정은 여부 사용자 구성할 수는 POP3 또는 IMAP4 전자 메일 계정을 모바일 장치에서 지정 합니다. 기본값은 <code>$true</code>합니다. 이 설정은 타사 전자 메일 프로그램으로 대 한 액세스를 제어 하지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>원격 데스크톱 허용</p></td>
<td><p>이 설정은 모바일 장치에서 원격 데스크톱 연결을 시작할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>단순 암호 허용</p></td>
<td><p>이 설정은 1111 또는 1234와 같은 단순 암호를 사용하는 기능을 사용하거나 사용하지 않도록 설정합니다. 기본값은 <code>$true</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME 암호화 알고리즘 협상 허용</p></td>
<td><p>이 설정은 받는 사람의 인증서가 지정 된 암호화 알고리즘을 지원 하지 않을 경우 모바일 장치의 메시징 응용 프로그램이 암호화 알고리즘을 협상할 수 있는지 여부를 지정 합니다.</p></td>
</tr>
<tr class="even">
<td><p>S/MIME 소프트웨어 인증서 허용</p></td>
<td><p>이 설정은 모바일 장치에서 S/MIME 소프트웨어 인증서 허용 여부를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>저장소 카드 허용</p></td>
<td><p>이 설정은 모바일 장치에서 저장소 카드에 저장된 정보에 액세스할 수 있는지 여부를 지정합니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>텍스트 메시징 허용</p></td>
<td><p>이 설정은 모바일 장치에서 텍스트 메시징을 허용할지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>서명되지 않은 응용 프로그램 허용</p></td>
<td><p>이 설정은 서명되지 않은 응용 프로그램을 모바일 장치에 설치할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>서명되지 않은 설치 패키지 허용</p></td>
<td><p>이 설정은 모바일 장치에서 서명되지 않은 설치 패키지를 실행할 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Wi-Fi 허용</p></td>
<td><p>이 설정은 모바일 장치에서 무선 인터넷 액세스를 허용할지 여부를 지정합니다. 기본값은 <code>$true</code>입니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>영숫자 암호 필요</p></td>
<td><p>이 설정에서는 암호에 숫자 및 숫자가 아닌 문자가 포함되어야 합니다. 기본값은 <code>$true</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>승인된 응용 프로그램 목록</p></td>
<td><p>이 설정은 모바일 장치에서 실행할 수 있는 승인된 응용 프로그램 목록을 저장합니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>첨부 파일 사용</p></td>
<td><p>이 설정은 첨부 파일을 모바일 장치에 다운로드할 수 있도록 설정합니다. 기본값은 <code>$true</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>장치 암호화 사용</p></td>
<td><p>이 설정은 모바일 장치에서 암호화를 사용하도록 설정합니다. 일부 모바일 장치는 암호화를 적용할 수 없습니다. 자세한 내용은 장치 및 모바일 운영 체제 설명서를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>장치 정책 새로 고침 간격</p></td>
<td><p>이 설정은 모바일 장치 사서함 정책을 서버에서 모바일 장치로 보내는 간격을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>IRM 사용</p></td>
<td><p>이 설정은 모바일 장치에서 IRM(정보 권한 관리)을 사용하도록 설정할지 여부를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>최대 첨부 파일 크기</p></td>
<td><p>이 설정은 모바일 장치에 다운로드할 수 있는 첨부 파일의 최대 크기를 제어합니다. 기본값은 무제한입니다.</p></td>
</tr>
<tr class="odd">
<td><p>최대 일정 기간 필터</p></td>
<td><p>이 설정은 모바일 장치에 동기화할 수 있는 최대 일정 기간을 지정합니다. 다음 값을 사용할 수 있습니다.</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>최대 전자 메일 기간 필터</p></td>
<td><p>이 설정은 모바일 장치에 동기화할 수 있는 전자 메일 항목의 최대 기간(일)을 지정합니다. 다음 값을 사용할 수 있습니다.</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>최대 전자 메일 본문 자르기 크기</p></td>
<td><p>이 설정은 모바일 장치에 동기화할 때 전자 메일 메시지가 잘리는 최대 크기를 지정합니다. 값은 KB(킬로바이트) 단위입니다.</p></td>
</tr>
<tr class="even">
<td><p>최대 전자 메일 HTML 본문 자르기 크기</p></td>
<td><p>이 설정은 모바일 장치에 동기화할 때 HTML 전자 메일 메시지가 잘리는 최대 크기를 지정합니다. 값은 KB(킬로바이트) 단위입니다.</p></td>
</tr>
<tr class="odd">
<td><p>최대 비활성 시간 잠금</p></td>
<td><p>이 값은 모바일 장치가 비활성 상태로 유지될 수 있는 시간을 지정하며, 이 시간이 지난 후에 장치를 다시 활성화하려면 암호가 필요합니다. 30초에서 1시간 사이의 간격을 입력할 수 있습니다. 기본값은 15분입니다.</p></td>
</tr>
<tr class="even">
<td><p>최대 암호 시도 실패 횟수</p></td>
<td><p>이 설정은 사용자가 모바일 장치에 올바른 암호를 입력하기 위해 시도할 수 있는 횟수를 지정합니다. 4에서 16까지의 숫자를 입력할 수 있으며 기본값은 8입니다.</p></td>
</tr>
<tr class="odd">
<td><p>최소 암호 복합 문자 수</p></td>
<td><p>이 설정은 모바일 장치 암호에 필요한 문자 집합의 수를 지정 합니다. 문자 집합은.</p>
<ul>
<li><p>소문자입니다.</p></li>
<li><p>대문자입니다.</p></li>
<li><p>0에서 9 사이의 숫자입니다.</p></li>
<li><p>특수 문자 (예: 느낌표)입니다.</p></li>
</ul>
<p>1에서 4까지의 숫자를 입력할 수 있으며 기본값은 1입니다.</p>
<p>Windows Phone 8 장치에 대 한이 설정은 암호에 필요한 문자 집합의 수를 지정 합니다. 예 3 값의 문자 집합의 모든 3에서 하나 이상의 문자가 필요합니다.</p>
<p>Windows Phone 10 장치에 대 한이 설정은 다음 암호 복잡성 요구 사항을 지정 합니다.</p>
<ol>
<li><p>숫자에만 해당 합니다.</p></li>
<li><p>숫자와 소문자입니다.</p></li>
<li><p>숫자, 소문자 대 문자와 대문자입니다.</p></li>
<li><p>숫자, 소문자, 대문자, 및 특수 문자.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>최소 암호 길이</p></td>
<td><p>이 설정은 모바일 장치 암호의 최소 문자 수를 지정합니다. 1에서 16까지의 숫자를 입력할 수 있으며 기본값은 4입니다.</p></td>
</tr>
<tr class="odd">
<td><p>암호 사용</p></td>
<td><p>이 설정은 모바일 장치 암호를 사용하도록 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p>암호 만료</p></td>
<td><p>이 설정을 사용하면 관리자가 모바일 장치 암호를 변경해야 하는 주기를 구성할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>암호 기록</p></td>
<td><p>이 설정은 사용자의 사서함에 저장될 수 있는 이전 암호의 개수를 지정합니다. 사용자는 저장된 암호를 다시 사용할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>암호 복구 사용</p></td>
<td><p>이 설정을 사용하도록 설정하면 모바일 장치가 서버에 전송되는 복구 암호를 생성합니다. 사용자가 모바일 장치 암호를 잊어버린 경우 복구 암호를 사용하여 모바일 장치를 잠금 해제할 수 있으며 새 모바일 장치 암호를 생성할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>장치 암호화 필요</p></td>
<td><p>이 설정은 장치에 암호화가 필요한지 여부를 지정합니다. <code>$true</code>로 설정할 경우 모바일 장치는 서버와 동기화하기 위해 암호화를 지원하고 구현할 수 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>암호화된 S/MIME 메시지 필요</p></td>
<td><p>이 설정은 S/MIME 메시지를 암호화해야 하는지 여부를 지정합니다. 기본값은 <code>$false</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>암호화 S/MIME 알고리즘 필요</p></td>
<td><p>이 설정은 S/MIME 메시지를 암호화할 때 사용해야 하는 필수 알고리즘을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>로밍 시 수동 동기화 필요</p></td>
<td><p>이 설정은 모바일 장치를 로밍 시 수동으로 동기화해야 하는지 여부를 지정합니다. 로밍 시 자동 동기화를 허용하면 모바일 장치 데이터 요금제의 데이터 비용이 예상보다 크게 지출되는 경우가 많습니다.</p></td>
</tr>
<tr class="odd">
<td><p>서명된 S/MIME 알고리즘 필요</p></td>
<td><p>이 설정은 메시지에 서명할 때 사용해야 하는 필수 알고리즘을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>서명된 S/MIME 메시지 필요</p></td>
<td><p>이 설정은 모바일 장치에서 서명된 S/MIME 메시지를 보내야 하는지 여부를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>저장소 카드 암호화 필요</p></td>
<td><p>이 설정은 저장소 카드를 암호화해야 하는지 여부를 지정합니다. 일부 모바일 장치 운영 체제는 저장소 카드 암호화를 지원하지 않습니다. 자세한 내용은 모바일 장치 및 모바일 운영 체제 설명서를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>승인되지 않은 InROM 응용 프로그램 목록</p></td>
<td><p>이 설정은 ROM에서 실행할 수 없는 응용 프로그램 목록을 지정합니다. 이 설정 값을 변경하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 필요합니다.</p></td>
</tr>
</tbody>
</table>


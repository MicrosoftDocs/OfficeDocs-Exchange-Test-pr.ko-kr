---
title: 'Exchange ActiveSync의 정보 권한 관리: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync의 정보 권한 관리
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50484436
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange ActiveSync의 정보 권한 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

정보 근로자가 전자 메일을 사용하여 중요한 정보를 교환하는 경우가 많습니다. 이 정보를 안전하게 보호하려면 조직에서 IRM(정보 권한 관리)을 사용하여 메시징 콘텐츠에 영구 보호를 적용할 수 있습니다. 모바일 장치를 사용하여 전자 메일에 액세스하는 경우가 점점 늘어나고 있으므로 모바일 장치 사용자가 IRM으로 보호된 콘텐츠를 만들고 사용할 수 있는 것이 중요합니다.

**목차**

Exchange 2013의 모바일 IRM 보호 기능

Requirements

Security

Enabling IRM in Exchange ActiveSync

IRM과 관련된 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

## Exchange 2013의 모바일 IRM 보호 기능

Exchange 2013 Microsoft Exchange ActiveSync 에서 IRM 하면 사용자가 AD RMS 권한 구성 또는 컴퓨터에는 장치를 연결 하 고, IRM에 대 한 활성화 하지 않고 모든 지원 되는 Exchange ActiveSync 장치에서 풍부한 IRM 기능에 액세스할 수 있습니다. 또한 모바일 장치 Windows 실행 되 고 필요가 없습니다. Exchange ActiveSync 는 모바일 장치 제조업체, original equipment manufacturer (), 및 다른 사용자를 Microsoft에서 어떠한 됩니다. 현재 Exchange ActiveSync 정식 사용자의 목록에 대 한 [Microsoft 기술 라이선스](https://go.microsoft.com/fwlink/p/?linkid=198562) 페이지에서 "Exchange ActiveSync 프로토콜" 섹션을 확장 합니다.

다음과 같은 요구 사항이 적용됩니다.

  - 조직의 클라이언트 액세스 서버가 UNRESOLVED\_TOKEN\_VAL(exExchange2010) SP1 이상을 실행하고 있어야 합니다.

  - 조직에 AD RMS 서버를 배포해야 합니다.

  - 내부 메시지에 대해 IRM을 사용하도록 설정해야 합니다. 이는 UNRESOLVED\_TOKEN\_VAL(exExchange2010)의 모든 IRM 기능에 대한 선행 조건입니다. 자세한 내용은 [내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)를 참조하십시오.

Exchange ActiveSync 사서함 정책에서 IRM을 사용하도록 설정해야 합니다. 서로 다른 Exchange ActiveSync 사서함 정책을 사용하여 각 사용자 집합에 대해 IRM을 사용하거나 사용하지 않도록 설정할 수 있습니다.

## 요구 사항

맨 위로 이동

  - 조직에서 클라이언트 액세스 서버를 실행 해야 Exchange 2010 SP1 이상입니다.

  - Exchange ActiveSync에서 IRM을 사용하도록 설정하면 클라이언트 액세스 서버가 지원되는 모바일 장치에서 액세스할 수 있도록 메시지를 제공하기 전에 IRM으로 보호된 메시지의 암호를 해독합니다. 동기화 시 IRM으로 보호된 메시지는 암호화되지 않은 형식으로 모바일 장치에 상주합니다. IRM 보호는 모바일 장치의 IRM 가능 전자 메일 클라이언트 응용 프로그램에서 적용합니다.

  - 내부 메시지에 IRM은 사용할 수 있어야 합니다. Exchange 2010 의 모든 IRM 기능에 대 한 필수 구성 요소입니다. 자세한 내용은 [내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)를 참조 합니다.

  - Exchange ActiveSync에서 IRM을 사용하도록 설정하는 경우 다음 표의 Exchange ActiveSync 정책 설정을 사용하여 모바일 장치 보안을 지원하는 것이 좋습니다.

  - 장치를 지 원하는 Exchange ActiveSync 프로토콜 버전 Windows 전화를 포함 하 여 14.1 Exchange ActiveSync 에서 IRM을 지원할 수 있습니다. 장치의 모바일 전자 메일 응용 프로그램 Exchange ActiveSync 버전 14.1에에서 정의 된 RightsManagementInformation 태그를 지원 해야 합니다.

설정

## 보안

New-ActiveSyncMailboxPolicy cmdlet을 사용하여 구성

Exchange ActiveSync 에서 IRM 클라이언트 액세스 서버에서 IRM으로 보호 된 첨부 파일 암호를 해독 하지 않습니다. IRM으로 보호 된 파일에 대 한 액세스를 만들거나 파일을 보려면 사용 되는 응용 프로그램에 의해 적용 됩니다. 예, Windows 휴대폰에서 [Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121)하 여 Microsoft Office 파일에 대 한 IRM 보호 적용 됩니다. IRM으로 보호 된 Office 파일에 액세스 하려면 사용자 컴퓨터에는 장치를 연결 하 고 Office 모바일 RMS 서버를 활성화 해야 합니다.

**암호 필요** 확인란을 선택합니다.

### Exchange ActiveSync 정책 설정

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>모바일 장치에 대해 암호화를 사용하도록 설정합니다.</th>
<th><strong>암호 필요</strong> 확인란을 선택한 다음 <strong>장치에서 암호화 필요</strong> 확인란을 선택합니다.</th>
<th><em>RequireDeviceEncryption</em> 매개 변수를 <code>$true</code>로 설정합니다.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequireDeviceEncryption</em> 매개 변수를 <code>$true</code>로 설정하면 장치 암호화를 지원하지 않는 모바일 장치는 연결할 수 없습니다.</p></td>
<td><p>지원 불가 모바일 장치가 Exchange 서버와 동기화될 수 없게 합니다.</p></td>
<td><p><strong>지원 불가 장치 허용</strong> 확인란을 선택 취소합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowNonProvisionableDevices</em> 매개 변수를 <code>$false</code>로 설정합니다.</p></td>
<td><p>자세한 내용은 <a href="mobile-device-mailbox-policies-exchange-2013-help.md">모바일 장치 사서함 정책</a>을 참조하십시오.</p></td>
<td><p>맨 위로 이동</p>

> [!IMPORTANT]
> <CODE>$true</CODE>를 <EM>RequireDeviceEncryption</EM> 매개 변수를 설정 하면 장치 암호화를 지원 하지 않는 모바일 장치 연결할 수 없습니다.


</td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync에서 IRM을 사용하도록 설정하려면 다음 작업을 수행합니다.</p></td>
<td><p>페더레이션 사서함(Exchange 2013 및 UNRESOLVED_TOKEN_VAL(exExchange2010) 설치에서 만든 시스템 사서함)을 AD RMS의 Super Users 그룹에 추가합니다. 이를 통해 Exchange 2013 및 UNRESOLVED_TOKEN_VAL(exExchange2010) 서버는 IRM으로 보호된 메시지에 액세스할 수 있습니다. 자세한 내용은 <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.</a>를 참조하십시오.</p></td>
<td><p>Exchange 관리 셸의 <a href="https://technet.microsoft.com/ko-kr/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a> cmdlet을 사용하여 클라이언트 액세스 서버에서 IRM을 사용하도록 설정합니다. 그러면 조직에 대해 Exchange ActiveSync의 IRM과 Microsoft OfficeOutlook Web App의 IRM이 사용하도록 설정됩니다. 자세한 내용은 <a href="enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md">클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


자세한 내용은 [모바일 장치 사서함 정책](mobile-device-mailbox-policies-exchange-2013-help.md)를 참조 하십시오.

맨 위로 이동

## Exchange ActiveSync의 IRM을 사용 하도록 설정

Exchange ActiveSync 에서 IRM을 사용 하려면 다음 작업을 수행 합니다.

1.  AD RMS에 고급 사용자 그룹에는 페더레이션 사서함 ( Exchange 2013 및 Exchange 2010 설치 하 여 만든 시스템 사서함)를 추가 합니다. 따라서 Exchange 2013 및 Exchange 2010 서버를 IRM으로 보호 된 메시지에 액세스할 수 있습니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조 합니다.

2.  Exchange 관리 셸 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) cmdlet을 사용 하 여 클라이언트 액세스 서버에서 IRM을 사용 하도록 설정 합니다. 이 통해 IRM Exchange ActiveSync 및 IRM에서 조직에 대 한 Microsoft OfficeOutlook Web App 에 있습니다. 자세한 내용은 [클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)를 참조 합니다.

맨 위로 이동


---
title: 'Windows 전화 및 장치에 대 한 모바일 장치 사서함 정책 지원: Exchange 2013 Help'
TOCTitle: Windows 전화 및 장치에 대 한 모바일 장치 사서함 정책 지원
ms:assetid: d76b1d4c-d1f6-4501-a7c9-854327aceda5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ983805(v=EXCHG.150)
ms:contentKeyID: 52058139
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows 전화 및 장치에 대 한 모바일 장치 사서함 정책 지원

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Windows Phone 8, Windows 8 및 Windows RT 릴리스마다 Exchange ActiveSync 및 모바일 장치 사서함 정책을 지 원하는 장치의 수가 있습니다. 각 장치 운영 체제에는 특정 모바일 장치 사서함 정책 설정 집합을 지원합니다.

## Windows 클라이언트와 Exchange Server 호환성 표

다음 표에 다양 한 버전의 Windows Phone, Windows 8, Windows RT 및 Exchange 서버에 대 한 호환 되는 모바일 장치 사서함 정책 매개 변수를 나열 합니다.

## Windows Phone 7 지원 정책 매개 변수

다음 표에 Windows Phone 7에 대 한 모바일 장치 사서함 정책 설정 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
</tr>
<tr class="even">
<td><p>MinPasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>PasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
<tr class="even">
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
</tr>
<tr class="even">
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
</tr>
<tr class="odd">
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
</tr>
<tr class="even">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
</tbody>
</table>


## Windows Phone 8 지원 정책 매개 변수

다음 표에 Windows Phone 8에 대 한 모바일 장치 사서함 정책 설정 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="even">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p>IRMEnabled</p></td>
<td><p>IRMEnabled</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


## Windows 8 및 Windows RT 지원 정책 매개 변수

다음 표에 Windows 8 및 Windows 직각에 대 한 모바일 장치 사서함 정책 설정


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="odd">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="even">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="odd">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


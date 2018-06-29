---
title: 'Exchange에서 기본 검색 사서함 삭제 및 다시 만들기: Exchange 2013 Help'
TOCTitle: Exchange에서 기본 검색 사서함 삭제 및 다시 만들기
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371328
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange에서 기본 검색 사서함 삭제 및 다시 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-05-04_

Exchange 관리 셸을 사용하여 기본 검색 사서함을 삭제한 후 다시 만든 다음 사용 권한을 할당할 수 있습니다.

## 이 작업을 수행하려는 이유는 무엇입니까?

Exchange Server 2013 및 Exchange Online 기본 검색 사서함의 최대 크기는 50GB입니다. 원본 위치 eDiscovery 검색 결과 저장 하는데 사용 됩니다. 크기 제한을 변경, 전에 조직 수 50GB 이상에 저장소 할당량을 늘릴 수 있습니다. 결과적으로 검색 사서함 50GB 이상의 커질 수 있습니다. 50GB 보다 큰 기본 검색 사서함이 있는 문제를 세 가지가 있습니다.

  - 지원되지 않습니다.

  - Office 365로 마이그레이션할 수 없습니다.

  - Exchange Server 2010 에서 기본 검색 사서함 있으면 Exchange Server 2013 으로 업그레이드할 수 없습니다.

이 문제를 해결하는 방법은 50GB를 초과하는 기본 검색 사서함의 검색 결과를 저장할지 여부에 따라 다릅니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이 검색 결과를 저장하시겠습니까?</th>
<th>수행 작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>아니요</p></td>
<td><p>이 항목의 단계에 따라 기본 검색 사서함을 삭제한 후 다시 만듭니다.</p></td>
</tr>
<tr class="even">
<td><p>예</p></td>
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Exchange에서 검색 사서함의 크기 줄이기</a>의 단계를 따릅니다.</p></td>
</tr>
</tbody>
</table>


## Exchange 관리 셸 를 사용 하 여 삭제 하 고 다시 기본 검색 사서함을 만들려면


> [!NOTE]
> 검색 사서함 EAC에 표시 되지 않으므로 Exchange 관리 센터 (EAC) 사용할 수 없습니다.



1.  다음 명령을 실행하여 기본 검색 사서함을 삭제합니다.
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  사서함 및 해당 Active Directory 사용자 개체를 삭제할지 확인하는 메시지가 표시되면 **Y**를 입력한 후 Enter 키를 누릅니다.
    
    다음 단계에서는 검색 사서함을 만들 때 새 사용자 개체가 Active Directory에 만들어집니다.

3.  다음 명령을 실행하여 기본 검색 사서함을 다시 만듭니다.
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  다음 명령을 실행하여 Discovery Management 역할 그룹 사용 권한을 할당하고 기본 검색 사서함을 열어서 검색 결과를 확인합니다.
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all


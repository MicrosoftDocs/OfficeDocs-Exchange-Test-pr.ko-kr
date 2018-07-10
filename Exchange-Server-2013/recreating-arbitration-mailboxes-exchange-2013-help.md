---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518123
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**마지막으로 수정된 항목:** 2018-01-17_

**요약:**  Exchange 2013 및 다시 만드는 방법에 대 한 중재 사서함에 대 한 합니다.

Exchange 2013 *중재 사서함*라고 하는 5 개의 시스템 사서함 함께 제공 됩니다. 중재 사서함 메시징 승인 워크플로 관리 하기 위한 다양 한 유형의 시스템 데이터를 저장 하기 위해 사용 됩니다. 차트 아래 각 유형의 중재 사서함 및 해당 책임을 나열 합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>중재 사서함 이름</th>
<th>표시 이름</th>
<th>지속 된 기능</th>
<th>기능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Microsoft Exchange 페더레이션 사서함</p></td>
<td><p>{}</p></td>
<td><p>이 사서함이 다른 Exchange 조직 간의 연결을 유지 하기 위해 사용 되는 데이터를 저장 합니다. 권한 관리 서비스, 크로스-프레미스 메일 흐름 모니터링 프로브 및 응답, 알림, 포함 온라인 보관 함, 메시징 레코드 관리 및 크로스-프레미스 약속 있음/없음 정보입니다.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Microsoft Exchange 승인 도우미</p></td>
<td><p>{}</p></td>
<td><p>이 사서함 받는 사람 중재 및 자동 그룹 승인 요청에 대 한 Exchange 승인 프레임 워크에서 사용 하기 위해 프로 비전 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Microsoft Exchange 마이그레이션</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>일괄 처리의 사서함을 이동할 때 사용 하 여 Exchange 마이그레이션 서비스에 대 한 데이터를 저장 합니다.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>시스템 사서함을 검색 합니다.</p>
<p>지정 된 선택 영역이 조건과 일치 하는 메시지를 찾으려고 규정 준수 관리자 등에서 사용 되는 e-검색 기능에 의해 사용 하기 위해 프로 비전 합니다. 이 사서함도 통합 메시징에서 UM 콘솔 참석 파일 및 기타 정보를 저장 하기 위해 사용 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>이 조직의 사서함 이라고 합니다. 오프 라인 주소록 (Oab) 만들기 (영문)에 사용 됩니다. 지리적으로 별도 사이트에 걸쳐 포함 하 여 조직 전체에서 부하를 분산 OAB 생성 하려면 추가 조직의 사서함을 만들 수 있습니다.</p></td>
</tr>
</tbody>
</table>


하나 이상의 이러한 중재 사서함을 다시 만들려면 해야하는 경우 다음에 나오는 지침을 참조 합니다.

## 알고 있어야 시작 하기 전에

  - 예상 완료 시간: 프로시저 당 10 분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## Exchange 관리 셸 를 사용 하 여 중재 사서함을 다시 만들려면

특정 종류의 중재 사서함을 다시 만들려면 다음 지침을 따르십시오.


> [!NOTE]
> 다음 섹션의 모든 단계는 Exchange 설치 미디어의 압축을 푼 같은 디렉터리에서 실행 되어야 합니다.



## Microsoft Exchange 페더레이션 사서함을 다시 만들려면

중재 사서함 FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042 다시 만들려면

1.  모든 중재 사서함 누락 된 경우 다음 명령을 실행 합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 관리 셸 다음을 실행 합니다.
    
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"

## Microsoft Exchange 길잡이 승인 사서함을 다시 만들려면

SystemMailbox {1f05a927-9350-4efe-a823-5529c2d64109} 중재 사서함 다시 만들려면

1.  모든 중재 사서함 누락 된 경우 다음 명령을 실행 합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 관리 셸 다음을 실행 합니다.
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## Microsoft Exchange 마이그레이션 사서함을 다시 만들려면

중재 사서함 Migration.8f3e7716-2011-43e4-96b1-aba62d229136 다시 만들려면

1.  모든 중재 사서함 누락 된 경우 다음 명령을 실행 합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 관리 셸 다음을 실행 합니다.
    
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"

3.  Exchange 관리 셸 다음 명령을 실행 하 여 유지 기능 (msExchCapabilityIdentifiers)를 설정 합니다.
    
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force

## Microsoft Exchange 검색 시스템 사서함을 다시 만들려면

SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 중재 사서함 다시 만들려면

1.  다음 명령을 실행합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## Oab에 대 한 Microsoft Exchange 조직의 사서함을 다시 만들려면

SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c} 중재 사서함 다시 만들려면

1.  모든 중재 사서함 누락 된 경우 다음 명령을 실행 합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  Exchange 관리 셸 다음을 실행 합니다.
    
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"

3.  Exchange 관리 셸 다음 명령을 실행 하 여 유지 기능 (msExchCapabilityIdentifiers)를 설정 합니다.
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

완료 되 면 46, 47, 및 51 누락 된 표시 명령 `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` 를 실행 하는 경우 모든 기능을 다시 추가 하려면 다음 명령을 실행 합니다.

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## 작동 여부는 어떻게 확인합니까?

성공적으로 다시를 만들었다고 중재 사서함을 확인 하려면 시스템 사서함을 검색 하려면 *Arbitration* 스위치와 함께 **Get-Mailbox** cmdlet을 사용 합니다.

    Get-Mailbox -Arbitration | Format-Table Name, DisplayName

이름 또는 위의 테이블에서 표시 이름을 사용 하거나 해당 적절 한 시스템 사서함을 다시 만들어졌는지 확인 하려면 명령의 결과 보기


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



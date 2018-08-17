---
title: '검색 사서함 만들기: Exchange 2013 Help'
TOCTitle: 검색 사서함 만들기
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50484027
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검색 사서함 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013 설치는 기본적으로 검색 사서함을 만듭니다. Exchange Online 기본적으로 검색 사서함도 생성 됩니다. 검색 사서함은 Exchange 관리 센터 (EAC) [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md) 검색에 대 한 대상 사서함으로 사용 됩니다. 필요에 따라 추가 검색 사서함을 만들 수 있습니다. 새 검색 사서함을 만든 후에 검색 사서함으로 복사 되는 eDiscovery 검색 결과 액세스할 수 있도록 적절 한 사용자에 대 한 전체 액세스 권한을 할당 해야 합니다.


> [!WARNING]
> 검색 관리자가 eDiscovery 검색의 결과를 검색 사서함에 복사하면 사서함은 중요한 정보를 잠재적으로 포함할 수 있습니다. 검색 사서함에 대한 액세스를 제어하고 인증된 사용자만 검색 사서함에 액세스하도록 해야 합니다.



자세한 내용은 [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md)을 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "검색 사서함 만들기" 항목.

  - 검색 사서함의 사서함 저장소 할당량은 50GB(기가바이트)입니다. 이 저장소 할당량은 늘릴 수 없습니다.

  - EAC를 사용 하 여 검색 사서함 만들기에 대 한 액세스 권한을 할당 하거나 수는 없습니다. 셸을 사용 하 여 해야 합니다. Office 365Exchange Online 조직에 연결 된 원격 PowerShell을 사용 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## (선택 사항) 1 단계: 원격 PowerShell을 사용 하는 Exchange Online에 연결

Exchange Online 또는 Office 365 조직이 있는 경우이 단계를 수행 해야 합니다. Exchange Server 2013 조직이 있는 경우에 다음 단계로 이동 하 고 Exchange 관리 셸 에서 명령을 실행 합니다.

1.  로컬 컴퓨터에서 Windows PowerShell을 열고 다음 명령을 실행합니다.
    
        $UserCredential = Get-Credential
    
    **Windows PowerShell 자격 증명 요청** 대화 상자에서 Office 365 전역 관리자 계정의 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.

2.  다음 명령을 실행합니다.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  다음 명령을 실행합니다.
    
        Import-PSSession $Session

4.  Exchange Online 조직에 연결 하려는 있는지를 확인 하려면 조직에 있는 모든 사서함의 목록을 가져오려면 다음 명령을 실행 합니다.
    
        Get-Mailbox

자세한 내용은 하거나 Exchange Online 조직에 연결할 때 문제가 있으면 [원격 PowerShell을 사용 하는 Exchange Online에 연결](https://go.microsoft.com/fwlink/p/?linkid=517283)을 참조 하십시오.

## 2 단계: 검색 사서함 만들기

이 예에서는 검색 사서함 SearchResults를 만듭니다.

    New-Mailbox -Name SearchResults -Discovery 

구문과 매개 변수에 대한 자세한 내용은 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\))를 참조하십시오.

Exchange 조직의 모든 검색 사서함 목록을 표시하려면 다음 명령을 실행합니다.

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.

## 3 단계: 검색 사서함에 사용 권한 할당

사용자 또는 그룹 사용자가 만든 검색 사서함을 열에 필요한 권한 명시적으로 할당 해야 합니다. 검색 사서함을 열고 검색 결과 볼 수는 사용자 또는 그룹 사용 권한을 할당 하려면 다음 구문을 사용 하십시오.

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

예를 들어 다음 명령은 Litigation Managers 그룹의 구성원이 Fabrikam Litigation 검색 사서함을 열 수 있도록 해당 그룹에 모든 권한을 할당합니다.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

구문과 매개 변수에 대한 자세한 내용은 [Add-MailboxPermission](https://technet.microsoft.com/ko-kr/library/bb124097\(v=exchg.150\))를 참조하십시오.

## 추가 정보

  - 기본적으로 검색 관리 역할 그룹의 구성원에게만 기본 사서함 검색에 대한 모든 권한이 있습니다. 검색 관리 역할 그룹의 구성원이 만들어진 검색 사서함을 열 수 있도록 하려면 해당 그룹에 모든 권한을 명시적으로 할당해야 합니다.

  - 검색 사서함이 Exchange 주소 목록에 표시되지만 사용자가 검색 사서함에 전자 메일을 보낼 수는 없습니다. 검색 사서함에 대한 전자 메일 배달은 배달 제한을 통해 금지됩니다. 따라서 검색 사서함에 복사되는 검색 결과의 무결성이 유지됩니다.

  - 검색 사서함은 용도가 변경되거나 다른 사서함 유형으로 변환될 수 없습니다.

  - 검색 사서함은 다른 사서함 유형과 마찬가지로 제거될 수 있습니다.


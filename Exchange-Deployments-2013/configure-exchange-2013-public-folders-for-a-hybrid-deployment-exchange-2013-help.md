---
title: '하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성: Exchange 2013 Help'
TOCTitle: 하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65296577
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

**요약:** 온-프레미스 Exchange 2013 환경에서 공용 폴더에 액세스 하려면 Exchange Online 사용자를 사용 하도록 설정 하는 것에 대 한 지침입니다.

하이브리드 배포에서 Exchange Online, 온-프레미스, 또는 둘 모두에 사용자가 될 수 있습니다 하 고 공용 폴더는 하거나 Exchange Online 또는 온-프레미스 합니다. 경우에 따라 온라인 사용자가 Exchange Server 2013 온-프레미스 환경에서 공용 폴더에 액세스 해야 합니다. 마찬가지로, Exchange 2013 사용자가 Office 365 또는 Exchange Online의 공용 폴더에 액세스 해야 합니다.


> [!NOTE]
> Exchange 2010 또는 Exchange 2007 공용 폴더를 사용 하는 경우 <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">하이브리드 배포용으로 레거시 온-프레미스 공용 폴더 구성</A>를 참조 하십시오.



이 문서에서는 2013 Exchange 공용 폴더에 액세스 하 여 Exchange Online/Office 365 사용자를 활성화 하는 방법에 설명 합니다. 온-프레미스 Exchange 2013 사용자가 Exchange Online 공용 폴더에 액세스할 수 있도록 [하이브리드 배포에 대 한 Exchange Online 공용 폴더 구성](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)를 참조 하십시오.

Exchange Online/Office 365 사용자를 Exchange 2013 공용 폴더에 액세스 하기 위해 Exchange 온-프레미스 환경에서 메일 사용자 개체에 의해 표현 되어야 합니다. 메일 사용자 개체에이 대상 Exchange 2013 공용 폴더 계층 구조에 대 한 로컬 수도 있어야 합니다. Office 365 사용자에 게 현재 없는 메일 사용자 개체에 의해 온-프레미스를 표시 해야 하는 경우, 일치 하는 온-프레미스 엔터티를 만들려는 3106618 ["Exchange Online 사용자가 레거시 온-프레미스 공용 폴더에 액세스할 수 없습니다"](https://go.microsoft.com/fwlink/p/?linkid=699451) Microsoft 기술 자료 문서를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

1.  이러한 지침에서는 하이브리드 구성 마법사를 사용하여 온-프레미스 및 Exchange Online 환경을 구성하고 동기화했으며, 사용자 대부분의 자동 검색에 사용되는 DNS 레코드가 온-프레미스 끝점을 참조한다고 가정합니다. 자세한 내용은 [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)를 참조하십시오.

2.  이러한 지침 및 온-프레미스 Exchange 서버에서 기능 활성화가 외부에서 Outlook 사용 하는 것으로 가정 합니다. 외부에서 Outlook 사용을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Outlook Anywhere](https://technet.microsoft.com/ko-kr/library/bb123741\(v=exchg.150\))을 참조 하십시오.

3.  Office 365와 함께 exchange 하이브리드 배포에 대 한 공용 폴더 공존 성을 구현 가져오기 절차 중 충돌을 해결 해야 할 수 있습니다. 충돌은 라우팅할 수 없는 전자 메일 주소를 메일 사용된 공용 폴더, 충돌을 다른 사용자 및 Office 365 및 기타 특성에는 그룹에 할당으로 인해 발생할 수 있습니다.

4.  프레미스 간 공용 폴더에 액세스하려면 사용자는 Outlook 클라이언트를 2012년 11월 Outlook 공개 업데이트 이상으로 업그레이드해야 합니다.
    
    1.  다운로드 하려면 2012 년 11 월 Outlook 업데이트 Outlook 2010에 대 한 [Microsoft Outlook 2010 (KB2687623) 32 비트 버전에 대 한 업데이트](https://www.microsoft.com/en-us/download/details.aspx?id=35702)를 참조 하십시오.
    
    2.  다운로드 하려면 2012 년 11 월 Outlook 업데이트 Outlook 2007 용 [Microsoft Office Outlook 2007 (KB2687404)에 대 한 업데이트](https://www.microsoft.com/en-us/download/details.aspx?id=35718)를 참조 합니다.

5.  Mac 용 outlook 2011 및 Mac 용 Office 365에 대 한 Outlook 크로스-프레미스 공용 폴더에 대 한 지원 되지 않습니다. 사용자가 액세스할 수와 Outlook 2011 Mac 또는 Outlook for Mac 용 Office 365에 대 한 공용 폴더와 같은 위치에 있어야 합니다. 또한 사서함이 Exchange Online 사용자는 Outlook Web App 를 사용 하 여 온-프레미스 공용 폴더에 액세스할 수 없습니다.
    

    > [!NOTE]
    > Mac 용 outlook 2016 크로스-프레미스 공용 폴더에 대 한 지원 됩니다. 조직의 클라이언트에서에서 Outlook 2016 for Mac을 사용 하는 경우 2016 년 4 월 업데이트를 설치한 있는지 확인 합니다. 그렇지 않은 경우 해당 사용자가 하이브리드 토폴로지에서 공용 폴더에 액세스할 수 없습니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/mt788631(v=exchg.150)">Mac 용 Outlook 2016와 공용 폴더 액세스 (영문)</A>을 참조 하십시오.



## 1 단계: 스크립트 다운로드

1.  [메일 사용이 가능한 공용 폴더-디렉터리 동기화 스크립트](https://www.microsoft.com/en-us/download/details.aspx?id=46381)에서 다음 파일을 다운로드 합니다.
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 파일을 저장합니다.

## 2 단계: 디렉터리 동기화를 구성 합니다.

디렉터리 동기화 서비스는 메일 사용이 가능한 공용 폴더를 동기화 하지 않습니다. 다음 스크립트를 실행 하는-프레미스 및 Office 365 메일 사용이 가능한 공용 폴더를 동기화 합니다. 메일 사용이 가능한 공용 폴더에 할당 된 특정 권한 크로스-프레미스 권한 하이브리드 배포 시나리오에서 지원 되지않는 이후 클라우드에서 다시 만들어야 할 수 있습니다. 자세한 내용은 [Exchange Server 2013 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조 하십시오.


> [!NOTE]
> 동기화 된 메일 사용이 가능한 공용 폴더는 메일 연락처 개체에 대 한 메일 흐름 목적으로 하 고 EExchange 관리 센터 에서 볼 수 표시 됩니다. Get-MailPublicFolder 명령을 참조 하십시오. 클라우드에서 SendAs 사용 권한을 다시, Add-recipientpermission 명령을 사용 합니다.



1.  Exchange 2013 서버에서 메일 사용이 가능한 공용 폴더를 동기화 로컬 온-프레미스 Active Directory에서 O365에 다음 명령을 실행 합니다.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    로그 동기화 작업 및.csv 형식의 오류를 원하는 위치에 대 한 경로 Office 365 사용자 이름 및 암호를 및 `CsvSummaryFile``Credential` 입니다.


> [!NOTE]
> 스크립트를 실행 하기 전에 경우 먼저는 동작을 시뮬레이션할 스크립트 걸립니다 환경의 <CODE>-WhatIf</CODE> 매개 변수와 함께 위에서 설명한 대로를 실행 하 여는 것이 좋습니다.<BR>또한 메일 사용이 가능한 공용 폴더를 동기화 하려면이 스크립트를 매일 실행 하는 것이 좋습니다.



## 3 단계: Exchange 2013 온-프레미스 공용 폴더에 액세스 하려면 Exchange Online 사용자 구성

이 절차의 마지막 단계에는 Exchange online 조직을 구성 하 고 Exchange 2013 공용 폴더에 대 한 액세스를 허용 하도록입니다.

온-프레미스 공용 폴더에 액세스 하도록 exchange online 조직을 사용 하도록 설정 합니다. 온-프레미스 공용 폴더 사서함의 모든 가리킵니다 됩니다.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3


> [!NOTE]
> 변경 내용을 보려면 ActiveDirectory 동기화가 완료 될 때까지 기다려야 합니다. 이 프로세스를 완료 하려면 3 시간까지 걸릴 수 있습니다. 3 시간 마다 발생 하는 되풀이 동기화 될 때까지 기다리는 하지 않으려면 하는 경우에 언제 든 지 디렉터리 동기화를 강제로 수 있습니다. 디렉터리 동기화를 강제로 수행 하는 자세한 단계, <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">디렉터리 동기화를 강제로</A>을 참조 하십시오.



## 작동 여부는 어떻게 확인합니까?

1.  Exchange Online의 사용자로 Outlook에 로그온하여 다음 공용 폴더 테스트를 수행합니다.
    
      - 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.


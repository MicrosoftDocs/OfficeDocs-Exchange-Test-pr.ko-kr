---
title: '하이브리드 배포에 대 한 Exchange Online 공용 폴더 구성: Exchange 2013 Help'
TOCTitle: 하이브리드 배포에 대 한 Exchange Online 공용 폴더 구성
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72778049
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 하이브리드 배포에 대 한 Exchange Online 공용 폴더 구성

 

_<strong>적용 대상:</strong>Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong>2016-12-15_

**요약:**  사용 하도록 설정 하는 것에 대 한 지침 온-프레미스 Exchange 2013 사용자가 Exchange Online의 공용 폴더에 액세스할 수 있습니다.

하이브리드 배포에서 Exchange Online, 온-프레미스, 또는 둘 모두에 사용자 수 하 고 공용 폴더는 하거나 Exchange Online 또는 온-프레미스. 경우에 따라 온라인 사용자가 Exchange Server 2013 온-프레미스 환경에서 공용 폴더에 액세스 해야 합니다. 마찬가지로, Exchange 2013 사용자가 Office 365 또는 Exchange Online에 공용 폴더에 액세스 해야 합니다.

이 문서에서는 Exchange 2013 온-프레미스 환경에서 사용자가 Exchange Online/Office 365 공용 폴더에 액세스할 수 있도록 하는 방법에 설명 합니다. Exchange Online/Office 365 사용자가 온-프레미스 Exchange 2013 공용 폴더에 액세스할 수 있도록 [하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/set-up-modern-hybrid-public-folders)를 참조 하십시오.


> [!NOTE]
> Exchange 2010 또는 Exchange 2007 공용 폴더를 사용 하는 경우 <A href="https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders">하이브리드 배포용으로 레거시 온-프레미스 공용 폴더 구성</A>를 참조 하십시오.



## 시작하기 전에 알아야 할 내용

1.  이러한 지침에서는 하이브리드 구성 마법사를 사용하여 온-프레미스 및 Exchange Online 환경을 구성하고 동기화했으며, 사용자 대부분의 자동 검색에 사용되는 DNS 레코드가 온-프레미스 끝점을 참조한다고 가정합니다. 자세한 내용은 [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)를 참조하십시오.

2.  이러한 지침 및 온-프레미스 Exchange 서버에서 기능 활성화가 외부에서 Outlook 사용 하는 것으로 가정 합니다. 외부에서 Outlook 사용을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Outlook Anywhere](https://technet.microsoft.com/ko-kr/library/bb123741\(v=exchg.150\))을 참조 하십시오.

3.  Office 365와 함께 exchange 하이브리드 배포에 대 한 공용 폴더 공존 성을 구현 가져오기 절차 중 충돌을 해결 해야 할 수 있습니다. 충돌은 라우팅할 수 없는 전자 메일 주소를 메일 사용된 공용 폴더, 충돌을 다른 사용자 및 Office 365 및 기타 특성에는 그룹에 할당으로 인해 발생할 수 있습니다.

4.  프레미스 간 공용 폴더에 액세스하려면 사용자는 Outlook 클라이언트를 2012년 11월 Outlook 공개 업데이트 이상으로 업그레이드해야 합니다.
    
    1.  다운로드 하려면 2012 년 11 월 Outlook 업데이트 Outlook 2010에 대 한 [Microsoft Outlook 2010 (KB2687623) 32 비트 버전에 대 한 업데이트](https://www.microsoft.com/en-us/download/details.aspx?id=35702)를 참조 하십시오.
    
    2.  다운로드 하려면 2012 년 11 월 Outlook 업데이트 Outlook 2007 용 [Microsoft Office Outlook 2007 (KB2687404)에 대 한 업데이트](https://www.microsoft.com/en-us/download/details.aspx?id=35718)를 참조 합니다.

5.  Mac 용 outlook 2011 및 Mac 용 Office 365에 대 한 Outlook 크로스-프레미스 공용 폴더에 대 한 지원 되지 않습니다. 사용자가 액세스할 수와 Outlook 2011 Mac 또는 Outlook for Mac 용 Office 365에 대 한 공용 폴더와 같은 위치에 있어야 합니다. 또한 사서함이 Exchange Online 사용자는 Outlook Web App를 사용 하 여 온-프레미스 공용 폴더에 액세스할 수 없습니다.
    

    > [!NOTE]
    > Mac 용 outlook 2016 크로스-프레미스 공용 폴더에 대 한 지원 됩니다. 조직의 클라이언트에서에서 Outlook 2016 for Mac을 사용 하는 경우 2016 년 4 월 업데이트를 설치한 있는지 확인 합니다. 그렇지 않은 경우 해당 사용자가 공존 또는 하이브리드 토폴로지에서 공용 폴더에 액세스할 수 없습니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/mt788631(v=exchg.150)">Mac 용 Outlook 2016와 공용 폴더 액세스 (영문)</A>을 참조 하십시오.



## 단계 1: 스크립트 다운로드

1.  [메일 사용이 가능한 공용 폴더-prem에서 스크립트를 EXO에서 디렉터리 동기화](https://go.microsoft.com/fwlink/p/?linkid=797795)에서 다음 파일을 다운로드 합니다.
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 파일을 저장합니다.

## 2 단계: 디렉터리 동기화를 구성 합니다.

`Sync-MailPublicFoldersCloudToOnprem.ps1` 스크립트 실행 하는 Exchange Online 및 Exchange 2013 온-프레미스 환경 간의 메일 사용이 가능한 공용 폴더를 동기화 합니다. 메일 사용이 가능한 공용 폴더에 할당 된 특정 권한 크로스-프레미스 권한 하이브리드 배포 시나리오에서 지원 되지않는 이후 클라우드에서 다시 만들어야 할 수 있습니다. 자세한 내용은 [Exchange Server 2013 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조 하십시오.


> [!NOTE]
> 동기화 된 메일 사용이 가능한 공용 폴더는 흐름 목적으로 메일에 대 한 연락처 개체를 메일 하 고 볼 수는 Exchange 관리 센터에 표시 됩니다. Get MailPublicFolder 명령을 참조 하십시오. 클라우드에서 SendAs 사용 권한을 다시를 Add-recipientpermission 명령을 사용 합니다.



1.  Exchange 2013 서버에서 메일 사용이 가능한 공용 폴더를 동기화 Exchange Online/Office 365에서 로컬 온-프레미스 Active directory에 다음 명령을 실행 합니다.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    여기서 `Credential` 는 Office 365 사용자 이름 및 암호입니다.


> [!NOTE]
> 메일 사용이 가능한 공용 폴더를 동기화 하는 매일이 스크립트를 실행 하는 것이 좋습니다.



## 3 단계: 온-프레미스 사용자가 Exchange Online 공용 폴더에 액세스할 수를 구성 합니다.

이 절차의 마지막 단계는 Exchange Online 공용 폴더에 대 한 액세스를 허용 하도록 Exchange 2013 온-프레미스 조직을 구성 하는 것입니다.

`Import-PublicFolderMailboxes.ps1` 스크립트 실행 합니다 개체를 가져올 공용 폴더 사서함 클라우드에서 메일 사용이 가능한 사용자로 온-프레미스 환경에입니다. 또한 스크립트 원격 공용 폴더 사서함으로 가져온된 개체를 구성 합니다.

1.  Exchange 2013 서버에서 온-프레미스 Active directory에서 클라우드의 공용 폴더 사서함 개체를 가져오려면 다음 명령을 실행 합니다.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    여기서 `Credential` 는 Office 365 사용자 이름 및 암호입니다.
    

    > [!NOTE]
    > 자동으로 여러 새 사서함으로 분할 때마다 공용 폴더 사서함을 자신의 임계값 용량에 도달 하기 때문에 공용 폴더 사서함 개체를 가져오려면이 스크립트를 매일 실행 하는 것이 좋습니다. 따라서 항상 하려는 클라우드에서 가장 최근의 공용 폴더 사서함을 가져온 확인 합니다.



2.  Exchange Online 공용 폴더에 액세스 하도록 Exchange 2013 온-프레미스 조직 사용 하도록 설정 합니다.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote


> [!NOTE]
> 변경 내용을 보려면 ActiveDirectory 동기화가 완료 될 때까지 기다려야 합니다. 이 프로세스를 완료 하려면 3 시간까지 걸릴 수 있습니다. 3 시간 마다 발생 하는 되풀이 동기화 기다리지 않으려면 언제 든 지 디렉터리 동기화를 강제로 수 있습니다. 디렉터리 동기화를 강제로 수행 하는 자세한 단계, <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">디렉터리 동기화를 강제로</A>을 참조 하십시오.



## 작동 여부는 어떻게 확인합니까?

1.  Exchange Online의 사용자로 Outlook에 로그온하여 다음 공용 폴더 테스트를 수행합니다.
    
      - 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.


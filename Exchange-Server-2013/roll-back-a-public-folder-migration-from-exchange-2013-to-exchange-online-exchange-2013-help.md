---
title: '공용 폴더 마이그레이션 롤백 Exchange 2013에서 Exchange Online으로: Exchange 2013 Help'
TOCTitle: 공용 폴더 마이그레이션 롤백 Exchange 2013에서 Exchange Online으로
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432740
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더 마이그레이션 롤백 Exchange 2013에서 Exchange Online으로

 

_**마지막으로 수정된 항목:** 2017-03-20_

**요약:**  마이그레이션 전 상태로 Exchange 2013 온-프레미스 조직에서 공용 폴더 인프라를 반환 하려면 다음이 단계를 수행 합니다.

를 실행 하면 문제에 공용 폴더 마이그레이션와 Exchange online 또는 Exchange 2013 공용 폴더를 다시 활성화 하려면 다른 이유 필요성에 대 한 경우 다음 단계를 수행 합니다.

## 마이그레이션 롤백

Note 마이그레이션 롤백 Exchange 온라인 마이그레이션, 클라이언트를 통해 또는 메일 사용이 가능한 공용 폴더에 대 한 전자 메일을 통해 후 공용 폴더에 추가 된 모든 콘텐츠 손실 됩니다. 이 콘텐츠를 저장 하려면 다음 가져올 수 있는 온-프레미스 공용 폴더에는 롤백 완료 되 면.pst 파일로 마이그레이션 후 공용 폴더 콘텐츠를 내보낼 수 있습니다.

1.  Exchange 온-프레미스 환경에서 Exchange 2013 공용 폴더 (몇 시간이 걸릴 수의 잠금을 해제 하는 내용의) 잠금을 해제 하려면 다음 명령을 실행 합니다.
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Exchange 온-프레미스 환경에서 SetMailPublicFolderExternalAddress.ps1 하 여 업데이트 된 모든 메일 사용이 가능한 공용 폴더의 `ExternalEmailAddress` 되돌리기 (에 사용 되는 스크립트 *8 단계: 테스트 Exchange Online의 공용 폴더의 잠금을 해제 하 고*[마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)의). 수정 된 오류를 식별 하는 스크립트에 의해 생성 되는 요약 파일을 참조 하거나 동일한 일괄 처리 migriont 프로세스 초반에 생성 되는 파일 OnPrem\_MEPF.xml 파일을 사용 하 여 모든 메일 사용이 가능한 공용 폴더에 대 한 원래 속성을 가져올 수 있습니다.

3.  Exchange Online PowerShell에서 모든 Exchange Online 공용 폴더와 사서함을 제거 하려면 다음 명령을 실행 합니다.
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  공용 폴더 트래픽을 온-프레미스 (Exchange 2013)로 다시 리디렉션 Exchange Online 환경에서 다음 명령을 실행 합니다.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Exchange Online 사용자에 게 액세스할 수 있도록 온-프레미스 공용 폴더에 대 한 액세스를 다시 구성에 대 한 자세한 내용 은 [하이브리드 배포에 대 한 Exchange 2013 공용 폴더 구성](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md) 참조 하십시오.


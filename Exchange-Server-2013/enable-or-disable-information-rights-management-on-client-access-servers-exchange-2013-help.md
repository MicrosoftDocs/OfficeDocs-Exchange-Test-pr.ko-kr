---
title: '클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50484131
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

클라이언트 액세스 서버에서 IRM(정보 권한 관리)을 사용하도록 설정하면 다음 기능을 사용할 수 있습니다.

  - Microsoft Office Outlook Web App

  - Microsoft Exchange ActiveSync의 IRM

클라이언트 액세스 서버에서 IRM 사용 하는 경우 Outlook Web App 사용자가 AD RMS 클러스터에서 만든 [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 템플릿을 적용 하 여 IRM 보호 메시지 수입니다. Outlook Web App 사용자가 IRM으로 보호 된 메시지를 볼 수도 및 첨부 파일을 지원 합니다. 클라이언트 액세스 서버에서 IRM을 사용 하도록 설정 하기 전에 AD RMS 클러스터에서 고급 사용자 그룹에는 페더레이션 사서함을 추가 해야 합니다.


> [!IMPORTANT]
> Super Users 그룹의 구성원이 AD RMS 클러스터에 라이선스를 요청할 경우 소유주 사용권이 부여됩니다. 이를 통해 클러스터에서 RMS로 보호된 모든 콘텐츠의 암호를 해독할 수 있습니다.



IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "IRM(정보 권한 관리) 구성" 항목

  - Active Directory 포리스트에 AD RMS 클러스터가 설치되어 있어야 합니다.

  - 페더레이션 사서함이 AD RMS 슈퍼 사용자 그룹에 추가되었습니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조하십시오.

  - IRM 기능이 조직에 대해 사용하도록 설정되어 있어야 합니다. 자세한 내용은 [내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)을 참조하십시오.

  - **Set-IRMConfiguration** cmdlet을 사용하여 전체 Outlook Web App 조직 또는 특정 수준에 대해 Exchange ActiveSync의 IRM과 Exchange의 IRM을 사용하거나 사용하지 않도록 설정할 수 있습니다.
    
    다음 수준에서 Outlook Web App의 IRM을 제어할 수 있습니다.
    
      - **Outlook Web App 가상 디렉터리별**   Outlook Web App 가상 디렉터리에 대해 Outlook Web App의 IRM을 사용하거나 사용하지 않도록 설정하려면 **Set-OWAVirtualDirectory** cmdlet을 사용하고 *IRMEnabled* 매개 변수를 `$false` 또는 `$true`(기본값)로 설정합니다. 그러면 Exchange 2013 클라이언트 액세스 서버에 있는 가상 디렉터리 하나에 대해서는 Outlook Web App의 IRM을 사용하지 않도록 설정하고, 다른 클라이언트 액세스 서버의 다른 가상 디렉터리에 대해서는 사용하도록 설정할 수 있습니다.
    
      - **Outlook Web App 사서함 정책별**   Outlook Web App 사서함 정책에 대해 Outlook Web App의 IRM을 사용하거나 사용하지 않도록 설정하려면 **Set-OWAMailboxPolicy** cmdlet을 사용하고 *IRMEnabled* 매개 변수를 `$false` 또는 `$true`(기본값)로 설정합니다. 그러면 한 사용자 집합에 대해서는 Outlook Web App의 IRM을 사용하도록 설정하고, 다른 사용자 집합에 대해서는 다른 Outlook Web App 사서함 정책을 할당하여 사용하지 않도록 설정할 수 있습니다.
    
    Exchange ActiveSync 사서함 정책별로 Exchange ActiveSync의 IRM을 제어할 수 있습니다. Exchange ActiveSync 사서함 정책에 대해 Exchange ActiveSync의 IRM을 사용하거나 사용하지 않도록 설정하려면 **Set-ActiveSyncMailboxPolicy** cmdlet을 사용하여 *IRMEnabled* 매개 변수를 `$false` 또는 `$true`(기본값)로 설정합니다. 그러면 한 사용자 집합에 대해서는 Exchange ActiveSync의 IRM을 사용하도록 설정하고, 다른 사용자 집합에 대해서는 다른 Exchange ActiveSync 사서함 정책을 할당하여 사용하지 않도록 설정할 수 있습니다.

  - 클라이언트 액세스 서버에서 IRM을 사용하거나 사용하지 않도록 설정하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 클라이언트 액세스 서버에서 IRM을 사용하도록 설정

이 예에서는 Exchange 조직의 클라이언트 액세스 서버에서 IRM을 사용하도록 설정합니다.

    Set-IRMConfiguration -ClientAccessServerEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 클라이언트 액세스 서버에서 IRM을 사용하지 않도록 설정

이 예에서는 Exchange 조직의 클라이언트 액세스 서버에서 IRM을 사용하지 않도록 설정합니다.

    Set-IRMConfiguration -ClientAccessServerEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

클라이언트 액세스 서버에서 IRM을 사용하거나 사용하지 않도록 성공적으로 설정했는지 확인하려면 다음을 수행하십시오.

  - **Get-IRMConfiguration** cmdlet을 실행하고 *ClientAccessServerEnabled* 속성 값을 확인합니다.
    
    IRM 구성 검색 방법의 예는 **Get-IRMConfiguration**에서 [Examples](https://technet.microsoft.com/ko-kr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) 항목을 참조하십시오.

  - Outlook Web App를 사용하여 IRM으로 보호된 메시지를 만들거나 읽습니다.


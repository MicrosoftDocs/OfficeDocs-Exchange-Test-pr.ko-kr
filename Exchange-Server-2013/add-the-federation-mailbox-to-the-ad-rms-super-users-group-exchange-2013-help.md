---
title: 'AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.: Exchange 2013 Help'
TOCTitle: AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50482988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

다음 Microsoft Exchange Server 2013 정보 권한 관리 (IRM) 기능을 사용 하려면 사용 하도록 설정, 조직의 [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 클러스터에서 고급 사용자 그룹에 페더레이션 사서함 ( Exchange 2013 설치 하 여 만든 시스템 사서함)를 추가 해야 합니다.

  - Microsoft Office Outlook Web App의 IRM

  - Exchange ActiveSync의 IRM

  - 저널 보고서 암호 해독

  - 전송 암호 해독

메일 사용이 가능한 메일 그룹을 AD RMS에서 Super Users 그룹으로 구성할 수 있습니다. 메일 그룹의 구성원이 AD RMS 클러스터에 라이선스를 요청할 경우 소유주 사용권이 부여됩니다. 이렇게 하면 해당 클러스터에서 게시된, RMS로 보호된 모든 콘텐츠의 암호를 해독할 수 있습니다. 기본 메일 그룹을 사용하거나 메일 그룹을 만들어 AD RMS에서 Super Users 그룹으로 구성할 경우, 이 메일 그룹을 해당 목적으로만 사용하고 승인, 감사, 구성원 변경 사항 모니터링을 위한 적절한 설정을 구성하는 것이 좋습니다.


> [!WARNING]
> AD RMS에 고급 사용자 그룹을 구성 그룹 구성원이 IRM으로 보호 된 콘텐츠를 해독할 수 있습니다. 그룹 구성원 자격을 제어 하 고 모니터링을 위한 적절 한 조치를 수행 하 고 구성원 자격 변경 내용을 추적 하도록 감사 기능을 사용 하는 것이 좋습니다. 또한 그룹 정책을 사용 하 여 제한 된 그룹으로 그룹을 구성 하 여 그룹 구성원 자격을 원하지 않는 변경 내용이 제한할 수 있습니다. 자세한 내용은 <A href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">제한 된 그룹 정책 설정</A>를 참조 하십시오.



IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "메일 그룹" 항목

  - Active Directory 포리스트에 AD RMS 클러스터가 배포되어 있어야 합니다.

  - AD RMS 클러스터에서 Super Users 그룹을 이미 구성한 경우, 메일 그룹 구성원에 대한 수정 사항이 AD RMS 클러스터에 반영될 때까지 최대 24시간이 소요될 수 있습니다. 이는 클러스터에서 그룹 구성원을 캐시한 결과입니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 셸을 사용하여 페더레이션 사서함을 메일 그룹에 추가

메일 그룹을 만들어 AD RMS 클러스터의 Super Users 그룹으로 구성한 경우에는 Exchange 2013 페더레이션 사서함을 해당 그룹의 구성원으로 추가할 수 있습니다. Super Users 그룹을 구성하지 않은 경우에는 메일 그룹과 함께 구성원인 페더레이션 사서함을 만들어야 합니다.

1.  AD RMS Super Users 그룹으로만 사용할 메일 그룹을 만듭니다. 자세한 내용은 [메일 그룹 만들기 및 관리](create-and-manage-distribution-groups-exchange-2013-help.md)를 참조하십시오.

2.  사용자 **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042**를 새 메일 그룹에 추가합니다. 페더레이션 사서함은 시스템 사서함이므로 EAC에서 볼 수 없습니다. 사용자를 메일 그룹에 추가하려면 셸에서 [Add-DistributionGroupMember](https://technet.microsoft.com/ko-kr/library/bb124340\(v=exchg.150\)) cmdlet을 사용해야 합니다.
    
    이 예제에서는 페더레이션 사서함을 ADRMSSuperUsers 메일 그룹에 추가합니다.
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

구문과 매개 변수에 대한 자세한 내용은 [Add-DistributionGroupMember](https://technet.microsoft.com/ko-kr/library/bb124340\(v=exchg.150\))를 참조하십시오.

## 2단계: AD RMS를 사용하여 Super Users 그룹 설정

AD RMS 클러스터에서 다음 절차를 수행합니다. 이 절차를 수행하는 데 사용하는 계정은 AD RMS 서버에서 AD RMS Enterprise Administrators 로컬 그룹의 구성원이어야 합니다.

1.  AD RMS(Active Directory Rights Management Services) 콘솔을 열고 AD RMS 클러스터를 확장합니다.

2.  콘솔 트리에서 **보안 정책**을 확장한 다음 **Super Users**를 클릭합니다.

3.  작업 창에서 **Super Users 사용**을 클릭합니다.

4.  결과 창에서 **Super User 그룹 변경**을 클릭하여 **Super Users** 속성 시트를 엽니다.

5.  **Super Users 그룹** 상자에 이전 절차에서 만든 메일 그룹의 전자 메일 주소를 입력하거나, **찾아보기**를 클릭하여 메일 그룹을 선택합니다.

## 작동 여부는 어떻게 확인합니까?

새 메일 그룹이나 기존 메일 그룹에 페더레이션 사서함을 추가한 후에 [Get-DistributionGroupMember](https://technet.microsoft.com/ko-kr/library/aa996367\(v=exchg.150\)) cmdlet을 사용하여 그룹 구성원을 확인할 수 있습니다.

메일 그룹 구성원을 확인하는 방법의 예제는 **Get-DistributionGroupMember**의 [Examples](https://technet.microsoft.com/ko-kr/aa996367\(exchg.150\)#examples) 항목을 참조하십시오.

AD RMS를 사용하여 Super Users 그룹을 설정한 후 다음 방법으로 Super Users 그룹이 올바르게 구성되었는지 확인할 수 있습니다. 또한 [Test-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979798\(v=exchg.150\)) cmdlet을 사용하여 IRM 기능을 확인할 수 있습니다.

  - AD RMS 콘솔을 사용하여 올바른 그룹이 Super Users 그룹으로 구성되었는지 확인합니다.

  - AD RMS 서버에서 다음 PowerShell 명령을 실행하여 Super Users 그룹을 검색합니다.
    

    > [!IMPORTANT]
    > ADRMSAdmin PowerShell 모듈은 Windows Server 2008 R2 이상 버전에서 사용할 수 있습니다.

    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser


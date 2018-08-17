---
title: '저널 보고서 암호 해독을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 저널 보고서 암호 해독을 사용 하지 않도록 설정 하거나 사용
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50482650
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 저널 보고서 암호 해독을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

사용 저널 보고서 암호 해독 저널링 에이전트를 권한으로 보호 된 메시지의 암호가 해독 된 복사본을 저널 보고서를 연결할 수 있습니다. 저널 보고서 암호 해독을 사용 하도록 설정 하기 전에 [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 서버에 구성 된 고급 사용자 그룹에는 페더레이션 배달 사서함을 추가 해야 합니다.

IRM(정보 권한 관리) 관련 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - Super Users 그룹의 구성원이 AD RMS 클러스터에 라이선스를 요청할 경우 소유주 사용권이 부여됩니다. 이를 통해 AD RMS 클러스터에서 만든 RMS로 보호된 모든 콘텐츠의 암호를 해독할 수 있습니다.

  - Active Directory 포리스트에 AD RMS 클러스터가 설치되어 있어야 합니다.

  - 페더레이션 배달 사서함이 AD RMS Super Users 그룹에 추가되어 있어야 합니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md) 항목을 참조하십시오.

  - EAC(Exchange 관리 센터)를 사용하여 저널 보고서 암호 해독을 사용하도록 설정할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 저널 보고서 암호 해독을 사용하도록 설정

다음은 Exchange 조직에서 저널 보고서 암호 해독을 사용하도록 설정하는 예입니다.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 저널 보고서 암호 해독을 사용하지 않도록 설정

다음은 Exchange 조직에서 저널 보고서 암호 해독을 사용하지 않도록 설정하는 예입니다.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) 항목을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

저널 보고서 암호 해독을 사용하도록 설정했는지 여부를 확인하려면 **Get-IRMConfiguration** cmdlet을 실행하고 *JournalDecryptionEnabled* 속성의 값을 확인하십시오.

IRM 구성 확인 방법의 예제는 **Get-IRMConfiguration**의 [Examples](https://technet.microsoft.com/ko-kr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) 항목을 참조하십시오.


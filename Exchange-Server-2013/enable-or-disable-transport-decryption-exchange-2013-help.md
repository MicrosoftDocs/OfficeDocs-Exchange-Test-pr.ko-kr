---
title: '사용 하도록 설정 또는 전송 암호 해독을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 또는 전송 암호 해독을 사용 하지 않도록 설정
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50483004
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 또는 전송 암호 해독을 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

전송 암호 해독을 사용 하면 전송 규칙 에이전트 Microsoft Exchange Server 2013 에서 정보 권한 관리 (IRM)으로 보호 된 메시지의 콘텐츠에 액세스 하려면 사서함 서버를 수 있습니다. 따라서 다른 전송 에이전트는 메시지 콘텐츠에 액세스 하 고 가능한 경우 항목을 변경 수 있습니다. 예, 메시지 콘텐츠를 조사 하 고 (예: 메시지에는 고 지 사항을 적용 하는 규칙) 전송 규칙을 적용 하는 전송 규칙 에이전트 해야 합니다. IRM으로 보호 된 메시지를 성공적으로 해독 하려면 [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 서버에 구성 된 고급 사용자 그룹에는 페더레이션 배달 사서함을 추가 해야 합니다.


> [!IMPORTANT]
> Super Users 그룹의 구성원이 AD RMS 클러스터에 라이선스를 요청할 경우 소유주 사용권이 부여됩니다. 이를 통해 AD RMS 클러스터에서 만든 RMS로 보호된 모든 콘텐츠의 암호를 해독할 수 있습니다.



전송 암호 해독을 사용 하도록 설정할 때 다음 설정을 지정할 수 있습니다.

  - **필수**    암호를 해독할 수 없는 메시지를 거부 하 고 보낸 사람에 게 배달 못함 보고서 (NDR)를 반환 합니다.

  - **선택 사항**    암호 해독 하는 최상의 방법을 사용합니다. 가능 하면 메시지의 암호 해독 하지만 암호 해독에 실패 하는 경우에 전달 되는 합니다. 이것이 기본 설정입니다.

전송 암호 해독 하는 방법에 대 한 자세한 내용은, [전송 암호 해독](transport-decryption-exchange-2013-help.md)를 참조 하십시오.

IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - AD RMS 서버 Active Directory 포리스트에 있으며 액세스할 수 있습니다.

  - 페더레이션 배달 사서함 AD RMS 고급 사용자 그룹에 추가 되었습니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조 합니다.

  - 전송 암호 해독을 사용 하도록 설정 하려면 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. 셸을 사용 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 전송 암호 해독을 사용 하도록 설정

Exchange 2013 조직에 대 한 전송 암호 해독을 설정 하는이 예제입니다. 암호를 해독할 수 없는 메시지는 거부 하 고 보낸 사람에 게 NDR이 반환 됩니다.

    Set-IRMConfiguration -TransportDecryptionSetting Mandatory

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 전송 암호 해독을 사용 하지 않도록 설정 하려면

이 예에서는 Exchange 2013 조직에 대 한 전송 암호 해독 사용 하지 않도록 설정 합니다.

    Set-IRMConfiguration -TransportDecryptionSetting Disabled

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용 하도록 설정 하거나 전송 암호 해독을 사용 하지 않도록 설정 했는지를 확인 하려면 **Get-IRMConfiguration** cmdlet을 사용 하 고 *JournalDecryptionEnabled* 속성의 값을 확인 합니다.

IRM 구성 확인 방법의 예제는 **Get-IRMConfiguration**의 [Examples](https://technet.microsoft.com/ko-kr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) 항목을 참조하십시오.


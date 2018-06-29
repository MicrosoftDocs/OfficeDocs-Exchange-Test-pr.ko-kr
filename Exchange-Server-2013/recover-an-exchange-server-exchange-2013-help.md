---
title: 'Exchange Server 복구: Exchange 2013 Help'
TOCTitle: Exchange Server 복구
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50483011
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server 복구

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 **Setup /m:RecoverServer** 스위치를 사용하여 손실된 서버를 복구할 수 있습니다. Exchange 2013을 실행하는 컴퓨터의 설정은 대부분 Active Directory에 저장됩니다. */m:RecoverServer* 스위치는 Exchange에 저장된 설정 및 기타 정보를 사용하여 Active Directory 서버를 동일한 이름으로 다시 작성합니다.

손실된 Exchange 서버를 복구하려는 경우 대체로 새 하드웨어를 사용합니다. 그러나 기존 서버를 사용할 수도 있습니다.

이 항목에서는 DAG(데이터베이스 가용성 그룹)의 구성원이 아닌 손실된 Exchange 2013 서버를 복구하는 방법을 보여 줍니다. DAG의 구성원인 서버를 복구하는 방법에 대한 자세한 내용은 [데이터베이스 가용성 그룹의 구성원 서버를 복구 합니다.](recover-a-database-availability-group-member-server-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> Exchange가 기본 위치가 아닌 위치에 설치된 경우 <EM>/TargetDir</EM> 스위치를 사용하여 Exchange 이진 파일의 위치를 지정해야 합니다. <EM>/TargetDir</EM> 스위치를 사용하지 않으면 Exchange 파일은 기본 위치(%programfiles%\Microsoft\Exchange Server\V15)에 설치됩니다.<BR>설치 위치를 확인하려면 다음 단계를 따르십시오. 
> <OL>
> <LI>
> <P>ADSIEDIT.MSC 또는 LDP.EXE를 엽니다.</P>
> <LI>
> <P>다음 위치로 이동합니다. <STRONG>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</STRONG></P>
> <LI>
> <P>Exchange 서버 개체를 마우스 오른쪽 단추로 클릭한 다음 <STRONG>속성</STRONG>을 클릭합니다.</P>
> <LI>
> <P><STRONG>msExchInstallPath</STRONG> 특성을 찾습니다. 이 특성은 현재 설치 경로를 저장합니다.</P></LI></OL>



데이터 백업 및 복원과 관련된 다른 관리 작업에 대한 자세한 내용은 [백업, 복원 및 재해 복구](backup-restore-and-disaster-recovery-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 20분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "Exchange 인프라 권한" 항목

  - 복구 중인 서버에서 손실된 서버와 동일한 운영 체제를 실행하고 있어야 합니다. 예를 들어, Windows Server 2012를 실행 중인 서버에서는 Exchange 2013 및 Windows Server 2008 R2를 실행했던 서버를 복구할 수 없으며 그 반대의 경우도 마찬가지입니다. 이와 같이 Exchange 2013 및 Windows Server 2012가 실행되는 서버를 Windows Server 2012 R2가 실행되는 서버에서 복구할 수 없으며 그 반대의 경우도 마찬가지입니다.

  - 오류가 발생한 서버에서 탑재된 데이터베이스에 사용된 디스크 드라이브 문자와 동일한 디스크 드라이브 문자가 복구를 실행 중인 서버에 있어야 합니다.

  - 복구 중인 서버의 성능 특성과 하드웨어 구성이 손실된 서버와 같아야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 손실된 Exchange Server 복구

1.  손실 된 서버에 대 한 컴퓨터 계정을 다시 설정 합니다. 자세한 단계에 대 한 [컴퓨터 계정 재설정](https://go.microsoft.com/fwlink/p/?linkid=165388)를 참조 하십시오.

2.  적절한 운영 체제를 설치하고 새 서버의 이름을 손실된 서버와 동일한 이름으로 지정합니다. 복구 중인 서버의 이름이 손실된 서버와 다르면 복구에 실패합니다.

3.  손실된 서버와 동일한 도메인에 서버를 가입시킵니다.

4.  필수 구성 요소와 운영 체제 구성 요소를 설치합니다. 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md) 및 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)를 참조하십시오.

5.  복구 중인 서버에 로그온한 후 명령 프롬프트를 엽니다.

6.  Exchange 2013 설치 파일로 이동한 후 다음 명령을 실행합니다.
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  설치가 완료되고 복구한 서버를 프로덕션에 배치하기 전, 이전에 서버에 있었던 모든 사용자 지정 설정을 다시 구성한 다음 서버를 다시 시작합니다.

## 작동 여부는 어떻게 확인합니까?

성공적인 설치 완료는 복구에 성공했음을 알려주는 가장 확실한 지표입니다. 손실된 서버가 성공적으로 복구되었는지 확인하려면 다음을 수행하십시오.

  - Windows Services 도구(services.msc)를 열고 Exchange 서비스가 설치되어 실행 중인지 확인합니다.


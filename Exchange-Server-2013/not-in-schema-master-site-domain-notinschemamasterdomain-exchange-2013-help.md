---
title: '스키마 마스터 사이트/domain_NotInSchemaMasterDomain에 없음: Exchange 2013 Help'
TOCTitle: 스키마 마스터 사이트/domain_NotInSchemaMasterDomain에 없음
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50483216
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스키마 마스터 사이트/domain\_NotInSchemaMasterDomain에 없음

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

설치 프로그램을 실행 하는 컴퓨터에 없는 동일한 Active Directory® 디렉터리 서비스 사이트 또는 도메인 역할에 할당 된 도메인 스키마 마스터로 알려져 유연한 단일 마스터 작업 또는 FSMO는 서버와 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치 Exchange 설치를 실행 하는 로컬 컴퓨터와 동일한 사이트 및 도메인에 있는 것으로 도메인 스키마 마스터와 역할 하는 도메인 컨트롤러를 필요 합니다.

모든 업데이트 및 Active Directory 스키마를 수정한 경우 도메인 스키마 마스터를 제어합니다.

이 문제를 해결 하려면 도메인 스키마 마스터와 동일한 사이트 및 도메인에서 **/prepareschema** 및 **/prepareAD** 스위치를 사용 하 여 Exchange Server 2007 설치 프로그램을 실행 합니다.

**/Prepareschema** 및 **/prepareAD** 설치 스위치에 대 한 자세한 내용은 Exchange 2007 제품 설명서 항목 "어떻게 하 준비 Active Directory 및 도메인" (<https://go.microsoft.com/fwlink/?linkid=78453>)을 참조 하십시오.

역할을 식별 하는 스키마 마스터 도구를 사용할 수 있습니다. 그러나 스키마 도구를 MMC 스냅인을 사용 하는로 사용할 수 있도록 하기 위해 다음 Schmmgmt.dll DLL은 등록 해야 합니다.

현재 스키마 마스터를 보려면

1.  명령 프롬프트에서 **다음 regsvr32 schmmgmt.dll** 를 입력 합니다.
    

    > [!NOTE]
    > 다음과 같은 대화 상자가 표시 되 면 <STRONG>RegSvr32</STRONG> 성공적으로 등록 되었는지 합니다.<BR>메시지가 다음 schmmgmt.dll에 성공 했습니다.



2.  새 관리 콘솔을 열려면 **시작**, **실행** 을 차례로 클릭 하 고 **mmc**를 입력 합니다.

3.  콘솔 메뉴에서 **스냅인 추가/제거를** 클릭 합니다.

4.  **독립 실행형 스냅인 추가** 대화 상자를 열려면 **추가** 클릭 합니다.

5.  **Active Directory 스키마** 를 선택한 다음 **추가** 클릭 합니다.

6.  "Active Directory 스키마" 추가/제거 스냅인에 표시 된 **Close** 를 클릭 한 다음 콘솔으로 돌아가려면 **확인** 클릭 합니다.

7.  **클래스** 와 **특성** 섹션 오른쪽에 표시 되도록 **Active Directory 스키마** 를 선택 합니다.

8.  **Active Directory 스키마** 를 마우스 오른쪽 단추로 클릭 하 고 **작업 마스터** 를 클릭 합니다.

9.  현재 스키마 마스터 표시

현재 스키마 마스터를 파악 한 후에 스키마 마스터에 있는 어떤 서브넷을 결정 합니다. Exchange를 설치 하는 다음 방법 중 하나를 사용:

  - 스키마 마스터가 있는 사이트로 이동 하는 Exchange 서버에서 서브넷을 수정 합니다. 그런 다음 Exchange를 설치 합니다.

  - 일시적으로 Exchange 서버에서 강제로 사이트 구성원 자격 변경 하 고 Exchange를 설치 합니다. Exchange가 설치 된 후 원래 사이트로 Exchange 서버를 반환 합니다.

사이트 구성원 자격을 강제 실행 하려면

1.  Exchange를 설치 하려는 서버에서 레지스트리 편집기를 시작 합니다. 이 작업을 수행 **시작**, **실행** 을 클릭, **regedit**를 입력 한 다음 **확인** 을 클릭 합니다.

2.  다음 레지스트리 하위 키를 찾습니다.
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  다음과 같은 새 **문자열** 값을 만듭니다.
    
    값 이름: **SiteName**
    
    값 형식: **REG\_SZ**
    
    값 데이터: **\< site\_that\_contains\_the\_schema\_master \>**

4.  레지스트리 편집기를 종료 하 고 Netlogon 서비스를 다시 시작 합니다. 이 작업을 수행 하면 지정 된 사이트에 참여 하도록 Exchange server 합니다.

5.  Exchange를 설치 합니다.

6.  3 단계에서 추가 하는 레지스트리 항목을 제거 합니다.

7.  Netlogon 서비스를 다시 시작 합니다. 원래 사이트에 Exchange를 반환 하는이 작업을이 수행 합니다.


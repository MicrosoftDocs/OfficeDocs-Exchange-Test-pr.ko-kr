---
title: 배포와 관련된 절차
TOCTitle: 배포와 관련된 절차
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53275602
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 배포와 관련된 절차

 

_**마지막으로 수정된 항목:**  2013-04-17_

이 섹션에서는 Exchange Server 2013 관리 팩을 가져올 때 참조로 사용할 수 있는 절차에 대해 설명합니다. 배포 후 작업과 관련된 절차는 [Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md)를 참조하십시오.

## 에이전트 배포 상태 확인

Exchange Server 2013 관리 팩을 가져오기 전에 Exchange 서버의 SCOM 에이전트가 작동 중인지, 운영 체제 상태가 SCOM에서 올바르게 보고되고 있는지 확인합니다.

이 절차를 수행하려면 사용자 계정이 Operations Manager 관리자 역할의 구성원이어야 합니다.

1.  SCOM 서버에 로그온하고 SCOM 콘솔을 엽니다.

2.  **모니터링**을 클릭한 후 **Windows 컴퓨터**를 클릭합니다.

3.  모든 Exchange 서버에 **정상**이 표시되는지 확인합니다.

![SCOM 콘솔의 정상 상태 에이전트](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "SCOM 콘솔의 정상 상태 에이전트")

## 에이전트 프록시 구성 확인

Exchange Server 2013 관리 팩을 가져오기 전에 SCOM에서 에이전트 프록시를 검색할 수 있도록 설정되어 있는지 확인합니다. 그렇지 않으면 Exchange 서버의 에이전트가 Exchange의 상태를 보고하지 않습니다. 모든 Exchange Server에 대해 이 구성을 확인해야 합니다.

이 절차를 수행하려면 사용자 계정이 Operations Manager 관리자 역할의 구성원이어야 합니다.

1.  SCOM 서버에 로그온하고 SCOM 콘솔을 엽니다.

2.  운영 콘솔에서 **관리**를 클릭합니다.

3.  **에이전트에서 관리**를 클릭하고 Exchange 서버를 마우스 오른쪽 단추로 클릭한 후 **속성**을 선택합니다.

4.  **보안** 탭에서 **이 에이전트를 프록시로 허용하고 다른 컴퓨터에서 관리되는 개체 검색** 확인란이 선택되어 있는지 확인합니다.

5.  **확인**을 클릭합니다.

## 에이전트 보안 구성 확인

Exchange 2013이 테스트된 보안 모델로 인해 **LocalSystem**이 아닌 계정으로 Exchange 서버에서 SCOM 에이전트를 실행할 수 없습니다. LocalSystem이 아닌 계정으로 에이전트를 실행하는 경우 가상 트랜잭션 실행이 실패합니다. 다른 문제도 발생할 수 있습니다.

이 절차를 수행하려면 사용자 계정이 Server Management 역할 그룹의 구성원이어야 합니다.

1.  Exchange 서버에 로그온합니다.

2.  **시작** \> **관리 도구** \> **서비스**를 클릭합니다.

3.  서비스 목록을 아래로 스크롤하여 **System Center Management** 서비스를 찾습니다.

4.  **다음으로 로그온** 열에 **로컬 시스템**이 표시되어 있는지 확인합니다.

5.  **다음으로 로그온** 열에 다른 항목이 표시된 경우 서비스 로그온을 \[로컬 시스템\]으로 변경합니다.
    
    1.  **System Center Management** 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
    
    2.  **로그온** 탭을 선택합니다.
    
    3.  **로컬 시스템 계정** 옵션을 클릭합니다.
    
    4.  **확인**을 클릭합니다.


---
title: Exchange Server 2013 관리 팩 가져오기
TOCTitle: Exchange Server 2013 관리 팩 가져오기
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53275607
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 관리 팩 가져오기

 

_**마지막으로 수정된 항목:**  2013-03-30_

먼저 SCOM 배포로 관리 팩을 가져옵니다.

## 필수 구성 요소

관리 팩을 가져오려면 다음 조건이 충족되었는지 확인합니다.

  - 조직에 다음 버전의 System Center Operations Manager 중 하나를 배포했습니다.
    
      - System Center Operations Manager 2012 RTM 이상
    
      - System Center Operations Manager 2007 R2 이상

  - Exchange Server에 SCOM 에이전트를 이미 배포했습니다. [에이전트 배포 상태 확인](procedures-related-to-deployment.md).

  - Exchange Server의 SCOM 에이전트가 로컬 시스템 계정으로 실행되고 있습니다. [에이전트 보안 구성 확인](procedures-related-to-deployment.md).

  - Exchange Server의 SCOM 에이전트가 프록시로 작동하도록 구성되어 있으며 다른 컴퓨터의 관리 개체를 검색합니다. [에이전트 프록시 구성 확인](procedures-related-to-deployment.md).

  - 사용자 계정이 Operations Manager Administrators 역할의 구성원입니다.

## Exchange Server 2013 관리 팩 가져오기

다음 단계에 따라 Exchange Server 2013 관리 팩을 가져옵니다. 이 절차에서는 SCOM(System Center Operations Manager) 서버의 로컬 드라이브에 관리 팩 콘텐츠를 추출했다고 가정합니다. Exchange Server 2013 관리 팩은 다음 위치에서 다운로드할 수 있습니다.

1.  SCOM 서버에 로그온한 다음 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/p/?linkid=268587)에서 Exchange Server 2013 관리 팩을 다운로드합니다.

2.  `ExchangeServerManagementPack.msi` 파일을 실행하여 시스템의 폴더에 관리 팩 콘텐츠를 추출합니다.

3.  SCOM 콘솔을 시작합니다. SCOM 콘솔에서 **관리**를 클릭합니다.

4.  **관리 팩**을 마우스 오른쪽 단추로 클릭한 다음 **관리 팩 가져오기**를 클릭합니다.

5.  관리 팩 가져오기 마법사가 열립니다. **추가**를 클릭한 다음 **디스크에서 추가**를 클릭합니다.

6.  **가져올 관리 팩 선택** 대화 상자가 나타납니다. 관리 팩을 추출한 디렉터리로 이동합니다. `Microsoft.Exchange.15.mp` 파일을 클릭하고 **열기**를 클릭합니다.

7.  **관리 팩 선택** 페이지에 Exchange Server 2013 관리 팩이 나열됩니다. **설치**를 클릭합니다.

8.  **관리 팩 가져오기** 페이지가 나타나고 진행률이 표시됩니다. 가져오기 프로세스 단계에서 문제가 발생하면 목록에서 관리 팩을 선택하여 상태 정보를 확인할 수 있습니다.

9.  가져오기가 완료되면 **닫기**를 클릭합니다.

10. **보기**와 **새로 고침**을 차례로 클릭하거나 F5 키를 눌러 관리 팩 목록에서 Microsoft Exchange Server 2013 관리 팩을 확인합니다.

관리 팩 가져오기가 완료되면 [Exchange Server 2013 관리 팩 시작](getting-started-with-exchange-server-2013-management-pack.md)에서 새로운 대시보드에 대한 내용을 확인하십시오.


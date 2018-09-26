---
title: '보관 할당량 원본 위치 보관에 대 한 Exchange 2013 구성: Exchange 2013 Help'
TOCTitle: 보관 할당량 원본 위치 보관에 대 한 Exchange 2013 구성
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50556111
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보관 할당량 원본 위치 보관에 대 한 Exchange 2013 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-12-04_

온-프레미스 배포에서의 원본 위치 보관 무제한 저장소 할당량 기본적으로 만들어집니다. 결과적으로 보관 사서함에 대 한 저장소 할당량을 설정 하는 사서함의 속성을 편집 하려면 필요 합니다. 보관에 대 한 다음 할당량을 설정할 수 있습니다.

  - **보관 경고 할당량**   지정 된 보관 경고 할당량을 초과 하는 원본 위치 보관, Exchange 관리자에 대 한 이벤트가 기록 됩니다 하 고 사서함 사용자에 게 경고 메시지가 전송 됩니다.

  - **보관 할당량**   지정 된 보관 할당량을 초과 하는 원본 위치 보관 하는 경우 메시지 더이상 보관 사서함으로 이동 하 고 경고 메시지가 사서함 사용자에 게 전송 됩니다.

원본 위치 보관에 대 한 자세한 내용은, [전체에서 Exchange 2013의 보관](in-place-archiving-in-exchange-2013-exchange-2013-help.md)를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - Exchange 관리 센터 (EAC)에서 드롭다운 목록 보관 할당량을 구성 하 고 보관 경고 할당량을 고정된 값으로 사용할 수 있습니다. EAC에 나열 되지 않은 값으로 할당량 중 하나를 설정 하려면 셸을 사용 합니다.

  - 보관 할당량 보다 낮은 값으로 보관 경고 할당량을 구성 합니다. 사용자에 대 한 보관 증가 비율에 따라 보관 경고 할당량과 보관 할당량이 간의 차이 허용 해야 보관 함의 항목을 삭제 하거나 요청 하는 등의 적절 한 작업을 수행 하려면 사용자에 대 한 충분 한 시간에 대 한 관리자 또는 IT helpdesk 그룹의 구성원이 보관 할당량을 발생 시킵니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 보관 할당량을 구성 하 고 사서함에 대 한 경고 할당량을 보관 하려면

1.  **받는 사람** 에 게 이동 \> **사서함**

2.  목록 보기에서 선택 된 사서함

3.  세부 정보 창에서 **원본 위치 보관 함세부 정보 보기를** 클릭 합니다.

4.  **보관 사서함** **할당량 값 (GB)** 및 **(GB) 때 경고 보내기** 목록을 사용 하 여 원하는 값을 선택 합니다.

5.  **확인**을 클릭합니다.

## 셸을 사용 하 여 보관 할당량을 구성 하 고 보관 사서함에 대 한 경고 할당량

이 설정 하는이 예제 Chris Ashton 사서함 보관 할당량 10 기가바이트 (GB)에 사용자는 원본 위치 보관 사서함 꽉 찼음을 경고 메시지를 받지 시간과 더이상 수 있게 됩니다 항목을 이동 하는 보관 합니다. 또한이 예제에서는 보관 경고 할당량 원본 위치 보관 거의 꽉 찼음을 경고 메시지가 받은 사용자는 시간이 며, 9.5 g B로 설정 합니다.

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

기존 사서함에 대해 온-프레미스 보관 사서함을 사용하도록 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** 에 게 이동 \> 원하는 **사서함** 및 사서함을 선택 합니다. 세부 정보 창의 **원본 위치 보관 함자세히 보기를** 클릭 하 고 보관 사서함의 할당량 설정을 확인 합니다.

  - 셸에서 보관 사서함에 대 한 할당량 정보를 표시 하려면 다음 명령을 실행 합니다.

      ```powershell
      Get-Mailbox <Name> | FL Name,Archive*Quota
      ```


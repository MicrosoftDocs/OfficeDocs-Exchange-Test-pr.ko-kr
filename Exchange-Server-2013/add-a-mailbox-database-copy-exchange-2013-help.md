---
title: '사서함 데이터베이스 복사본을 추가 합니다.: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본을 추가 합니다.
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50483493
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본을 추가 합니다.

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-10-30_

사서함 데이터베이스 복사본을 추가하면 기존 데이터베이스와 데이터베이스 복사본 간의 연속 복제가 자동으로 사용하도록 설정됩니다. 데이터베이스 복사본에는 \<*DatabaseName*\>\\\<*HostMailboxServerName*\> 형식의 ID가 자동으로 할당됩니다. 예를 들어 MBX3 서버에 호스트된 DB1 데이터베이스의 복사본은 DB1\\MBX3이 됩니다.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 2분 + 데이터베이스 복사본을 시드하는 시간. 이 시간은 데이터베이스 크기, 속도, 사용 가능한 대역폭, 네트워크의 대기 시간, 저장소 속도 등과 같은 다양한 요소에 따라 달라집니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 데이터베이스의 활성 복사본이 탑재되어 있어야 합니다.

  - 지정된 사서함 서버에서 데이터베이스의 복사본을 호스트하고 있지 않아야 합니다.

  - 선택한 사서함 서버에서 데이터베이스 복사본 및 해당 로그 파일의 경로를 사용할 수 있어야 합니다.

  - 활성 복사본을 호스트하는 서버와 수동 복사본을 호스트할 서버가 모두 동일한 DAG(데이터베이스 가용성 그룹)에 있어야 합니다. 또한 DAG에 쿼럼이 있어야 하고 상태가 양호해야 합니다.

  - 두 번째 데이터베이스 복사본을 추가하는 경우(예: 데이터베이스의 첫 번째 수동 복사본 만들기) 지정된 사서함 데이터베이스에 대해 순환 로깅을 사용하지 않도록 설정해야 합니다. 순환 로깅이 사용하도록 설정된 경우 먼저 사용하지 않도록 설정해야 합니다. 사서함 데이터베이스 복사본을 추가한 후 순환 로깅을 사용하도록 설정할 수 있습니다. 복제된 사서함 데이터베이스에 대해 순환 로깅을 사용하도록 설정하면 CRCL(연속 복제 순환 로깅)이 JET 순환 로깅 대신 사용됩니다. 데이터베이스의 세 번째 또는 연속 복사본을 추가하는 경우 CRCL을 사용할 수 있게 설정한 상태로 둘 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본 추가

1.  
    
    EAC에서 <strong>서버</strong> \> <strong>데이터베이스</strong>로 이동합니다.

2.  복사할 데이터베이스를 선택하고 ![데이터베이스 복사본 추가](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "데이터베이스 복사본 추가")을 클릭합니다.

3.  
    
    <strong>사서함 데이터베이스 복사본 추가</strong> 페이지에서 <strong>찾아보기...</strong>를 클릭하고 데이터베이스 복사본을 호스트할 사서함 서버를 선택한 다음 <strong>확인</strong>을 클릭합니다.

4.  필요한 경우 데이터베이스 복사본에 대한 <strong>활성화 기본 설정 번호</strong>를 구성합니다.

5.  재생 지연 시간을 구성하여 데이터베이스를 지연된 데이터베이스 복사본으로 지정하거나 데이터베이스 복사본의 자동 시드를 연기하려면 <strong>기타 옵션…</strong>을 클릭합니다.

6.  <strong>저장</strong>을 클릭하여 구성 변경 내용을 저장하고 사서함 데이터베이스 복사본을 추가합니다.

7.  <strong>확인</strong>을 클릭하여 표시되는 메시지를 확인합니다.

## 셸을 사용하여 사서함 데이터베이스 복사본 추가

이 예에서는 MBX3이라는 사서함 서버에 사서함 데이터베이스 DB1의 복사본을 추가합니다. 재생 지연 시간과 자르기 지연 시간은 기본값 0으로 유지되고, 활성화 기본 설정은 값 2를 사용하여 구성됩니다.

```powershell
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2
```

이 예에서는 사서함 서버 MBX4에 사서함 데이터베이스 DB2의 복사본을 추가합니다. 재생 지연 시간과 자르기 지연 시간은 기본값 0으로 유지되고, 활성화 기본 설정은 값 `5`를 사용하여 구성됩니다. 또한 이 복사본에 대한 시드가 연기되므로 지리적으로 MBX4에서 멀리 떨어진 현재 활성 데이터베이스 복사본 대신 로컬 원본 서버를 사용하여 시드할 수 있습니다.

```powershell
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed
```

이 예에서는 사서함 서버 MBX5에 사서함 데이터베이스 DB3의 복사본을 추가합니다. 재생 지연 시간은 3일로 설정되고, 자르기 지연 시간은 기본값 0으로 유지되고, 활성화 기본 설정은 값 `4`를 사용하여 구성됩니다.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본이 만들어졌는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 <strong>서버</strong> \> <strong>데이터베이스</strong>로 이동합니다. 복사된 데이터베이스를 선택합니다. 세부 정보 창에 데이터베이스 복사본의 상태 및 해당 콘텐츠 인덱스와 함께 현재 복사 큐 길이가 표시됩니다.

  - 셸에서 다음 명령을 실행하여 사서함 데이터베이스 복사본이 작성되어 있고 정상 상태인지 확인합니다.
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
```
    
    상태 및 콘텐츠 인덱스 상태가 모두 정상이어야 합니다.

## 자세한 내용

[사서함 데이터베이스 복사본](mailbox-database-copies-exchange-2013-help.md)

[사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)


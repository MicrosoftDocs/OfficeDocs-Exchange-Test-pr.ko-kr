---
title: 'P o p 3에 대 한 연결 시간 제한 설정: Exchange 2013 Help'
TOCTitle: P o p 3에 대 한 연결 시간 제한 설정
ms:assetid: 40003115-be4e-4cf1-97b4-f5ca05b314dc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997604(v=EXCHG.150)
ms:contentKeyID: 50555978
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# P o p 3에 대 한 연결 시간 제한 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-28_

유휴 인증 되거나 인증 되지 않은 POP3 연결에 대 한 연결 제한 시간 제한을 구성 하는 EAC 또는 셸을 사용할 수 있습니다.

POP3에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 설정" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 p o p 3에 대 한 연결 제한 시간 제한 설정

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  아래로 스크롤하여 **기타 옵션**을 클릭합니다.

5.  **시간 제한 설정**에서 다음 설정을 사용합니다.
    
      - **인증된 시간 제한(초)**    인증된 유휴 연결을 닫을 때까지의 대기 시간을 지정합니다. 기본값은 1,800이고, 30에서 86,400까지의 값을 사용할 수 있습니다.
    
      - **인증되지 않은 시간 제한(초)**    인증되지 않은 유휴 연결을 닫을 때까지의 대기 시간을 지정합니다. 기본값은 60이고, 30에서 3,600까지의 값을 사용할 수 있습니다.

6.  **적용**을 클릭한 다음 **확인**을 클릭하여 변경 내용을 저장합니다.

P o p 3에 대 한 연결 시간 제한 설정 했을 때 하면, 설정 적용 하려면에 대 한 POP3 서비스를 다시 시작 해야 합니다. POP3 서비스를 다시 시작 하는 방법에 대 한 정보를 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조 하십시오.

## 셸을 사용 하 여 p o p 3에 대 한 연결 제한 시간 제한 설정

이 예에서는 인증된 유휴 연결에 대한 연결 시간 제한을 설정합니다.

    Set -PopSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

이 예에서는 인증되지 않은 유휴 연결에 대한 연결 시간 제한을 설정합니다.

    Set -PopSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

P o p 3에 대 한 연결 시간 제한 설정 했을 때 하면, 설정 적용 하려면에 대 한 POP3 서비스를 다시 시작 해야 합니다. POP3 서비스를 다시 시작 하는 방법에 대 한 정보를 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조 하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

연결 제한이 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  아래로 스크롤하여 **기타 옵션**을 클릭합니다.

5.  **시간 제한 설정**에서 연결 설정이 올바른지 확인합니다.

또는

1.  셸에서 다음 명령을 실행합니다.
    
        Get-PopSettings | format-list

2.  연결 설정이 올바른지 확인합니다.

## 자세한 내용

P o p 3에 대 한 연결을 시간 제한을 설정 하면를 할 수 있습니다.

[Exchange 2013에서 POP3 사용](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[P o p 3에 대 한 연결 제한 설정](set-connection-limits-for-pop3-exchange-2013-help.md)


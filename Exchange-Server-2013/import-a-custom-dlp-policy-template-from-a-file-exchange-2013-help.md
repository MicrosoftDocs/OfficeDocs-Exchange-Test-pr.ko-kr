---
title: '파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면: Exchange 2013 Help'
TOCTitle: 파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50482293
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-08-09_

정책 정보 설정이 포함 된 파일을 가져와서 DLP 정책을 통해 중요 한 정보를 관리할 수 있습니다. DLP 정책 템플릿 개발할 수 Exchange에 관계 없이 XML 파일로 합니다. 그러나 제대로 작동 하기 위해 특정 형식 요구 사항을 충족 해야 합니다. 또는 이전 버전의 Exchange에서 내보내는 정책 Microsoft Exchange Server 2013 로 가져올 수 있습니다.


> [!WARNING]
> DLP 정책을 프로덕션 환경에서 실행하기 전에 테스트 모드에서 실행해야 합니다. 그러한 테스트 중에, 샘플 사용자 사서함을 구성한 다음 결과 확인을 위해 테스트 정책을 호출하는 테스트 메시지를 전송해보는 것이 좋습니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "데이터 손실 방지(DLP)" 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면

다음 절차를 사용 하 여 파일에서 사용자 지정 DLP 정책 서식 파일을 가져올 수 있습니다. 혼란을 방지 하기 위해 자신의 이름을 제공 하는 옵션을 사용 하는 경우 정책 또는 규칙의 각 부분에 대 한 고유 이름을 제공 합니다.

1.  EAC에서 **규정 준수 관리** \> **데이터 손실 방지**로 이동합니다.

2.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 아이콘 옆의 화살표를 클릭하고 **정책 가져오기**를 클릭합니다.

3.  **정책 가져오기** 페이지에서 다음 필드에 값을 입력합니다.
    
    1.  **가져올 파일 선택**   설치할 정책 파일의 이름을 추가합니다.
    
    2.  **이름**   이 정책을 다른 정책과 구분하는 이름을 추가합니다.
    
    3.  **설명**   이 정책을 요약하는 설명을 추가합니다(옵션).
    
    4.  **기타 옵션**   이 정책에 대한 모드 또는 상태를 선택합니다. 새 정책은 지정할 사항을 지정하기 전까지는 완전하게 사용할 수 없습니다. 정책에 대한 기본 모드는 알림이 없는 테스트 모드입니다.
    
    5.  **다음**을 클릭하여 정책의 유효성을 검사하고 정책을 가져옵니다.

## 셸을 사용 하 여 파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면

이 예에서는 C:\\My Documents\\DLP Backup.xml 파일의 사용자 지정 DLP 정책 템플릿 파일을 가져옵니다. XML 파일에서 DLP 정책 컬렉션 가져오기 (영문)를 제거 하거나 조직에 정의 된 모든 기존 DLP 정책을 덮어씁니다. 가져오기 및 현재 DLP 정책을 덮어쓰기 전에 현재 DLP 정책 모음의 백업이 되어있는지 확인 합니다.

    Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))

## 자세한 내용

[데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)


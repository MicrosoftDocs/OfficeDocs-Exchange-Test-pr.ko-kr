---
title: 'DLP 정책 관리: Exchange 2013 Help'
TOCTitle: DLP 정책 관리
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50484022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 정책 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-14_

보기 지정, 변경 또는 Exchange 관리 센터 (EAC) 또는 Exchange 관리 셸을 사용 하 여 Microsoft Exchange 에서 기존 데이터 손실 방지 (DLP) 정책을 제거 합니다.

DLP에 관련 된 추가 관리 작업을 [DLP 절차](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) 또는 [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.

Exchange 관리 셸을 하는 방법에 대 한 자세한 내용은 [PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 각 절차를 완료 시간: 15-60 분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "데이터 손실 방지(DLP)" 항목을 참조하십시오.

  - 모든 DLP 정책에 대 한 다음과 같은 세가지 모드 중 하나를 선택할 수 있습니다.
    
      -    **적용**   정책 내 규칙은 모든 메시지 및 지원되는 파일 형식에 대해 평가됩니다. 정책의 조건을 충족하는 데이터가 검색될 경우 메일 흐름이 중단될 수 있습니다. 정책 내에 설명된 모든 작업이 수행됩니다.
    
      -    **정책 설명이 있는 DLP 정책 테스트**   정책 내 규칙은 모든 메시지 및 지원되는 파일 형식에 대해 평가됩니다. 정책의 조건을 충족하는 데이터가 검색될 경우 메일 흐름이 중단되지 않습니다. 즉, 메시지가 차단되지 않습니다. 정책 설명이 구성되어 있는 경우 사용자에게 표시됩니다.
    
      -    **정책 설명이 없는 DLP 정책 테스트**   정책 내 규칙은 모든 메시지 및 지원되는 파일 형식에 대해 평가됩니다. 정책의 조건을 충족하는 데이터가 검색될 경우 메일 흐름이 중단되지 않습니다. 즉, 메시지가 차단되지 않습니다. 정책 설명이 구성되어 있는 경우 사용자에게 표시되지 않습니다.

  - DLP 정책 내에서 개별 규칙에는 자체 모드 설정을 지정할 수 있습니다. 정책 모드는 해당 정책 내의 규칙의 모드 다르므로, 규칙 설정이 우선순위 있으며 모드에서 최대 성능에 따라 계산 됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 기존 DLP 정책의 세부 정보를 보려면

규칙 및 조직에 이미 설정 된 기존 DLP 정책의 작업 확인 해야할 수 있습니다. 예기치 않은 메일 흐름 문제를 발생 하는 경우 또는 중요 한 정보를 모니터링 해야 하는 방식을 변경 하는 조직 하는 경우에 유용할 수 있습니다.

## EAC를 사용 하 여 기존 DLP 정책 내에서 세부 정보를 보려면

1.  EAC에서 **규정 준수 관리** \> **데이터 손실 방지**로 이동합니다.

2.  정책 목록에 나타난 또는 하나의 항목을 강조 표시 하 고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")클릭 되는 정책 중 하나를 두번클릭 합니다.

3.  **편집 DLP 정책** 페이지에서 **규칙** 을 클릭 합니다.


> [!TIP]
> DLP 정책을 만들고 비 활성화 또는 비활성화 된 모드에서 나갈 수 있습니다. 이 모드에서 정책이 적용 되지 않습니다 하 고 모든 조건자, 작업, 또는 테스트 하거나 그 적용 (영문)를 시작 하기 전에 해당 규칙와 관련 된 값을 변경할 수 있습니다.



## 셸을 사용 하 여 기존 DLP 정책 내에서 세부 정보를 보려면

이 예에서는 Employee Numbers 라는 가상의 DLP 정책에 대 한 정보를 반환 합니다. 명령은 지정 된 DLP 정책의 자세한 구성을 표시 하려면 **Format-List** cmdlet에 파이프 됩니다.

```powershell
Get-DlpPolicy "Employee Numbers" | Format-List
```

구문 및 매개 변수 정보에 대 한 [Get-DlpPolicy](https://technet.microsoft.com/ko-kr/library/jj215752\(v=exchg.150\))를 참조 합니다.

## DLP 정책 변경

정책의 이름 또는 정책의 효과 제어 하는 규칙을 수정 하 여 기존 DLP 정책을 변경할 수 있습니다. 예제 규칙으로 변경 된 포함 될 메시지 본문 및 RMS 보호 (영문) 특정 도메인 내에서 보낸 메시지를 사용자 지정 고 지 사항 텍스트 추가 (영문)와 중요 한 정보를 포함 하는 감지 됩니다. DLP 정책 템플릿을 사용 하는 경우 염두 디자인 하 고 메시징 환경에 대 한 강력한 정책 및 규정 준수 시스템을 적용 하는데 도움이 되는 Exchange 2013 의 기능 중 하나는 이러한 합니다.

## EAC를 사용 하 여 기존 DLP 정책을 변경 하려면

1.  EAC에서 **규정 준수 관리** \> **데이터 손실 방지**로 이동합니다.

2.  정책 목록에 나타난 또는 하나의 항목을 강조 표시 하 고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")클릭 되는 서식 파일 기반 정책 중 하나를 두번클릭 합니다.

3.  **편집 DLP 정책** 페이지에서 **규칙** 을 클릭 합니다.

4.  기존 규칙을 변경 하려면 규칙을 강조 표시 하 고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

5.  원하는대로 사용자 지정할 수 있는 새로운 빈 규칙을 추가 하려면![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**새로 만들기** 클릭 합니다.

6.  보낸사람 알림 메시지를 차단 하거나 재정의 허용 하는 방법에 대 한 규칙을 추가 하려면 **새**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 아이콘 옆에 있는 화살표를 클릭 합니다.

7.  규칙을 제거 하려면 규칙을 강조 표시 하 고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭 합니다.

8.  정책 수정을 완료 하려면 **저장** 을 클릭 하 고 변경 내용을 저장 합니다.

## 셸을 사용 하 여 기존 DLP 정책을 변경 하려면

Exchange 관리 셸을 사용 하 여 정책 작업 및 알림 수준을 지정할 수 있습니다. 작업이 적용 되지 않으며 알림 메시지가 표시 되지 않습니다 되도록 Employee Numbers 라는 가상의 DLP 정책에 대 한 모드를 설정 하는이 예제입니다.

```powershell
Set-DlpPolicy "Employee Numbers" -Mode Audit
```

구문 및 매개 변수 정보에 대 한 [Set-DlpPolicy](https://technet.microsoft.com/ko-kr/library/jj215778\(v=exchg.150\))를 참조 합니다.

## DLP 정책 삭제

EAC를 사용 하는 DLP 정책을 영구적으로 제거할 수 있습니다. 정책을 삭제 한 후 적용 더이상 됩니다 및 규칙 및 작업의 none 저장 됩니다.

또는 **정책 설명이 없는 테스트 DLP 정책** 에 작동 상태 또는 정책 모드를 설정할 수 있습니다. 이 메시지 환경에서 적용 되 고에서 중지 하지 않지만 정책 자체의 자세한 구성 설정을 유지 합니다. 이 정책을 나중에 다시 적용 해야하는 가능성이 하는 경우에 유용할 수 있습니다.

## EAC를 사용 하 여 기존 DLP 정책을 삭제 하려면

1.  EAC에서 **규정 준수 관리** \> **데이터 손실 방지**로 이동합니다.

2.  정책 목록에서 제거 하려는 정책을 선택 하 고![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다.

## 셸을 사용 하 여 기존 DLP 정책을 삭제 하려면

이 예에서는 Employee Numbers 라는 가상의 DLP 정책을 제거 합니다.

```powershell
Remove-DlpPolicy "Employee Numbers"
```

구문 및 매개 변수 정보에 대 한 [Remove-DlpPolicy](https://technet.microsoft.com/ko-kr/library/jj215677\(v=exchg.150\))를 참조 합니다.

## 자세한 내용

[데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[정책 팁](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/policy-tips)


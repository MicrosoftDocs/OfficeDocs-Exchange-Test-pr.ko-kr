---
title: '세부 정보 서식 파일을 기본 구성 복원: Exchange 2013 Help'
TOCTitle: 세부 정보 서식 파일을 기본 구성 복원
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50483566
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 세부 정보 서식 파일을 기본 구성 복원

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-12_

세부 정보 템플릿 편집기에는 **실행 취소** 단추가 없으며, 바로 가기 키를 사용하여 작업을 취소할 수도 없습니다. 템플릿에 추가한 항목에 대해 실행을 취소하려면 Delete 키를 사용해야 합니다. 삭제 작업을 취소하려면 설정을 다시 적용해야 합니다. 또한 변경 내용을 저장하지 않고 세부 정보 템플릿 편집기를 끝내 원래 설정으로 되돌릴 수 있습니다. 저장한 변경 내용을 취소하려면 템플릿을 복원하면 됩니다. 템플릿을 복원하면 사용자 지정 내용이 모두 손실되고 템플릿이 원래 구성으로 복원됩니다.

이 항목에서는 Exchange 2013 도구 상자나 Exchange 관리 셸을 사용하여 세부 항목 템플릿을 기본 구성으로 복원하는 방법에 대해 설명합니다.

세부 항목 템플릿에 대한 자세한 내용은 [세부 항목 템플릿](details-templates-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "세부 정보 템플릿" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Exchange 도구 상자를 사용하여 세부 항목 템플릿을 기본 구성으로 복원

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange Server 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **Exchange 도구 상자**에서 **세부 항목 템플릿 편집기**를 클릭하고 작업 창에서 **도구 열기**를 클릭합니다.

3.  **세부 항목 템플릿 편집기**의 세부 항목 창에서 복원하려는 템플릿을 선택하고 작업 창에서 **복원**을 클릭합니다.

4.  템플릿을 원래 상태로 복원하려면 **예**를 클릭합니다. 모든 사용자 지정이 손실됩니다.

## 셸을 사용하여 세부 항목 템플릿을 기본 구성으로 복원

이 예에서는 영어(미국) 연락처 세부 항목 템플릿을 복원합니다.

```powershell
Restore-DetailsTemplate -Identity "en-US\Contact"
```

구문과 매개 변수에 대한 자세한 내용은 [Restore-DetailsTemplate](https://technet.microsoft.com/ko-kr/library/bb125188\(v=exchg.150\))을 참조하십시오.


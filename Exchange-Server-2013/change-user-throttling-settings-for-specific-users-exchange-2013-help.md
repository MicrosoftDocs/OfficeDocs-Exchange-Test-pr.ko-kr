---
title: '사용자 제한 특정 사용자에 대 한 설정을 변경 합니다.: Exchange 2013 Help'
TOCTitle: 사용자 제한 특정 사용자에 대 한 설정을 변경 합니다.
ms:assetid: c5f834d6-189d-485e-9800-5e0066815ecf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863577(v=EXCHG.150)
ms:contentKeyID: 50556082
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 제한 특정 사용자에 대 한 설정을 변경 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-08-05_

Exchange 조직에서 개별 사용자가 기본 제한 설정을 변경 하 여 리소스를 사용 하는 방법을 제어할 수 있습니다.

개별 사용자가 리소스를 사용 하는 방법을 제어 Exchange Server 2010 가능한 되었으며 Exchange Server 2013 에 대 한이 기능이 확장 되었습니다. GlobalThrottlingPolicy 이라는 정책 정의 기본 제한 정책 사용자 지정 했을 때 하지 않으면 조직에서 모든 기존 및 새 사용자에 대 한 설정을 제한 합니다. 많은 일반적인 Exchange 배포 시나리오에서 GlobalThrottlingPolicy 이라는 정책 사용자를 관리 하려면 적절 한 경우

조직에서 특정 사용자 에게만 적용 하도록 제한 설정의 사용자 지정 하려면 범위 할당을 Regular 새 제한 정책을 만듭니다. 셸을 사용 하 여 제한 설정을 기본만 변경할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [서버 상태 및 성능 사용 권한](server-health-and-performance-permissions-exchange-2013-help.md) 항목의 "사용자 제한" 항목.

  - 새 일반 범위 정책에서 GlobalThrottlingPolicy 및 기타 조직 정책 이라는 정책에서 사항과 다릅니다 제한 설정을 설정 해야 합니다. 이와 같은 방식이으로 GlobalThrottlingPolicy 이라는 정책에서 정책 설정의 나머지 부분 상속 됩니다, 추가 하는 나중에 업데이트 하는 Exchange 정책 제한에 대 한 업데이트 됩니다. 것이 좋습니다 "관리 범위를 사용 하 여 정책을 제한" 섹션을 검토 하는 항목 [Exchange 작업 관리](exchange-workload-management-exchange-2013-help.md) 에서이 절차를 따르기 전에 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 방법 리소스를 변경 하려면 셸을 사용 하 여 전체 조직에서 특정 사용자가 사용할 수 있습니다.

이 예제에서는 제한 정책 ITStaffPolicy 특정 사용자에 게 연결할 수 라는 기본이 아닌 사용자를 만듭니다. 매개 변수를 생략 하면 기본 제한 정책 GlobalThrottlingPolicy에서에서 값을 상속 합니다. 이 정책을 만든 후 특정 사용자와 연결 해야 합니다.

```powershell
New-ThrottlingPolicy -Name ITStaffPolicy -EwsMaxConcurrency 4 -ThrottlingPolicyScope Regular
```

이 예제에서는 제한 정책 ITStaffPolicy (하는 더 높은 제한을 가진)와 사용자 이름에서는 tonysmith 인 사용자와 연결 합니다.

```powershell
Set-ThrottlingPolicyAssociation -Identity tonysmith -ThrottlingPolicy ITStaffPolicy
```

**Set-ThrottlingPolicyAssociation** cmdlet을 사용 하 여 정책을 사용 하 여 사용자를 연결할 필요가 없습니다. 다음 명령은에서는 tonysmith 제한 정책 ITStaffPolicy와 연결 하는 다른 방법은 보여줍니다.

```
$b = Get-ThrottlingPolicy ITStaffPolicy
```

```
Set-Mailbox -Identity tonysmith -ThrottlingPolicy $b
```

구문과 매개 변수에 대 한 자세한 내용은 [New-ThrottlingPolicy](https://technet.microsoft.com/ko-kr/library/dd351045\(v=exchg.150\)) 및 [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/ko-kr/library/ff459231\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

제한 정책 일반 성공적으로 만들었는지를 확인 하려면 다음을 수행 합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-ThrottlingPolicy | Format-List
```

2.  제한 정책 방금 만든 일반 GlobalThrottlingPolicy 개체를 표시 하는 열에 표시 되는지 확인 합니다.

3.  다음 명령을 실행합니다.
    
    ```powershell
Get-ThrottlingPolicy | Format-List
```

4.  새 일반 정책에 대 한 속성 값 또는 값을 구성 하면 일치 하는지 확인 합니다.

5.  다음 명령을 실행합니다.
    
    ```powershell
Get-ThrottlingPolicyAssociation
```

6.  새 일반 정책 되었거나 사용자와 연결 하면 연결 된 사용자가 사용 하 여 있는지 확인 합니다.


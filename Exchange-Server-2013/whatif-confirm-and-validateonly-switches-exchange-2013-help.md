---
title: 'WhatIf, Confirm 및 ValidateOnly 스위치: Exchange 2013 Help'
TOCTitle: WhatIf, Confirm 및 ValidateOnly 스위치
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 50483900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# WhatIf, Confirm 및 ValidateOnly 스위치

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-10-04_

숙련된 관리자와 스크립트 작성자 그리고 Exchange 및 스크립팅을 잘 알지 못하는 관리자 모두 *WhatIf*, *Confirm* 및 *ValidateOnly* 스위치를 사용하면 도움을 받을 수 있습니다. 이러한 스위치를 사용하면 명령이 실행되는 방식을 제어할 수 있고 명령이 데이터에 영향을 미치기 전에 수행하는 작업을 정확하게 표시할 수 있습니다. 이 기능은 테스트 환경에서 프로덕션 환경으로 전환할 때와 새 스크립트 또는 명령을 새로 선보일 때 매우 유용합니다.

*WhatIf*, *Confirm* 및 *ValidateOnly* 스위치는 필터를 사용하거나 파이프라인의 <strong>Get</strong> 명령을 사용하여 반환된 개체를 수정하는 명령과 함께 사용할 때 특히 유용합니다. 이 항목에서는 각 스위치에 대해 설명하고 각 스위치에 대한 명령 예를 제공합니다.


> [!IMPORTANT]
> 스크립트에서 명령과 함께 <EM>WhatIf</EM>, <EM>Confirm</EM> 및 <EM>ValidateOnly</EM> 스위치를 사용하려면 스크립트를 호출하는 명령줄이 아니라 스크립트에서 각 명령에 적합한 스위치를 추가해야 합니다.




> [!NOTE]
> <EM>WhatIf</EM>, <EM>Confirm</EM> 및 <EM>ValidateOnly</EM>를 스위치 매개 변수라고 합니다. 스위치 매개 변수에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/bb124388(v=exchg.150)">매개 변수</A>를 참조하십시오.



## WhatIf 스위치

*WhatIf* 스위치는 명령을 실행할 경우 영향을 받는 개체와 이러한 개체에 적용될 변경 내용만 표시하도록 명령에 지시합니다. 이 스위치는 해당 개체를 실제로 변경하지는 않습니다. *WhatIf* 스위치를 사용하면 개체를 수정하지 않고도 해당 개체에 대한 변경 내용이 올바르게 적용되었는지 여부를 확인할 수 있습니다.

*WhatIf* 스위치와 함께 명령을 실행할 경우 다음 예와 같이 명령의 끝에 *WhatIf* 스위치를 배치합니다.

  ```poweshell
  New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 
  ```
  
이 명령 예를 실행하면 셸에서 다음 텍스트가 반환됩니다.

```powershell
What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".
```

## Confirm 스위치

*Confirm* 스위치는 적용 대상 명령에 변경 내용을 적용하기 전에 처리를 중지하도록 명령에 지시합니다. 그러면 해당 명령은 계속하기 전에 각 동작에 대한 확인 메시지를 표시합니다. *Confirm* 스위치를 사용하면 개체에 단계적으로 변경 내용을 적용하여 변경하려는 특정 개체에만 변경 내용이 적용되도록 할 수 있습니다. 이 기능은 많은 개체에 변경 사항을 적용할 때와 셸 작업 전체를 정밀하게 제어하려는 경우 유용합니다. 셸에서 개체를 수정하기 전에 각 개체에 대해 확인 메시지가 표시됩니다.

기본적으로 셸은 다음 동사가 있는 cmdlet에 자동으로 *Confirm* 스위치를 적용합니다.

  - <strong>Clear</strong>

  - <strong>Disable</strong>

  - <strong>Dismount</strong>

  - <strong>Move</strong>

  - <strong>Remove</strong>

  - <strong>Stop</strong>

  - <strong>Suspend</strong>

  - <strong>Uninstall</strong>

이러한 동사가 있는 cmdlet이 실행되면 셸은 자동으로 명령을 중지하고 처리를 계속하기 전에 사용자의 확인을 기다립니다.

*Confirm* 스위치를 명령에 수동으로 적용하려면 다음 예에서와 같이 명령의 끝에 *Confirm* 스위치를 포함하십시오.

```powershell
Get-JournalRule | Enable-JournalRule -Confirm
```

이 명령 예를 실행하면 셸에서 다음 확인 메시지가 반환됩니다.

    Confirm
    Are you sure you want to perform this action?
    Enabling journal rule "Litigation Journal Rule".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):

확인 메시지를 통해 다음을 선택할 수 있습니다.

  - <strong>\[Y\] 예</strong>   작업을 계속하도록 명령에 지시하려면 <strong>Y</strong>를 입력합니다. 다음 작업에서 확인 메시지가 다시 표시됩니다. 기본값은 `[Y] Yes`입니다.

  - <strong>\[A\] 모두 예</strong>   이 작업과 모든 후속 작업을 계속하도록 명령에 지시하려면 <strong>A</strong>를 입력합니다. 이 명령을 수행하는 동안에는 추가 확인 메시지가 나타나지 않습니다.

  - <strong>\[N\] 아니요</strong>   이 작업을 건너뛰고 다음 작업을 계속하도록 명령에 지시하려면 <strong>N</strong>을 입력합니다. 다음 작업에서 확인 메시지가 다시 표시됩니다.

  - <strong>\[L\] 모두 아니요</strong>   이 작업과 모든 후속 작업을 건너뛰도록 명령에 지시하려면 <strong>L</strong>을 입력합니다.

  - <strong>\[S\] 일시 중단</strong>   현재 파이프라인을 일시 중지하고 명령줄로 돌아가려면 <strong>S</strong>를 입력합니다. 파이프라인을 다시 시작하려면 <strong>Exit</strong>를 입력합니다.

  - <strong>\[?\] 도움말</strong>   명령줄에 확인 메시지 도움말을 표시하려면 <strong>?</strong>를 입력합니다.

셸의 기본 동작을 무시하고 이 스위치가 자동으로 적용되는 cmdlet에 대해 확인 메시지를 표시하지 않으려면 다음 예에서와 같이 값이 `$False`인 *Confirm* 스위치를 포함할 수 있습니다.

```powershell
Get-JournalRule | Disable-JournalRule -Confirm:$False
```

이 경우 확인 메시지가 표시되지 않습니다.


> [!WARNING]
> <EM>Confirm</EM> 스위치의 기본값은 <CODE>$True</CODE>입니다. 셸의 기본 동작은 확인 메시지를 자동으로 표시하는 것입니다. 이 기본 동작이 수행되지 않도록 하려면 해당 명령이 실행되는 동안 모든 확인 메시지를 표시하지 않도록 지시할 수 있습니다. 명령이 확인 없이 명령에 대한 조건을 충족하는 모든 개체를 처리합니다.



## ValidateOnly 스위치

*ValidateOnly* 스위치는 변경 내용을 적용하기 전에 작업을 수행하는 데 필요한 모든 조건과 요구 사항을 평가하도록 명령에 지시합니다. *ValidateOnly* 스위치는 실행하는 데 오랜 시간이 걸리거나, 여러 시스템과 여러 종속 관계를 갖거나, 사서함과 같은 중요한 데이터에 영향을 미칠 수 있는 cmdlet에서 사용할 수 있습니다.

*ValidateOnly* 스위치를 명령에 적용하면 해당 명령은 전체 프로세스에 걸쳐 실행됩니다. 이 명령은 *ValidateOnly* 스위치가 없을 때와 마찬가지로 각 동작을 수행하지만 개체를 변경하지는 않습니다. 명령이 해당 프로세스를 완료하면 유효성 검사 결과가 있는 요약이 표시됩니다. 유효성 검사에서 명령이 성공적으로 수행된 것으로 표시되면 *ValidateOnly* 스위치 없이 다시 명령을 실행할 수 있습니다.

*ValidateOnly* 스위치와 함께 명령을 실행할 경우 명령의 끝에 *ValidateOnly* 스위치를 넣습니다.


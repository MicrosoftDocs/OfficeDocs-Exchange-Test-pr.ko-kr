---
title: 'Exchange 2013: 에디션 및 버전: Exchange 2013 Help'
TOCTitle: 'Exchange 2013: 에디션 및 버전'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50556071
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013: 에디션 및 버전

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013에서는 이렇게 2개의 서버 에디션으로 판매됩니다. Enterprise Edition은 RTM(Release To Manufacturing) 및 CU1(누적 업데이트 1) 버전에서 서버당 데이터베이스를 50개까지 탑재할 수 있으며, CU2(누적 업데이트 2) 이상 버전에서는 서버당 데이터베이스를 100개까지 탑재할 수 있습니다. Standard Edition은 서버당 탑재된 데이터베이스가 5개로 제한됩니다. 탑재된 데이터베이스는 사용 중인 데이터베이스입니다. 탑재된 데이터베이스는 클라이언트가 사용하도록 탑재된 활성 사서함 데이터베이스이거나, 로그 복제 및 재생을 위해 복구에 탑재된 수동 사서함 데이터베이스일 수 있습니다. 위에서 설명한 제한보다 많은 데이터베이스를 만들 수는 있지만 위에 지정된 최대 수만큼만 탑재할 수 있습니다. 복구 데이터베이스는 이 제한에 포함되지 않습니다.

이러한 라이선스 에디션은 제품 키로 정의됩니다. 유효한 라이선스 제품 키를 입력하면 해당 서버에 대해 지원되는 에디션이 설정됩니다. 제품 키는 동일한 에디션 키의 교체 및 업그레이드에만 사용할 수 있으며 다운그레이드에는 사용할 수 없습니다. 유효한 제품 키를 사용하여 Exchange 2013의 평가 버전(평가판 에디션)에서 Standard Edition 또는 Enterprise Edition으로 전환하거나 Standard Edition에서 Enterprise Edition으로 전환할 수도 있습니다.

같은 에디션의 제품 키를 사용하여 서버에 라이선스를 다시 부여할 수도 있습니다. 예를 들어, 각각 다른 키가 있는 두 대의 Standard Edition 서버가 있는데 실수로 두 서버에서 동일한 키를 사용한 경우 한 서버의 키를 발급받은 다른 키로 변경할 수 있습니다. 이러한 작업은 다시 설치하거나 다시 구성할 필요 없이 수행할 수 있습니다. 제품 키를 입력하고 Microsoft Exchange Information Store 서비스를 다시 시작하면 해당 제품 키의 에디션이 반영됩니다.

평가판 에디션이 만료되어도 기능은 손실되지 않으므로 Exchange 2013 평가판 에디션을 다시 설치할 필요 없이 실험실, 데모, 교육 시설 및 기타 비프로덕션 환경을 120일 이상 유지 관리할 수 있습니다.

앞에서 설명한 대로 제품 키를 사용하여 Enterprise Edition에서 Standard Edition으로 다운그레이드하거나 평가판 에디션으로 되돌릴 수는 없습니다. 이러한 유형의 다운그레이드는 Exchange 2013을 제거한 후 Exchange 2013을 다시 설치하고 올바른 제품 키를 입력해야만 가능합니다.

## Exchange 2013 버전

Exchange 2013 버전 목록 및 최신 버전의 Exchange 2013을 다운로드하여 업그레이드하는 방법에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [Exchange Server 업데이트: 빌드 번호 및 릴리스 날짜](https://technet.microsoft.com/ko-kr/library/hh135098\(v=exchg.150\))

  - [최신 누적 업데이트 또는 서비스 팩으로 Exchange 2013 업그레이드](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

실행 중인 Exchange 2013 버전의 빌드 번호를 보려면 Exchange 관리 셸에서 다음 명령을 실행합니다.

```powershell
Get-ExchangeServer | fl name,edition,admindisplayversion
```

## Exchange 2013 라이선스 유형

Exchange 2013 Exchange 2010 사용이 허가 된 어떻게와 비슷합니다 서버/클라이언트 액세스 라이선스 (CAL) 모델로 사용이 허가 됩니다. 다음은 라이선스의 유형입니다.

  - **서버 라이선스**   실행 중인 서버 소프트웨어의 각 인스턴스에 대해 라이선스가 할당되어야 합니다. 서버 라이선스는 Standard Edition과 Enterprise Edition, 이렇게 2개의 서버 에디션으로 판매됩니다.

  - **CAL(클라이언트 액세스 라이선스)**   또한 Exchange 2013은 Standard CAL 및 Enterprise CAL이라고도 하는 두 개의 CAL(클라이언트 액세스 라이선스) 에디션으로도 제공됩니다. 서버 에디션과 CAL 유형을 적절히 조합하여 사용할 수 있습니다. 예를 들어, Exchange 2013 Standard Edition과 함께 Enterprise CAL을 사용하고 마찬가지로 Exchange 2013 Enterprise Edition과 함께 Standard CAL을 사용할 수 있습니다.

Exchange 라이선스 유형에 대 한 자세한 내용은 [라이선스](https://go.microsoft.com/fwlink/p/?linkid=392675)를 참조 하십시오.


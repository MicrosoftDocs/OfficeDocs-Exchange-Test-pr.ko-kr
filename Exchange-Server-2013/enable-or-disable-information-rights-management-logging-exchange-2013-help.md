---
title: '사용 또는 사용 안함 정보 권한 관리 로깅: Exchange 2013 Help'
TOCTitle: 사용 또는 사용 안함 정보 권한 관리 로깅
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50483306
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 또는 사용 안함 정보 권한 관리 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-12_

Exchange Server 2013 를 모니터링 하 고 해결 IRM 작업 정보 권한 관리 (IRM) 로그를 사용할 수 있습니다. IRM 로깅은 기본적으로 사용 됩니다.

IRM 로그 매개 변수는 다음과 같은 일반적인 집합을 사용 하십시오.

  - *IrmLogEnabled*   사용 하거나 IRM 로깅 사용 하지 않도록 설정 합니다. 기본값: `$true`합니다.

  - *IrmLogMaxAge*   IRM 로그 파일의 최대 사용 기간을 지정합니다. 지정 된 기간 보다 오래 된 파일 삭제 됩니다. 기본값: 30 일입니다.

  - *IrmLogMaxDirectorySize*   IRM 로그를 포함 하는 디렉터리의 최대 크기를 지정 합니다. 디렉터리의 최대 파일 크기에 도달 하면 서버 먼저 가장 오래 된 로그 파일을 삭제 합니다. 기본값: 250MB입니다.

  - *IrmLogMaxFileSize*   각 IRM 로그 파일의 최대 크기를 지정합니다. 로그 파일을 지정 된 크기에 도달 하면 새 로그 파일이 만들어집니다. 기본값: 10MB입니다.

  - *IrmLogPath*   IRM 로그 디렉터리의 위치를 지정합니다. 기본값: `%ExchangeInstallPath%Logging\IRMLogs`합니다.

IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 각 절차를 완료 시간: 2 ~ 5 분입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "IRM 로깅 구성" 항목.

  - 서버에 로그온 하는 IRM을 사용할지 여부를 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. 셸을 사용 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 하는 서버에 로그온 하는 IRM을 사용 하도록 설정 하려면

사서함 서버에서 IRM 로그를 사용 하는이 예제입니다.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $true
```

자세한 구문 및 매개 변수 정보에 대 한 [Set-TransportService](https://technet.microsoft.com/ko-kr/library/jj215682\(v=exchg.150\))를 참조 하십시오.

## 셸을 사용 하 여 서버에 로그온 하는 IRM을 사용 하지 않도록 설정

이 예에서는 사서함 서버에서 로깅을 IRM 사용 하지 않도록 설정 합니다.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $false
```

자세한 구문 및 매개 변수 정보에 대 한 [Set-TransportService](https://technet.microsoft.com/ko-kr/library/jj215682\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

성공적으로 사용 하도록 설정 하거나 했는지 비활성화 하는 서버에 로그온 하는 IRM을 확인 하려면 IRM 설정을 검색 하려면 [Get-TransportService](https://technet.microsoft.com/ko-kr/library/jj215746\(v=exchg.150\)) cmdlet을 실행 합니다.

이 예에서는 EXCH01 서버에 모든 IRM 로깅 속성을 검색 합니다.

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*


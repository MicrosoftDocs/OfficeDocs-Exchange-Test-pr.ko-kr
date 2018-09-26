---
title: 'RollAlternateServiceAccountCredential.ps1 스크립트 문제해결: Exchange 2013 Help'
TOCTitle: RollAlternateServiceAccountCredential.ps1 스크립트 문제해결
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63914119
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# RollAlternateServiceAccountCredential.ps1 스크립트 문제해결

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-14_

이 항목에서는 솔루션 및 RollAlternateServiceAccountPassword.ps1 스크립트를 사용 하는 경우 발생할 수 있는 일반적인 오류에 대 한 정보를 제공 합니다.

## 클라이언트 액세스 서버 중 하나 이상을 암호도 업데이트할 수 없습니다.

## 문제

경우에 따라 스크립트를 사용 하 여 매개 변수 *ToEntireForest* 또는 *ToArrayMembers* 를 사용 하면 클라이언트 액세스 서버 중 하나 이상을 업데이트 하지 않을 수 있습니다.

## 문제 해결 방법

서버 확인 스크립트를 대상으로 모든 필수 서버 **Get-ClientAccessArray** cmdlet을 사용 하 여 다음 예제와 같이 합니다.

```powershell
Get-ClientAccessArray | fl members
```

업데이트에 실패 하는 서버는 클라이언트 액세스 배열 구성원 하는 여전히 하지 적절 하 게 업데이트 하는 경우 Exchange 설치 프로그램을 다시 실행 하 고 다시 서버에 클라이언트 액세스 서버 역할을 추가 합니다. 또한 *ToSpecificServers*매개 변수 사용 하 여 대상으로 하는 개별 서버를 지정할 수 있습니다.

## 일부 서버 스크립트에 응답 하지

## 문제

일부 경우에서 서버는 잘못 된 네트워크 연결 등 일시적인 오류로 인해 업데이트에 실패할 수 있습니다.

## 문제 해결 방법

확인 문제의 서버 네트워크 및 Active Directory 연결이 한 후 스크립트를 다시 시도 하십시오.

## 일부 배열 구성원은 오랜 시간 동안 서비스 로그 아웃

## 문제

서버 오랜 시간에 대 한 순환에서 이지만 여전히의 멤버가 배열에 **Get-ClientAccessArray cmdlet**에 의해 결정을 하는 경우 매개 변수 *ToArrayMembers* 및 *ToEntireForest*를 사용 하는 경우에 스크립트 기능 장애가 발생할 수도 있습니다. 동일한 문제가 발생 하는 서버에 영구 실패 있었지만 배포에서 완벽 하 게 제거 되지 않았는지 하는 경우에 발생 합니다.

## 문제 해결 방법

이 문제를 해결 하려면 Exchange 설치 프로그램을 사용 하 여 배포에서 서버를 제거 하거나 서버를 제거할 수 있을 때까지 유인된 모드에서 스크립트를 실행 합니다.

짧은 시간에 대 한 서버 작동이 중지 되었을는 하는 경우 Exchange 를 영구적으로 제거 하지 않으려면만 현재 서버를 대상으로 있도록 *ToSpecificServers* 매개 변수 사용 하 여 특정 서버에 대해 실행 하려면 스크립트를 조정할 수 있습니다. 또는 제거할 수 있습니다는 RPC 클라이언트 액세스 서비스는 응답 하지 않는 서버 Active Directory 개체에서 **Remove-ClientAccessArray** cmdlet을 사용 하 여 다음 예제와 같이 합니다.

```powershell
Remove-RPCClientAccess -Server Server.Contoso.com
```

RPC 클라이언트 액세스 서비스를 제거한 후 [Get-ClientAccessArray](https://technet.microsoft.com/ko-kr/library/dd297976\(v=exchg.150\)) 하 여 서버를 배열 구성원으로 반환 되지 않음 및 스크립트 대상 지정 되지 않습니다. 서버가 다시 작동 되는 즉시 **New-RpcClientAccess** cmdlet을 사용 하 여 RPC 클라이언트 액세스 서비스를 다시 추가할 수 있습니다. RPC 클라이언트 액세스 서비스를 다시 추가 될 때에 영향을 받는 서버에서 Microsoft Exchange 주소록 서비스를 다시 시작 해야 합니다.


> [!WARNING]
> 서버에서 RPC 클라이언트 액세스 서비스를 제거 하기 전에 <A href="https://technet.microsoft.com/ko-kr/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</A>항목 참조 하십시오.



## 자세한 내용

클라이언트 액세스 서버 배열 또는 부하 분산 솔루션을 함께 Kerberos 인증을 사용 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [부하 분산 된 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [셸에서 RollAlternateserviceAccountCredential.ps1 스크립트를 사용 하 여](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)


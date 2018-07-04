---
title: '페더레이션 인증서를 갱신: Exchange 2013 Help'
TOCTitle: 페더레이션 인증서를 갱신
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429170
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 인증서를 갱신

 

_**마지막으로 수정된 항목:** 2017-02-28_

이 항목에서는 페더레이션 트러스트에 사용 되는 페더레이션 자체 서명 된 인증서를 업데이트 하는 방법에 설명 합니다.

  - 페더레이션 인증서 만료 되지 않았으면 하는 경우 작업 페더레이션 인증서를 업데이트 섹션의 단계를 수행 합니다.

  - 페더레이션 인증서가 이미 만료 된 경우에 페더레이션 만료 된 인증서를 교체 섹션의 단계를 수행 합니다.

페더레이션 트러스트 및 페더레이션 하는 방법에 대 한 자세한 내용은 [페더레이션](federation-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 "페더레이션 및 인증서" 항목.

  - 이 항목의 절차에서는 Exchange 관리 셸 를 사용합니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요.

  - 기존 페더레이션 인증서가 만료 된 경우를 보려면 Exchange 관리 셸 에서 다음 명령을 실행 합니다.
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

> [!CAUTION]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>


## 작업 페더레이션 인증서를 업데이트 합니다.

페더레이션 인증서 만료 되지 않았으면 하는 경우 새 페더레이션 인증서 사용 하 여 기존 페더레이션 트러스트를 업데이트할 수 있습니다.

## 1 단계: 새 페더레이션 인증서 만들기

새 페더레이션 인증서를 만들려면 Exchange 관리 셸 에 다음 명령을 실행 합니다.

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

구문과 매개 변수에 대한 자세한 내용은 [New-ExchangeCertificate](https://technet.microsoft.com/ko-kr/library/aa998327\(v=exchg.150\))를 참조하십시오.

명령 출력 새 인증서의 지문 값을 포함합니다. 나머지 단계에서이 값이 필요 하 고 Exchange 관리 셸 창에서 직접 값을 복사할 수 있습니다.

1.  Exchange 관리 셸 창에서 마우스 오른쪽 단추로 클릭 하 고 나타나는 대화 상자에서 **표시** 를 선택 합니다.

2.  지문 값을 선택 하 고 ENTER 키를 누릅니다.

이 항목의 다른 절차에서는에서는 페더레이션 인증서 지문 값: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`합니다. 사용자가 인증서 지문 값 다른 됩니다.

## 2 단계: 페더레이션 인증서로 새 인증서 구성

페더레이션 인증서로 새 인증서를 구성 하려면 Exchange 관리 셸 을 사용 하려면 다음 구문을 사용 합니다.

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

이 예제에서는 1 단계에서에서 인증서 지문을 값 `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73` 를 사용 합니다.

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

자세한 구문 및 매개 변수 정보에 대 한 [Set-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd298034\(v=exchg.150\))을 참조 하십시오.

**참고:**  명령 출력 DNS에서 TXT 레코드 도메인 소유권 증명을 업데이트 해야 알리는 경고 메시지를 포함 합니다. 다음 단계에는 작업을 수행 합니다.

## 3 단계: 도메인 소유권 외부 DNS에서 TXT 레코드의 페더레이션 증명 업데이트

TXT 레코드 도메인 소유권 증명 (5 단계) 정품 인증 하는 동안만 검사 하기 때문에 지금,이 단계를 수행할 수 안전 하 게 합니다. 그러나 TXT 레코드를 업데이트 한 후 및 다음 단계를 계속 하기 전에 (지속 시간 또는 DNS 레코드의 TTL 값에 따라) 전파할 업데이트 된 TXT 레코드에 대 한 시간을 허용 해야 합니다.

1.  필요한 TXT 레코드 Exchange 관리 셸 에 다음 명령을 실행 하 여 필요한 값을 찾습니다.
    
        Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    
    예, contoso.com 페더레이션된 도메인을 사용 하는 경우에 다음 명령을 실행 합니다.
    
        Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    
    명령 출력은 다음과 같습니다.
    
    `Thumbprint : <new certificate thumbprint>` (예: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)
    
    `Proof      : <new hash text>` (예: `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)
    
    `Thumbprint : <old certificate thumbprint>` (예: `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)
    
    `Proof      : <old hash text>` (예: `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    
    명령 출력을는 도메인의 두 증명에 대 한 정보 소유권 레코드를 반환: 대체 하는 현재 인증서에 대 한 새 인증서에 대 한 개와 합니다. 지문 값 및 외부 (공용) DNS에서 TXT 레코드는 현재 도메인 소유권 증명에 구성 된 해시 텍스트 값은 하는 것을 알 수 있습니다.

2.  도메인 소유권 외부 DNS에서 TXT 레코드의 페더레이션 증명을 업데이트 합니다. 지침 DNS 공급자에 따라 달라 집니다 하지만 새 해시 텍스트 값을 가진 현재 해시 텍스트 값을 바꾸려면 현재 TXT 레코드를 편집할 수 있습니다. 자세한 내용은 [Office 365에 대 한 외부 도메인 이름 시스템 레코드](https://go.microsoft.com/fwlink/p/?linkid=265522)의 Exchange Online 섹션을 참조 하십시오.

## 4 단계: 모든 Exchange 서버에 새 페더레이션 인증서의 배포를 확인 하십시오.

모든 서버에 새 페더레이션 인증서를 자동으로 배분 하는 Exchange 하지만 계속할 수 분포를 확인 해야 합니다.

새 페더레이션 인증서의 배포를 확인 하려면 Exchange 관리 셸 를 사용 하려면 다음 명령을 실행 합니다.

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**참고:**  **Test-FederationCertificate** cmdlet의 출력을 Exchange 2010 서버 이름을 포함 합니다. Exchange 2013 또는 나중에 cmdlet의 출력에는 서버 이름은 포함 되지 않습니다.

## 5 단계: 새 페더레이션 인증서를 활성화 합니다.

새 페더레이션 인증서를 활성화 하려면 Exchange 관리 셸 을 사용 하려면 다음 명령을 실행 합니다.

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate

자세한 구문 및 매개 변수 정보에 대 한 [Set-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd298034\(v=exchg.150\))을 참조 하십시오.

**참고:**  명령 출력 (이미 수행한 단계 3에서)는 DNS에서 TXT 레코드 도메인 소유권 증명을 업데이트 하는 경고를 포함 합니다.

## 작동 여부는 어떻게 확인합니까?

새 페더레이션 인증서를 사용 하 여 기존 페더레이션 트러스트를 성공적으로 업데이트 했을 때 있는지를 확인 하려면 다음이 단계를 사용 합니다.

  - Exchange 관리 셸 에서 새 인증서를 사용 하는지 확인 하려면 다음 명령을 실행 합니다.
    
        Get-FederationTrust | Format-List *priv*
    
      - **OrgPrivCertificate** 속성에는 새 페더레이션 인증서의 지문을 포함 되어야 합니다.
    
      - **OrgPrevPrivCertificate** 속성에는 이전 (교체) 페더레이션 인증서의 지문을 포함 되어야 합니다.

  - Exchange 관리 셸 에서 사용자 조직에 있는 사용자의 전자 메일 주소를 가진 *\<user's email address\>* 바꾸고 페더레이션 트러스트가 제대로 작동 하는지 확인 하려면 다음 명령을 실행 합니다.
    
        Test-FederationTrust -UserIdentity <user's email address>

## 만료 된 페더레이션 인증서를 교체

페더레이션 인증서가 이미 만료 된 경우 해야 페더레이션 트러스트에서 모든 페더레이션된 도메인을 제거 하 고 다음을 제거 하 고 페더레이션 트러스트를 다시 만듭니다.

1.  여러 페더레이션된 도메인을 설치한 경우 마지막 제거할 수 있도록 기본 도메인 공유 되는 도메인을 식별 해야 합니다. 기본 공유 도메인 및 모든 페더레이션된 도메인을 확인 하려면 Exchange 관리 셸 을 사용 하려면 다음 명령을 실행 합니다.
    
        Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    
    **AccountNamespace** 속성의 값 형식 `FYDIBOHF25SPDLT<primary shared domain>`에서 기본 공유 도메인을 포함합니다. 예 값 `FYDIBOHF25SPDLT.contoso.com`contoso.com 공유 되는 기본 도메인을 됩니다.

2.  Exchange 관리 셸 에서 다음 명령을 실행 하 여 기본 공유 도메인 아닌 각 페더레이션된 도메인을 제거 합니다.
    
        Remove-FederatedDomain -DomainName <domain> -Force

3.  다른 모든 페더레이션된 도메인을 제거한 후 Exchange 관리 셸 에서 다음 명령을 실행 하 여 기본 공유 되는 도메인을 제거 합니다.
    
        Remove-FederatedDomain -DomainName <domain> -Force

4.  Exchange 관리 셸 에 다음 명령을 실행 하 여 페더레이션 트러스트를 제거 합니다.
    
        Remove-FederationTrust "Microsoft Federation Gateway"

5.  페더레이션 트러스트를 다시 만듭니다. 자세한 내용은 [페더레이션 트러스트 만들기](https://technet.microsoft.com/ko-kr/library/dd335198\(v=exchg.150\))을 참조 하십시오.


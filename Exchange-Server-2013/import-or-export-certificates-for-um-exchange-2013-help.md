---
title: '가져오기 또는 UM에 대 한 인증서를 내보내려면: Exchange 2013 Help'
TOCTitle: 가져오기 또는 UM에 대 한 인증서를 내보내려면
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54651843
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 가져오기 또는 UM에 대 한 인증서를 내보내려면

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-12-18_

EAC 또는 셸을 사용하여 자체 서명된 인증서, 내부 PKI(공개 키 인프라) 인증서 또는 타사의 상업용 인증서를 가져오거나 내보낼 수 있습니다. UM(통합 메시징)의 경우에는 Microsoft Exchange 통합 메시징 서비스와 Microsoft Exchange 통합 메시징 통화 라우터 서비스에 대해 이러한 인증서 중 하나를 사용할 수 있습니다. 두 서비스에 대해 같은 인증서를 사용해도 되고 서비스마다 다른 인증서를 사용해도 됩니다.

다음과 같은 경우 Exchange용 인증서를 가져오면 유용할 수 있습니다.

  - 파일로 내보낸 인증서를 가져오려는 경우

  - 내부 인증 기관에서 생성한 PKI 인증서를 가져오려는 경우

  - 타사 상업용 인증서를 가져오려는 경우

다음과 같은 경우 로컬 Exchange 서버의 인증서 저장소에서 기존 인증서를 내보내면 유용할 수 있습니다.

  - 다른 Exchange 서버에서 가져올 수 있도록 인증서를 내보내려는 경우

  - VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX에서 가져올 수 있도록 인증서를 내보내려는 경우

  - 인증서 및 해당 개인 키를 백업할 수 있도록 인증서를 내보내려는 경우

통합 메시징용 인증서 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 절차에 대 한 인증서를 배포합니다.](deploying-certificates-for-um-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "인증서 관리" 항목 및 [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 서비스" 항목 역시 해당 컴퓨터의 로컬 관리자 그룹 구성원인 계정을 사용하여 로그온해야 합니다.

  - 인증서를 내보내기 전에 **Get-ExchangeCertificate** cmdlet을 사용하여 인증서의 *PrivateKeyExportable* 특성이 `$true`로 설정되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 인증서 내보내기

1.  EAC에서 **서버** \> **인증서** \> **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")을 클릭하고 **Exchange 인증서 내보내기**를 클릭합니다.

2.  **Exchange 인증서 내보내기** 페이지의 **내보낼 파일** 상자에 인증서 파일의 이름을 입력합니다.

3.  **암호** 상자에 개인 키를 보호하는 데 사용할 암호를 입력한 후 **확인**을 클릭합니다.

## 셸을 사용하여 인증서 내보내기

이 예에서는 사용자 이름과 암호를 입력하라는 메시지가 표시된 후 지문 A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC가 포함된 인증서를 파일로 내보냅니다.

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

이 예에서는 다음을 수행합니다.

1.  **Get-ExchangeCertificate** cmdlet을 사용하여 내보낼 인증서를 찾습니다.

2.  **Export-ExchangeCertificate** cmdlet을 사용하여 인증서의 암호를 설정합니다.

3.  사용자 이름과 암호를 입력한 후 인증서를 파일로 출력합니다.

<!-- end list -->
  ```
    $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
  ```
  ```
```powershell
Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
```
  ```

## EAC를 사용하여 인증서 가져오기

1.  EAC에서 **서버** \> **인증서** \> **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")을 클릭하고 **Exchange 인증서 가져오기**를 클릭합니다.

2.  **Exchange 인증서 가져오기** 페이지의 **가져올 파일** 상자에 인증서 파일의 공유 폴더 경로와 이름을 입력합니다. 인증서가 암호로 보호되어 있으면 **암호** 상자에 암호를 입력하고 **다음**을 클릭합니다.

3.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 인증서를 적용할 서버를 선택한 후 **확인**을 클릭합니다. 목록 보기에서 서버를 제거하려면 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하고 **마침**을 클릭합니다.

## 셸을 사용하여 인증서 가져오기

이 예에서는 사용자 이름과 암호를 입력한 후 d:\\certificates\\exchange\\SelfSignedUMCert.pfx 인증서 파일에서 인증서를 가져옵니다.

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password


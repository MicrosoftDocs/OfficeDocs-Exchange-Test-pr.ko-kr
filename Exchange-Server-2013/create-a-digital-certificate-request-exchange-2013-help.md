---
title: '디지털 인증서 요청 만들기: Exchange 2013 Help'
TOCTitle: 디지털 인증서 요청 만들기
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52058147
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 디지털 인증서 요청 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-21_

Exchange Server 2013 EAC 또는 셸을 사용 하 여 인증서를 관리할 수 있습니다. EAC는 새 인증서 관리 사용자 인터페이스를 포함합니다. 이 새로운 UI를 통해 새 인증서 만들기, 기존 인증서를 편집 또는 인증서를 제거할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10 분 + 인증 기관에 대 한 응답에 대 한 시간입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "클라이언트 액세스 서버 보안" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 새 인증서 요청을 만들려면

1.  EAC에서 **서버** \> **인증서**로 이동합니다.

2.  **서버 선택** 목록에서 인증서를 만들려는 서버를 선택 하 고![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 합니다.

3.  **새 Exchange 인증서** 마법사에서 **인증 기관의 인증서에 대 한 요청 만들기** 또는 **자체 서명 된 인증서 만들기** 를 선택 하 고 을 선택 합니다.

4.  인증서에 대 한 친숙 한 이름을 입력 하 고 을 선택 합니다.

5.  자체 서명 된 인증서를 선택 하지 않은 경우 와일드 카드 인증서 **와일드 카드 인증서를 요청** 하는 표시 된 상자를 선택, 예는 루트 도메인을 입력 \*. contoso.com, 하 고 다음 선택 **다음** 합니다. 자체 서명 된 인증서를 선택한 경우이 단계를 건너뜁니다.

6.  이 인증서를 적용 하 고 **다음** 을 선택 하려면 서버를 선택 합니다.

7.  인증서에 포함 되어야 하 고 **다음** 을 선택 하려는 도메인을 지정 합니다.

8.  포함 된 도메인이 올바른지 확인 합니다. 자체 서명 된 인증서를 선택한 경우 **완료 날짜** 를 선택 합니다. 그렇지 않은 경우 **다음** 을 선택 합니다.

9.  사용자 조직 이름, 부서 이름, 도시 군/시, 상태 또는 시/도, 및 국가 또는 지역를 입력 하 고 을 선택 합니다.

10. 인증서 요청을 저장 하 고 **완료 날짜** 를 선택 하려면 위치를 입력 합니다.

자체 서명 된 인증서를 선택 하지 않은 경우에 처리에 대 한 인증 기관에 인증서 요청 파일을 보낼 필요 합니다.

## 셸을 사용 하 여 새 인증서 요청을 만들려면

다음 명령을 실행 합니다.

  ```
    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
  ```
  
  ```
```powershell
$reqfile | out-file c:\certreq.txt
```
  ```

## 작동 여부는 어떻게 확인합니까?

자체 서명 된 인증서를 만든 경우 새로 만든된 인증서는 인증서 관리 UI에에서 표시 됩니다. 인증 기관에서 인증서 요청을 만든 경우에 지정한 위치에 인증서 요청 파일이 됩니다. 인증 기관에는이 파일을 보냅니다.


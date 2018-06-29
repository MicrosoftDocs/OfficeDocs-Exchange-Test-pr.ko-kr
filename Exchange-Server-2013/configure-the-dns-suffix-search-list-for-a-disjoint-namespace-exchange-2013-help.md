---
title: '분리 된 네임 스페이스에 대 한 DNS 접미사 검색 목록을 구성 합니다.: Exchange 2013 Help'
TOCTitle: 분리 된 네임 스페이스에 대 한 DNS 접미사 검색 목록을 구성 합니다.
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50484238
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 분리 된 네임 스페이스에 대 한 DNS 접미사 검색 목록을 구성 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 GPMC(그룹 정책 관리 콘솔)를 사용하여 DNS(Domain Name System) 접미사 검색 목록을 구성하는 방법에 대해 설명합니다. 일부 Microsoft Exchange 2013 시나리오의 경우 연결되지 않은 네임스페이스가 있으면 복수 DNS 접미사를 포함하도록 DNS 접미사 검색 목록을 구성해야 합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - 이 절차를 수행하려면 사용하는 계정이 도메인 관리자 그룹 구성원을 위임받아야 합니다.

  - GPMC를 설치할 컴퓨터에 .NET Framework 3.0이 설치되어 있는지 확인합니다.
    

    > [!NOTE]
    > Microsoft 다운로드 센터에서 다운로드할 수 있는 현재 GPMC 버전은 32비트 버전의 Windows Server 2003 및 Windows XP 운영 체제에서 작동하며 32비트 및 64비트 도메인 컨트롤러에서 그룹 정책 개체를 원격으로 관리할 수 있습니다. 이 GPMC 버전에는 64비트 버전이 포함되지 않으며 32비트 버전은 64비트 플랫폼에서 실행되지 않습니다. 32비트 버전의 Windows Server 2008&nbsp;및 32비트 버전의 Windows Vista에는 모두 32비트 버전의 GPMC가 포함됩니다. 64비트 버전의 Windows Server 2008&nbsp;및 64비트 버전의 Windows Vista에는 모두 64비트 버전의 GPMC가 포함됩니다.



  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## GPMC를 사용하여 DNS 접미사 검색 목록 구성

1.  사용자 도메인의 32 비트 컴퓨터에서 서비스 팩 1 (SP1) GPMC를 설치 합니다. 다운로드 정보에 대 한 [그룹 정책 관리 콘솔 서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=100126)를 참조 하십시오.
    

    > [!NOTE]
    > 도메인에 Windows Server 2008 또는 Windows Vista를 실행하는 컴퓨터가 있을 경우 이 단계를 건너뛸 수 있습니다.



2.  **시작** \> **프로그램** \> **관리 도구** \> **그룹 정책 관리**를 클릭합니다.

3.  **그룹 정책 관리**에서 그룹 정책을 적용할 포리스트와 도메인을 확장합니다. **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 클릭합니다.

4.  **새 GPO**에서 정책 이름을 입력한 후 **확인**을 클릭합니다.

5.  4단계에서 만든 새 정책을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.

6.  **그룹 정책 관리 편집기**에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **네트워크**를 차례로 확장한 다음 **DNS 클라이언트**를 클릭합니다.

7.  **DNS 접미사 검색 목록**을 마우스 오른쪽 단추로 클릭한 다음 **모든 작업**, **편집**을 차례로 클릭합니다.

8.  **DNS 접미사 검색 목록 속성** 페이지에서 **사용**을 선택합니다. **DNS 접미사** 상자에 연결되지 않은 컴퓨터의 주 DNS 접미사, DNS 도메인 이름 및 Exchange가 상호 작용하는 다른 서버(예: 모니터링 서버 또는 타사 응용 프로그램용 서버)에 대한 추가 네임스페이스를 입력합니다. **확인**을 클릭합니다.

9.  **그룹 정책 관리**에서 **그룹 정책 개체**를 확장한 다음 4단계에서 만든 정책을 선택합니다. **범위** 탭에서 정책이 연결되지 않은 컴퓨터에만 적용되도록 범위를 지정합니다.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - Exchange 2013을 설치한 후 조직 내부와 외부에서 전자 메일 메시지를 보낼 수 있는지 확인합니다.

## 자세한 내용

[Windows Server 그룹 정책](https://go.microsoft.com/fwlink/p/?linkid=100128)

[그룹 정책](https://go.microsoft.com/fwlink/?linkid=268043)

[분리 된 네임 스페이스 시나리오](disjoint-namespace-scenarios-exchange-2013-help.md)


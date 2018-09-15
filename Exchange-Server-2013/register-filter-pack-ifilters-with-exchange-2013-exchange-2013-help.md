---
title: 'Exchange 2013으로 Filter Pack IFilter 등록: Exchange 2013 Help'
TOCTitle: Exchange 2013으로 Filter Pack IFilter 등록
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50555932
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013으로 Filter Pack IFilter 등록

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

첨부 파일 검색 조건이 포함된 전송 규칙은 첨부 파일의 콘텐츠를 분석할 때 텍스트 추출을 수행합니다. Exchange 2013은 기본적으로 가장 흔히 사용되는 첨부 파일 형식을 검색할 수 있습니다. Exchange 2013에 IFilter를 등록하면 추가 첨부 파일 형식을 포함할 수 있습니다. 이 항목에서는 Microsoft 및 타사 공급자가 릴리스한 IFilter를 등록하는 방법을 보여 줍니다.

특정 파일 형식에 대한 IFilter를 등록하고 나면 첨부 파일 처리 조건이 포함된 전송 규칙은 이러한 첨부 파일을 검색할 수 있습니다. 따라서 이러한 파일 형식이 더 이상 *AttachmentIsUnsupported* 조건을 트리거하지 않습니다.


> [!WARNING]
> 이 항목에 나오는 절차에는 Exchange 서버의 레지스트리를 수정하는 작업이 포함됩니다. 레지스트리를 잘못 편집하면 운영 체제를 다시 설치해야 할 수 있는 심각한 문제가 발생할 수 있습니다. 잘못된 레지스트리 편집으로 인한 문제는 해결하지 못할 수도 있습니다. 레지스트리를 편집하기 전에 중요한 데이터를 백업해 두십시오.<BR>또한 각 절차를 따르려면 사서함 서버에서 Microsoft Exchange Transport Service를 중지했다가 다시 시작해야 합니다.



전송 규칙과 관련된 추가 관리 작업에 대한 자세한 내용은 [메일 흐름 규칙 관리](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 서버당 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "Exchange 서버 구성 설정" 항목

  - 아래 절차는 Exchange 2013 사서함 서버 역할이 이미 설치된 서버에서 수행해야 합니다. 이러한 절차를 수행한 후에 다른 사서함 서버를 추가하려면 새로 프로비전된 서버에서 동일한 절차를 다시 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## Microsoft Office 2010 Filter Pack 등록

기본적으로 다음 Office 파일 형식은 Exchange 전송 규칙에서 지원되지 않습니다.

  - Office OneNote

  - Office Publisher

이러한 파일을 지원하려면 Microsoft Office 2010 Filter Pack을 배포해야 합니다. 이 Filter Pack은 Exchange 2013 설치 중에 배포되지 않으며 배포 필수 구성 요소도 아닙니다.

## Microsoft Office 2010 Filter Pack 배포

Office 2010 Filter Pack 배포는 두 가지 주요 단계로 구성됩니다.

  - IFilter를 Windows (Search)에 등록하기 위한 Filter Pack 다운로드 및 설치

  - iFilter가 Exchange 2013에도 등록되도록 레지스트리 수정. 이를 통해 Exchange가 파일 형식에 대한 첨부 파일 검색을 지원할 수 있습니다.


> [!IMPORTANT]
> 이 절차는 조직의 모든 사서함 서버에서 수행해야 합니다.



1.  다운로드 하 고 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=191548)에서 Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`)를 저장 합니다.

2.  사서함 서버에서 `FilterPack64bit.exe` 파일을 실행하고 지시에 따라 설치를 완료합니다.

3.  레지스트리 편집기를 시작하여 다음 레지스트리 하위 키를 찾습니다.
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  **CLSID**에서 OneNote 파일에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **CLSID**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`로 변경합니다.
    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 Office 2010 Filter Pack을 설치한 위치로 설정합니다. 기본적으로 Filter Pack은 `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`에 설치됩니다.
    
    4.  <strong>{B8D12492-CE0F-40AD-83EA-099A03D493F1}</strong>을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **문자열 값**을 클릭합니다.
    
    5.  새 문자열 값의 이름을 `ThreadingModel`로 지정하고 그 값을 `Both`로 설정합니다.

5.  **CLSID**에서 Publisher 파일에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **CLSID**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`로 변경합니다.
    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 Office 2010 Filter Pack을 설치한 위치로 설정합니다. 기본적으로 Filter Pack은 `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`에 설치됩니다.
    
    4.  <strong>{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}</strong>를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **문자열 값**을 클릭합니다.
    
    5.  새 문자열 값의 이름을 `ThreadingModel`로 지정하고 그 값을 `Both`로 설정합니다.

6.  레지스트리 키
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  **필터**에서 .one 확장명에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **필터**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `.one`로 변경합니다.
    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`로 설정합니다.

8.  **필터**에서 .pub 확장명에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **필터**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `.pub`로 변경합니다.
    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`로 설정합니다.

9.  레지스트리 편집기를 닫습니다.

10. 사서함 서버에서 다음 서비스를 지정된 순서대로 중지했다가 다시 시작합니다.
    
    1.  Microsoft Exchange Transport Service를 중지합니다.
    
    2.  Microsoft Filtering Management Service를 중지합니다.
    
    3.  Microsoft Filtering Management Service를 시작합니다.
    
    4.  Microsoft Exchange 전송 서비스를 시작합니다.

## 작동 여부는 어떻게 확인합니까?

Microsoft Office 2010 Filter Pack IFilter를 성공적으로 등록했는지 확인하려면 다음 작업을 수행하십시오.

1.  다음 속성을 사용하여 전송 규칙을 만듭니다. 전송 규칙을 만드는 방법에 대한 자세한 내용은 [메일 흐름 규칙 관리](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)를 참조하십시오.
    
      - 보낸 사람이 다음과 같음: 내 사서함
    
      - 첨부 파일 내용에 다음 포함: "Testing IFilters"
    
      - 문제 보고서 생성 및 다음으로 보내기: 내 사서함

2.  "Testing IFilters"라는 구문이 포함된 OneNote를 만들어 새 전자 메일 메시지에 첨부한 다음 이를 자신에게 보냅니다.

3.  방금 만든 규칙에 대한 전송 규칙 문제 보고서가 수신되는지 확인합니다. 이를 통해 규칙 엔진이 OneNote 파일의 내용을 분석할 수 있었음을 알 수 있습니다.

4.  Publisher 파일로 2단계와 3단계를 반복합니다.

## 타사 IFilter를 등록하여 추가 파일 형식 지원

타사 IFilter를 추가로 등록하여 다른 파일 형식에 대해 첨부 파일 검색 기능을 확장할 수 있습니다. 추가 파일에 대한 지원은 각 사서함 서버에 파일 형식의 IFilter를 설치 및 등록하여 추가할 수 있습니다.


> [!IMPORTANT]
> Microsoft에서는 전송 규칙을 사용하여 타사 IFilter를 테스트하지 않았으므로 프로덕션 환경에 배포하기 전에 테스트 환경에서 타사 IFilter를 배포하고 테스트하는 것이 좋습니다.



## Adobe PDF IFilter 배포

이 절차에서는 전송 규칙에서 PDF 첨부 파일의 처리를 지원 하기 위해 [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) 를 배포 하는 방법을 보여줍니다.


> [!NOTE]
> 기본적으로 Exchange 2013은 전송 규칙에서 PDF 파일의 검색을 지원합니다. 여기에 나오는 PDF 예는 타사 IFilter를 사용하여 추가 파일 형식에 대해 지원을 확장할 수 있는 방법을 보여 주기 위해 간단히 사용됩니다.



1.  [Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)를 다운로드 하 고 설치 지침을 따릅니다.

2.  레지스트리 편집기를 시작하여 다음 하위 키를 찾습니다.
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  **CLSID**에서 PDF 파일에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **CLSID**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`로 변경합니다.
        

        > [!NOTE]
        > 각 IFilter에는 고유한 클래스 ID(CLSID)가 있습니다. 등록할 IFilter에 대한 설치 설명서에서 또는 레지스트리의 <CODE>HKEY_CLASSES_ROOT\CLSID</CODE> 키 하위에 있는 파일 확장명을 검색하여 CLSID를 찾을 수 있습니다.

    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 PDF IFilter를 설치한 위치로 설정합니다. 기본적으로 PDF IFilter는 `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`에 설치됩니다.

4.  레지스트리 키
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  **필터**에서 .pdf 확장명에 대한 하위 키를 다음과 같이 추가합니다.
    
    1.  **필터**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    2.  새 키의 이름을 `.pdf`로 변경합니다.
    
    3.  방금 만든 키를 클릭하고 **(기본값)** 값을 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`로 설정합니다.

6.  레지스트리 편집기를 닫습니다.

7.  사서함 서버에서 다음 서비스를 지정된 순서대로 중지했다가 다시 시작합니다.
    
    1.  Microsoft Exchange Transport Service를 중지합니다.
    
    2.  Microsoft Filtering Management Service를 중지합니다.
    
    3.  Microsoft Filtering Management Service를 시작합니다.
    
    4.  Microsoft Exchange 전송 서비스를 시작합니다.

## 작동 여부는 어떻게 확인합니까?

이 항목의 앞부분에 나오는 How do you know this worked? 섹션에 설명된 절차를 사용합니다. 이때 Publisher 파일은 Adobe PDF 파일로 대체합니다.

## 자세한 내용

[전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)


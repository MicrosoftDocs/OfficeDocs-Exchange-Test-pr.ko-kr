---
title: '보존 태그 내보내기 및 가져오기: Exchange 2013 Help'
TOCTitle: 보존 태그 내보내기 및 가져오기
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51407671
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보존 태그 내보내기 및 가져오기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-11-15_

다음을 포함하여 보존 태그를 내보내거나 가져오는 여러 가지 시나리오가 있습니다.

  - 다중 포리스트 Exchange 조직의 모든 서버에에서 걸쳐 동일한 보존 정책 적용

  - 사서함이 온-프레미스 Exchange 조직과 Exchange Online에 나눠져 있는 하이브리드 배포에 동일한 보존 정책 적용

  - 사용자가 온-프레미스 Exchange 2010 또는 이상 사서함의 클라우드 기반 보관이 있는 Exchange 보관 시나리오에서 보존 정책을 적용 합니다.

이러한 시나리오에서 관리되는 폴더 도우미는 항목이나 사서함이 다른 조직으로 이동된 후에 보존 태그가 적용된 항목을 올바르게 처리할 수 있습니다.


> [!WARNING]
> 두 조직 간에 보존 태그와 보존 정책을 동기화하려면 원본 조직에서 보존 태그나 정책을 변경할 때마다 이 절차를 수행하여 원본 조직에서 보존 태그 및 정책을 내보내고 대상 조직에 가져옵니다.<BR>내보낼 특정 보존 태그나 정책을 선택할 수 없습니다. Export-RetentionTags.ps1 스크립트는 조직에서 모든 보존 태그와 정책을 내보냅니다.



메시징 레코드 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "메시징 레코드 관리" 항목

  - 이 항목의 절차에서는Exchange 서버에서 `%ExchangeInstallPath%Scripts` 폴더에 이러한 세 파일에 따라 달라 집니다.
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - 내보내거나 가져올 특정 보존 태그나 정책을 선택할 수 없습니다. Export-RetentionTags.ps1 스크립트는 조직에서 모든 보존 태그와 정책을 내보냅니다. Import-RetentionTags.ps1 스크립트는 가져오는 XML 파일의 모든 보존 태그 및 정책을 가져와서 Exchange 조직의 모든 기존 보존 태그 및 정책을 바꿉니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 1 단계: 온-프레미스 Exchange 조직에서 보존 태그 내보내기

1.  디렉터리에서 Exchange 설치 경로에 **스크립트** 하위 디렉터리를 변경 하려면이 Exchange 관리 셸 명령을 실행 합니다.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Export-RetentionTags.ps1 스크립트를 실행하여 보존 태그를 .xml 파일로 내보냅니다.
    

    > [!IMPORTANT]
    > 가져오기 (영문) 또는 보존 태그 및 보존 정책 Exchange Online 로 내보내기 하는 경우에 Exchange Online 에 Windows PowerShell 세션을 연결 해야 합니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/jj984289(v=exchg.150)">원격 PowerShell을 사용하여 Exchange Online에 연결</A>를 참조 합니다.

    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 작동 여부는 어떻게 확인합니까?

보존 태그와 보존 정책을 내보냈는지 확인하려면 다음을 수행합니다.

1.  내보내기 명령에서 지정했던 경로로 이동하여 지정한 이름의 XML 파일이 만들어졌는지 확인합니다.

2.  원하는 경우 텍스트 편집기에서 XML 파일을 열어 해당 내용을 검토할 수 있습니다.

## 2 단계: Exchange 조직에 보존 태그 가져오기

1.  디렉터리에서 Exchange 설치 경로에 **스크립트** 하위 디렉터리를 변경 하려면이 Exchange 관리 셸 명령을 실행 합니다.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Import-RetentionTags.ps1 스크립트를 실행하여 이전에 내보낸 XML 파일에서 보존 태그를 가져옵니다.
    

    > [!IMPORTANT]
    > 가져오기 (영문) 또는 보존 태그 및 보존 정책 Exchange Online 로 내보내기 하는 경우에 Exchange Online 에 Windows PowerShell 세션을 연결 해야 합니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/jj984289(v=exchg.150)">원격 PowerShell을 사용하여 Exchange Online에 연결</A>를 참조 합니다.

    

    > [!NOTE]
    > Exchange Online 에 대해이 스크립트를 실행할 때에 신뢰할 수 없는 게시자를에서 소프트웨어를 실행 하려면 확인 하 라는 메시지가 표시 될 수 있습니다. 게시자의 이름을 <CODE>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</CODE>나타나는지 확인 하 고 스크립트를 한 번 실행할 수 있도록 하려면 <STRONG>R</STRONG> 또는 <STRONG>A</STRONG> 항상 실행을 클릭 합니다.

    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 작동 여부는 어떻게 확인합니까?

보존 태그와 보존 정책을 가져왔는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **준수 관리** \> **보존 태그**로 이동한 후 보존 태그를 가져왔는지 확인합니다. **준수 관리** \> **보존 태그**로 이동한 후 보존 정책을 가져왔는지 확인합니다.

2.  태그 및 정책이 만들어졌는지 확인 하려면 **Get-RetentionPolicy** 및 **Get-RetentionPolicyTag** cmdlet을 사용 합니다. 보존 태그 및 보존 정책을 검색 하는 방법에 대 한 예 [Get-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298009\(v=exchg.150\)) 및 [Get-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd298086\(v=exchg.150\))에서 예를 참조 하십시오.


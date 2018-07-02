---
title: '예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비: Exchange 2013 Help'
TOCTitle: 예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50484493
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2013 사서함 이동 및 **New-MoveRequest** 및 **New-MigrationBatch** cmdlet을 사용 하 여 마이그레이션을 지원 합니다. Exchange 관리 센터 (EAC)를 통해 사서함을 이동할 수도 있습니다. 대상 Exchange 2010 포리스트에 원본 Exchange 포리스트의 사서함을 이동할 수 있습니다.

**New-MoveRequest**를 실행 하려면 메일 사용자를 대상 Exchange 포리스트에 있어야 하 고 메일 사용자에 필요한 Active Directory 특성의 최소 집합 있어야 합니다. 합니다. Microsoft 수명 주기 ILM (Identity Manager) 2007 배포를 사용자 지정 하 여 대상 Exchange 포리스트에서 필요한 메일 사용자를 만들 수 있습니다. 이 항목에 설명 된 ILM 기반 규칙 확장 샘플 코드 대상 Exchange 2013 포리스트에서 필요한 메일 사용이 가능한 사용자를 만들려면 현재 ILM 배포를 사용자 지정 하는 방법을 보여줍니다.

필요한 Active Directory 특성에 대 한 설명이 포함 하는 크로스 포리스트 이동 준비 하는 방법에 대 한 자세한 내용은 [크로스 포리스트 이동 요청에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - Microsoft 다운로드 센터에서 [온라인 사서함 이동에 대 한 준비](https://go.microsoft.com/fwlink/p/?linkid=177882) 페이지에서 예제 코드를 다운로드 합니다.

  - 예제 코드를 실행 하려면 ILM 2007 기능 팩 1 서비스 팩 1 (SP1) 해야 합니다. 기능 팩을 다운로드 하려면 Microsoft 기술 자료 문서 977791, [서비스 팩 1 (빌드 3.3.1139.2) Identity Lifecycle Manager 2007 기능 팩 1에 대 한 교육은](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=977791)를 참조 하십시오.

  - 또한 다음이 필요 합니다.
    
      - Exchange 2013을 실행하며 사서함이 현재 존재하는 원본 포리스트.
    
      - Exchange 2013이 설치되어 있으며 사서함을 이동할 대상 포리스트.

  - Exchange 2013 대상 포리스트에 연결할 **UpdateRecipient** cmdlet을 호출 하 여 적절 한 사용 권한이 있어야 합니다. 필요한 사용 권한을 [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "받는 사람의 프로 비전 권한" 섹션을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## ILM 샘플 코드를 설치 하는 1 단계:

1.  Microsoft Visual Studio 2008, 코드 예제를 보려면 Microsoft.Exchange.Sample.OneWayGALSync.sln를 엽니다. 예제 코드는 다음과 같습니다.
    
      - Microsoft.MetadirectoryServicesEx.dll은 ILM 2007 FP1 s p 1에서와 함께 제공 되는 이진 파일 "Identity Integration Server\\Bin\\Assemblies \\Program Files\\Microsoft?. 샘플 코드에 의해 참조 됩니다.
    
      - OneWaySync.xml 샘플 코드에서 참조 됩니다.
    
      - ILMServerConfig 폴더에는 원본 관리 에이전트 (MA), 대상 MA, 및 ILM Metaverse (M)에 대 한 ILM 구성 파일이 들어 있습니다.
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll 및 Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (샘플 코드에서 작성 됨)는 "\\obj\\Debug 아래?

2.  ILM 서버에서 Identity Integration Server\\Extensions \\Program Files\\Microsoft에 다음 텍스트를 복사 합니다.
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  메일 사용자를 만들려는 대상 Exchange 포리스트에서 TargetOU 컨테이너의 고유 이름 (DN)을 지정 하는 1 단계에서 ILM 확장 폴더에 복사 하는 OneWaySync.xml 파일을 편집 합니다. LDP.exe 또는 ADSIEdit.exe 이름 이란 잘 모를 경우 TargetOU 컨테이너에 대 한 탐색을 사용할 수 있습니다.
    

    > [!NOTE]
    > 이 샘플 ILM GalSync 2007과 함께 사용 하는 경우 GalSync2007에서 관리 하는 컨테이너의 목록에서이 컨테이너를 제외 합니다.



4.  ILM Id 관리자 콘솔에서 **파일** 을 이동 \> ILMServerConfig 폴더에서 ILM 서버 구성을 가져오려면 **서버 구성을 가져옵니다**. 이 매크로 함수는 Metaverse 스키마 및 프로 비전 규칙 함께 두 Active Directory 관리 에이전트를 가져옵니다.
    

    > [!NOTE]
    > 가져오는 동안 포리스트 이름 및 자격 증명을 제공 하 고 원본 및 대상 ADMAs에 대 한 구성에는 가져온된 Active Directory 관리 에이전트 (ADMA) 파티션 이름을 파티션 일치 해야 합니다.



5.  **관리 에이전트 만들기** 페이지의 **확장 구성** 창에서 Exchange 2013 대상 포리스트를 지원 하기 위해 ADMA에 대 한 **Exchange 2013에 대 한 프로 비전** 드롭다운 목록에서 선택 하 고 **Exchange 2013 RPS URI** 에서 Exchange 2010 클라이언트 액세스 서버의 원격 Windows PowerShell URI를 입력 합니다.
    
    **관리 에이전트 페이지 만들기**
    
    ![관리 에이전트 Exchange 2010 프로비전](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "관리 에이전트 Exchange 2010 프로비전")  

6.  **관리 에이전트 만들기** 창에서 ILM Id 관리자 콘솔에서 원본 포리스트 관리 에이전트에 대 한 **속성** 을 엽니다. **디렉터리 파티션 구성** 마법사를 선택 하 고 대상 포리스트에 옮겨가는 사서함에 있는 컨테이너를 선택 하려면 **컨테이너** 클릭 합니다. 모든 다른 컨테이너, 즉, 범위만이 하나의 컨테이너를 관리 하려면 관리 에이전트에 대 한 선택 항목의 선택을 취소 합니다. 마찬가지로, 대상 포리스트 MA에 대 한 컨테이너를 선택 하는 메일 사용이 가능한 사용자가 프로 비전 할 즉, 2 단계에서 지정한는 TargetOU 합니다.
    

    > [!NOTE]
    > ILM GalSync 2007과 함께이 예제를 사용 하는 경우 GalSync 2007에서 관리 하는 컨테이너의 목록에서 모두 이러한 컨테이너를 제외 합니다.



7.  ILM 2 단계에서 지정한 TargetOU를 검색할 수 있도록 대상 Ma에서 초기 전체 가져오기 (단계에만 해당)를 수행 합니다.

## 2 단계: 대상 Exchange 포리스트에서에서 메일 사용자 만들기

예제 코드를 설치한 했으므로 다음 절차를 사용 하 여 온라인 사서함 이동을 수행 하려면 **New-MoveRequest** 를 실행할 수 있도록 대상 Exchange 포리스트에서 필요한 메일 사용자를 만들 수 있습니다.

1.  원본 포리스트에 Exchange 관리 센터를 사용 하 여 "설치 ILM 샘플 코드"의 4 단계에서 선택한 컨테이너에 사서함 사용자를 만들 수 있습니다. 컨테이너에 기존 사서함 사용자를 이동 하려면 Active Directory 사용자 및 컴퓨터를 사용할 수도 있습니다.

2.  델타 가져오기 및 소스를 원본 컨테이너 및 대상 MA에 프로 비전 메일 사용자를 추가 하는 사서함을 검색할 MA에서 실행 되는 델타 동기화를 수행 합니다.

3.  내보내기 대상 대상 Active Directory 을 1 단계에서 프로 비전 메일 사용자를 내보내려면 MA에서 실행을 수행 합니다.

4.  2 단계에서 내보낸 변경 내용을 확인 하는 MA 대상에 델타 가져오기를 수행 합니다.

5.  대상 포리스트에서 Exchange 관리 셸을 열고 **New-MoveRequest** cmdlet을 사용 하 여 원본 포리스트의 사서함을 이동 합니다.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - 대상 포리스트의 대상 포리스트에서 원본 포리스트의 이동 하는 사용자가 있는지를 확인 합니다.


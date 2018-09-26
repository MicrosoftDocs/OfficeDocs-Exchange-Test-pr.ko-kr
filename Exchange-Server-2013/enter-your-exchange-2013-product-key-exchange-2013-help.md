---
title: 'Exchange 2013 제품 키 입력: Exchange 2013 Help'
TOCTitle: Exchange 2013 제품 키 입력
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51407747
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: MT
---

# Exchange 2013 제품 키 입력

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

제품 키 Standard 또는 Enterprise Edition 라이선스를 구입한 Exchange Server 2013 에 지시 합니다. Enterprise Edition 라이선스에 대 한 제품 키를 구입한 경우 Standard Edition 라이센스와 함께 사용할 수 있는 모든 항목 외에도 서버당 5 개 이상의 데이터베이스를 탑재할 수 있습니다. 자세한 하려는 경우 Exchange 라이선스에 대 한 [Exchange 2013: 에디션 및 버전](exchange-2013-editions-and-versions-exchange-2013-help.md)를 참조 합니다.

제품 키를 입력 하지 않으면 하는 경우 서버에는 자동으로 사용이 허가 평가판 합니다. 평가판 함수 바로 Exchange Standard Edition 서버를 같은 표시 되며, 구입 하기 전에 Exchange 를 사용해 하거나 랩에서 테스트를 실행 하려는 경우에 유용 합니다. 유일한 차이점은만 최대 180 일 평가판으로 사용이 허가 Exchange 서버를 사용할 수 있습니다. 180 일 이상 서버를 사용 하 여 유지 하려는 경우 제품 키를 입력 해야 또는 Exchange 관리 센터 (EAC)를 만들어야 하는 서버 라이선스 제품 키를 입력 하는 미리 알림을 표시 하도록 시작 됩니다.


> [!TIP]
> 이 페이지의 일부 방문자가 Office의 설치 또는 정품 인증 방법을 찾고 있다는 사실을 알게 되었습니다. 이러한 사용자는 다음 페이지를 확인하세요. 
> <UL>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403360">Office 설치</A></P>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403361">Office 제품 키에 대한 도움이 필요하십니까?</A></P></LI></UL>Exchange 2010 서버에서 제품 키를 입력하려면 <A href="http://go.microsoft.com/fwlink/p/?linkid=403370">Exchange 2010 제품 키 입력</A>으로 이동합니다.<BR>Exchange 2013 서버에 제품 키를 입력하려는 경우 이 정보가 적절합니다. 다음을 읽어보세요.



## 시작하기 전에 알아야 할 내용

  - 이 절차의 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "제품 키" 항목

  - 사서함 서버 역할이 실행되는 Exchange 서버의 사용을 허가하는 경우 제품 키를 입력한 후에 서버에서 Microsoft Exchange Information Store Service를 다시 시작해야 합니다.

  - Standard Edition 라이선스에서 Enterprise Edition 라이선스로 Exchange 서버를 업그레이드하려면 이 항목의 단계를 따르세요.

  - Enterprise Edition 라이선스에서 Standard Edition 라이선스로 Exchange 서버를 다운그레이드하려면 Exchange를 다시 설치해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 제품 키 입력

1.  https://\<*클라이언트 액세스 서버 이름*\>/ecp로 이동하여 EAC를 엽니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  **서버** \> **서버**로 이동합니다. 사용을 허가할 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  (옵션) Standard Edition 라이선스에서 Enterprise Edition 라이선스로 서버를 업그레이드하려면 **일반** 페이지에서 **제품 키 변경**을 선택합니다. 서버 사용이 이미 허가된 경우 이 옵션만 표시됩니다.

5.  **일반** 페이지에서 **올바른 제품 키를 입력하십시오** 텍스트 상자에 제품 키를 입력합니다.

6.  **저장**을 클릭합니다.

7.  사서함 서버 역할이 실행되는 Exchange 서버의 사용을 허가한 경우 다음을 수행하여 Microsoft Exchange Information Store Service를 다시 시작하세요.
    
    1.  **제어판**을 열고 **관리 도구**로 이동한 다음 **서비스**를 엽니다.
    
    2.  **Microsoft Exchange Information Store**를 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 클릭합니다.

## 셸을 사용하여 제품 키 입력

이 예에서는 **set-ExchangeServer** cmdlet을 사용하여 제품 키를 입력합니다.


> [!NOTE]
> 같은 서버에서 이 명령을 다시 실행하여 해당 서버를 Standard Edition 라이선스에서 Enterprise Edition 라이선스로 업그레이드할 수 있습니다.

```powershell
Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ExchangeServer](https://technet.microsoft.com/ko-kr/library/bb123716\(v=exchg.150\))를 참조하세요.

사서함 서버 역할이 실행되는 Exchange 서버의 사용을 허가한 경우 다음을 수행하여 Microsoft Exchange Information Store Service를 다시 시작하세요.

1.  **제어판**을 열고 **관리 도구**로 이동한 다음 **서비스**를 엽니다.

2.  **Microsoft Exchange 정보 저장소** 를 마우스 오른쪽 단추로 클릭 하 고 **다시 시작** 을 클릭 합니다.

## 작동 여부는 어떻게 확인합니까?

EAC를 사용하여 서버가 Standard Edition 또는 Enterprise Edition으로 사용이 허가되었는지 확인하려면 다음을 수행합니다.

1.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

2.  **서버** \> **서버**로 이동합니다.

3.  확인할 서버를 선택하고 서버 세부 정보 창을 확인합니다. 제품 키가 수락되었으면 **사용 허가됨**이 Exchange 2013 Edition과 함께 표시됩니다.

셸을 사용하여 서버가 Standard Edition 또는 Enterprise Edition으로 사용이 허가되었는지 확인하려면 다음을 수행합니다.

1.  셸을 엽니다.

2.  다음 명령을 실행하여 특정 Exchange 서버의 라이선스 상태를 확인합니다.
        
    ```powershell
    Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*
    ```

3.  (옵션) 다음 명령을 실행하여 조직의 모든 Exchange 서버 라이선스 상태를 확인합니다.

    ```powershell    
    Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto
    ```
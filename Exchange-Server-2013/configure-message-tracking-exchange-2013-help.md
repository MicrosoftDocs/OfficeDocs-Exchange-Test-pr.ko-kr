---
title: '메시지 추적 구성: Exchange 2013 Help'
TOCTitle: 메시지 추적 구성
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51407695
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 추적 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-18_

메시지 추적은 Microsoft Exchange Server 2013 사서함 서버의 전송 서비스나 사서함에서 보내고 받은 모든 메시지의 SMTP 전송 활동을 기록합니다. 메시지 정보 분석, 메일 흐름 분석, 보고 및 문제 해결을 위해 메시지 추적 로그를 사용할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "Transport Service" 항목 또는 [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 서버 구성" 항목

  - EAC(Exchange 관리 센터)를 사용하여 메시지 추적을 사용하도록 설정하거나 사용하지 않도록 설정하고 메시지 추적 로그 경로를 설정할 수 있습니다. 그 이외의 모든 메시지 추적 옵션을 설정하려면 Exchange 관리 셸을 사용해야 합니다.

  - Exchange 2013 사서함 서버에서 **Set-TransportService**나 **Set-MailboxServer** cmdlet을 사용하여 메시지 추적 옵션을 구성할 수 있습니다. 이 항목의 절차에서는 **Set-TransportService** cmdlet이 사용됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 사서함 서버에 대해 메시지 추적 구성

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  구성하려는 사서함 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **전송 로그**를 클릭합니다.

4.  **메시지 추적 로그** 섹션에서 다음 항목을 변경합니다.
    
      - **메시지 추적 로그 사용**   서버에서 메시지 추적을 사용하지 않도록 설정하려면 이 확인란을 선택 취소합니다. 서버에서 메시지 추적을 사용하도록 설정하려면 이 확인란을 선택합니다.
    
      - **메시지 추적 로그 경로**   지정하는 값은 로컬 Exchange 서버에 있어야 합니다. 해당 폴더가 없는 경우 **저장**을 클릭하면 만들어집니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 메시지 추적 구성

메시지 추적을 구성하려면 다음 명령을 실행합니다.

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

이 예에서는 Mailbox01이라는 사서함 서버에 다음과 같은 메시지 추적 로그 설정을 구성합니다.

  -  메시지 추적 로그 파일의 위치를 D:\\Message Tracking Log로 설정합니다. 해당 폴더가 없는 경우 새로 만들어집니다.

  -  메시지 추적 로그 파일의 최대 크기를 20MB로 설정합니다.

  -  메시지 추적 로그 디렉터리의 최대 크기를 1.5GB로 설정합니다.

  -  메시지 추적 로그 파일의 최대 보존 기간을 45일로 설정합니다.

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P><EM>MessageTrackingLogPath</EM> 매개 변수를 <CODE>$null</CODE> 값으로 설정하면 메시지 추적을 사용할 수 없습니다. 이 경우 <EM>MessageTrackingLogEnabled</EM> 매개 변수의 값이 <CODE>$true</CODE>이면 이벤트 로그 오류가 생성됩니다.</P>
> <LI>
> <P><EM>MessageTrackingLogMaxAge</EM> 매개 변수를 <CODE>00:00:00</CODE>으로 설정하면 기간 만료로 인해 메시지 추적 로그 파일이 자동으로 제거되는 것이 방지됩니다.</P>
> <LI>
> <P>Exchange 2013 사서함 서버의 경우 메시지 추적 로그 디렉터리의 최대 크기는 <EM>MessageTrackingLogMaxDirectorySize</EM> 매개 변수 값의 세 배입니다. 서로 다른 네 가지 서비스에서 생성되는 메시지 추적 로그 파일의 이름 접두사는 모두 다르지만, <STRONG>MSGTRKMA</STRONG> 로그 파일에 기록되는 데이터의 양과 빈도는 나머지 3개 로그 파일 접두사에 비해 매우 적습니다. 자세한 내용은 <A href="message-tracking-exchange-2013-help.md">메시지 추적</A> 항목의 "메시지 추적 로그 파일의 구조" 섹션을 참조하십시오.</P></LI></UL>



이 예에서는 Mailbox01이라는 사서함 서버의 메시지 추적 로그에서 메시지 제목 기록을 사용하지 않도록 설정합니다.

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false
```

이 예에서는 Mailbox01이라는 사서함 서버에서 메시지 추적을 사용하지 않도록 설정합니다.

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false
```

## 작동 여부는 어떻게 확인합니까?

메시지 추적이 구성되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  표시된 값이 구성한 값인지 확인합니다.


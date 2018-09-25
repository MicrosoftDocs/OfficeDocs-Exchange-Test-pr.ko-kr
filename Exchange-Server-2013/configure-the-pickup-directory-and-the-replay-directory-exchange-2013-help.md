---
title: 'Pickup 디렉터리 및 Replay 디렉터리 구성: Exchange 2013 Help'
TOCTitle: Pickup 디렉터리 및 Replay 디렉터리 구성
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50484165
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pickup 디렉터리 및 Replay 디렉터리 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Pickup 및 Replay 디렉터리는 메시지 파일을 전송 파이프라인에 직접 삽입하기 위해 사서함 서버 및 Edge 전송 서버의 전송 서비스에서 사용됩니다. Pickup 또는 Replay 디렉터리에 복사된 올바른 형식의 전자 메일 메시지 파일이 배달을 위해 제출됩니다. Pickup 디렉터리는 관리자가 메일 흐름 테스트를 위해 사용하거나 자체 메시지를 만들어 전송해야 하는 응용 프로그램에 의해 사용됩니다. Replay 디렉터리는 SMTP가 아닌 외부 게이트웨이 서버에서 메시지를 수신하고 사용자가 Microsoft Exchange 서버 큐에서 내보낸 메시지를 재전송합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "전송 서비스" 항목을 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - **Set-TransportService** cmdlet의 *PickupDirectoryMaxMessagesPerMinute* 매개 변수 값은 Pickup 및 Replay 디렉터리에서 사용됩니다.

  - Pickup 또는 Replay 디렉터리의 위치를 변경하면 이전 위치의 기존 메시지 파일이 새 디렉터리로 복사되지 않습니다. 새 Pickup 또는 Replay 디렉터리는 구성 변경 후 거의 즉시 활성화되지만 모든 기존 메시지 파일은 이전 위치에 남아 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 수행할 작업

## 셸을 사용하여 Pickup 디렉터리 구성

Pickup 디렉터리를 구성하려면 다음 구문을 사용합니다.

```powershell
Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>
```

이 예에서는 Exchange01이라는 사서함 서버의 Pickup 디렉터리를 다음과 같이 변경합니다.

  - Pickup 디렉터리 위치는 D:\\Pickup 디렉터리로 설정됩니다.

  - 메시지 파일에서 메시지 헤더에 허용되는 최대 크기는 96KB로 늘어납니다.

  - 메시지 파일에 허용되는 최대 받는 사람 수는 250명으로 늘어납니다.

  - Pickup 및 Replay 디렉터리에 대한 최대 메시지 처리 속도가 분당 200개의 메시지로 증가합니다.

<!-- end list -->

```powershell
Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200
```


> [!NOTE]
> <UL>
> <LI>
> <P><EM>PickupDirectoryPath</EM> 매개 변수의 값을 <CODE>$null</CODE>로 설정하면 Pickup 디렉터리를 사용할 수 없습니다.</P>
> <LI>
> <P><EM>PickupDirectoryPath</EM> 매개 변수와 <EM>ReplayDirectoryPath</EM> 매개 변수로 지정되는 디렉터리는 동일할 수 없습니다.</P></LI></UL>



## 셸을 사용하여 Replay 디렉터리 구성

Replay 디렉터리를 구성하려면 다음 구문을 사용합니다.

```powershell
Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>
```

이 예에서는 Exchange01이라는 사서함 서버의 Replay 디렉터리를 다음과 같이 변경합니다.

  - Replay 디렉터리 위치는 D:\\Replay 디렉터리로 설정됩니다.

  - Pickup 및 Replay 디렉터리에 대한 최대 메시지 처리 속도가 분당 200개의 메시지로 증가합니다.

<!-- end list -->

```powershell
Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200
```


> [!NOTE]
> <UL>
> <LI>
> <P><EM>ReplayDirectoryPath</EM> 매개 변수의 값을 <CODE>$null</CODE>로 설정하면 Replay 디렉터리를 사용할 수 없습니다.</P>
> <LI>
> <P><EM>PickupDirectoryPath</EM> 매개 변수와 <EM>ReplayDirectoryPath</EM> 매개 변수로 지정되는 디렉터리는 동일할 수 없습니다.</P></LI></UL>



## 작동 여부는 어떻게 확인합니까?

Pickup 및 Replay 디렉터리가 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
    Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*
    ```

2.  표시된 값이 구성한 값인지 확인합니다.


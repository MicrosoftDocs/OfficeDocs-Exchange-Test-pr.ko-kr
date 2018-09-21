---
title: 'Edge 전송 서버에서 첨부 파일 필터링 관리: Exchange 2013 Help'
TOCTitle: Edge 전송 서버에서 첨부 파일 필터링 관리
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60829899
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버에서 첨부 파일 필터링 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

첨부 파일 필터링은 Edge 전송 서버에서만 사용 가능한 첨부 파일 필터 에이전트에서 제공됩니다. 첨부 파일 필터링을 수행하면 전자 메일 메시지에 첨부된 파일이 조직으로 유입되지 않도록 할 수 있습니다. 하나 이상의 첨부 파일 필터 항목을 구성하여 콘텐츠 형식이나 파일 이름으로 첨부 파일을 필터링할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목 및 [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "전송 에이전트" 항목

  - Edge 전송 서버의 첨부 파일 필터링에 대한 구성 변경 내용은 로컬 컴퓨터에만 적용됩니다. 경계 네트워크에 Edge 전송 서버가 여러 대 있는 경우에는 각 Edge 전송 서버에 대해 개별적으로 첨부 파일 필터링을 구성해야 합니다.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 첨부 파일 필터링을 사용하지 않도록 설정하고 Microsoft Exchange Transport Service를 다시 시작하면 모든 첨부 파일 필터링 기능의 작동이 중지됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 첨부 파일 필터링을 사용하거나 사용하지 않도록 설정

첨부 파일 필터링 에이전트를 사용하거나 사용하지 않도록 설정하면 Microsoft Exchange Transport Service를 다시 시작한 후에 변경 내용이 적용됩니다. Edge 전송 서버에서 Microsoft Exchange Transport Service를 다시 시작하면 서버의 메일 흐름이 일시적으로 중지됩니다.

첨부 파일 필터링을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Disable-TransportAgent "Attachment Filtering Agent"
```

첨부 파일 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Enable-TransportAgent "Attachment Filtering Agent"
```

첨부 파일 필터링을 사용하거나 사용하지 않도록 설정한 후 다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.

```powershell
Restart-Service MSExchangeTransport
```

## 작동 여부는 어떻게 확인합니까?

첨부 파일 필터링이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-TransportAgent "Attachment Filtering Agent"
```

2.  **Enabled**의 값이 `True`이면 첨부 파일 필터링이 사용하도록 설정된 것이고 값이 `False`이면 첨부 파일 필터링이 사용하지 않도록 설정된 것입니다.

## 셸을 사용하여 첨부 파일 필터링 항목 보기

첨부 파일 필터링 항목은 조직에 유입되지 않도록 할 메시지 첨부 파일을 정의합니다. 첨부 파일 필터링 에이전트에서 사용하는 첨부 파일 필터링 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-AttachmentFilterEntry | Format-Table
```

특정 MIME 콘텐츠 형식 항목을 보려면 다음 구문을 사용합니다.

```powershell
Get-AttachmentFilteringEntry ContentType:<MIMEContentType>
```

예를 들어 JPEG 이미지에 대한 콘텐츠 형식 항목을 보려면 다음 명령을 실행합니다.

```powershell
Get-AttachmentFilteringEntry ContentType:image/jpeg
```

특정 파일 이름 또는 파일 이름 확장명 항목을 보려면 다음 구문을 사용합니다.

```powershell
Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>
```

예를 들어 JPEG 첨부 파일의 파일 이름 확장명 항목을 보려면 다음 명령을 실행합니다.

    Get-AttachmentFilteringEntry FileName:*.jpg

## 셸을 사용하여 첨부 파일 필터링 항목 추가

MIME 콘텐츠 형식으로 첨부 파일을 필터링하는 첨부 파일 필터링 항목을 추가하려면 다음 구문을 사용합니다.

```powershell
Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType
```

다음 예에서는 JPEG 이미지를 필터링하는 MIME 콘텐츠 형식 항목을 추가합니다.

```powershell
Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType
```

파일 이름 또는 파일 이름 확장명으로 첨부 파일을 필터링하는 첨부 파일 필터링 항목을 추가하려면 다음 구문을 사용합니다.

```powershell
Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName
```

다음 예에서는 파일 이름 확장명이 .jpg인 첨부 파일을 필터링합니다.

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## 작동 여부는 어떻게 확인합니까?

첨부 파일 필터링 항목이 추가되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행하여 필터링 항목이 있는지 확인합니다.
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  금지된 첨부 파일이 포함된 테스트 메시지를 외부 사서함에서 내부 받는 사람에게 보낸 다음 해당 메시지가 거부, 제거 또는 삭제되는지 확인합니다.

## 셸을 사용하여 첨부 파일 필터링 항목 제거

MIME 콘텐츠 형식으로 첨부 파일을 필터링하는 첨부 파일 필터링 항목을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-AttachmentFilterEntry ContentType:<ContentType>
```

다음 예에서는 JPEG 이미지에 대한 MIME 콘텐츠 형식 항목을 제거합니다.

```powershell
Remove-AttachmentFilterEntry ContentType:image/jpeg
```

파일 이름 또는 파일 이름 확장명으로 첨부 파일을 필터링하는 첨부 파일 필터링 항목을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>
```

다음 예에서는 .jpg 파일 이름 확장명에 대한 파일 이름 항목을 제거합니다.

    Remove-AttachmentFilterEntry FileName:*.jpg

## 작동 여부는 어떻게 확인합니까?

첨부 파일 필터링 항목이 제거되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행하여 필터링 항목이 제거되었는지 확인합니다.
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  허용된 첨부 파일이 포함된 테스트 메시지를 외부 사서함에서 내부 받는 사람에게 보낸 다음 해당 메시지가 첨부 파일과 함께 정상적으로 배달되었는지 확인합니다.

## 셸을 사용하여 첨부 파일 필터링 작업 보기

금지된 첨부 파일이 메시지에서 검색될 때 사용되는 첨부 파일 필터링 작업을 보려면 다음 명령을 실행합니다.

```powershell
Get-AttachmentFilterListConfig
```

## 셸을 사용하여 첨부 파일 필터링 작업 구성

금지된 첨부 파일이 메시지에서 검색될 때 사용할 첨부 파일 필터링 작업을 구성하려면 다음 구문을 사용합니다.

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

이 예에서는 첨부 파일 필터링 구성을 다음과 같이 변경합니다.

  - 금지된 첨부 파일이 포함된 메시지 거부(차단)

  - 거부된 메시지에 대해 사용자 지정 응답 사용

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

자세한 내용은 [Set-AttachmentFilterListConfig](https://technet.microsoft.com/ko-kr/library/bb123483\(v=exchg.150\))를 참조하세요.

## 작동 여부는 어떻게 확인합니까?

첨부 파일 필터링 작업이 구성되었는지 확인하려면 금지된 첨부 파일이 포함된 테스트 메시지를 외부 사서함에서 내부 받는 사람에게 보낸 다음 해당 메시지와 첨부 파일이 올바르게 처리되는지 확인합니다.


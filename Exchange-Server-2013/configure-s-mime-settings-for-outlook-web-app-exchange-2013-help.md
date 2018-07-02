---
title: 'Outlook Web App에 대 한 S/MIME 설정 구성: Exchange 2013 Help'
TOCTitle: Outlook Web App에 대 한 S/MIME 설정 구성
ms:assetid: c7dee22c-9b5b-425c-91a9-d093204ff84e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn626160(v=EXCHG.150)
ms:contentKeyID: 61212687
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App에 대 한 S/MIME 설정 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Exchange 2013 및 Exchange Online의 조직 관리자는 S/MIME으로 보호되는 메시지 보내기와 받기를 허용하도록 Outlook Web App을 설정할 수 있습니다. `SMIMEConfig` cmdlet을 사용하여 Exchange 관리 셸 인터페이스를 통해 이 기능을 관리합니다.

`get-SMIMEConfig` 및 `set-SMIMEConfig`에 대한 예제 및 매개 변수 상세 설명 등의 자세한 내용은 [Get-SmimeConfig](https://technet.microsoft.com/ko-kr/library/dn554257\(v=exchg.150\)) 및 [Set-SmimeConfig](https://technet.microsoft.com/ko-kr/library/dn554259\(v=exchg.150\)) 설명서를 참조하세요.

이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

## 자세한 내용

[메시지 서명 및 암호화를 위한 S/MIME](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)


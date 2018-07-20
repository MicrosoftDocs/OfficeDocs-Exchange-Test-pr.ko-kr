---
title: 'S/MIME 유효성을 검사 하려면 가상 인증서 컬렉션 설정: Exchange 2013 Help'
TOCTitle: S/MIME 유효성을 검사 하려면 가상 인증서 컬렉션 설정
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212682
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# S/MIME 유효성을 검사 하려면 가상 인증서 컬렉션 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

테넌트 관리자는 S/MIME 인증서의 유효성을 검사하는 데 사용할 가상 인증서 컬렉션을 구성해야 합니다. 이 가상 인증서 컬렉션은 SST 파일 이름 확장명이 지정된 인증서 저장소 파일 형식으로 설정됩니다. SST 파일에는 S/MIME 인증서 유효성을 검사할 때 사용되는 모든 루트 및 중간 인증서가 포함됩니다.

## SST 만들기 및 저장

이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

관리자로 서 인증서를 내보내면 하 여이 SST 파일을 만들 수 있습니다 `Export-Certificate` cmdlet을 사용 하 고 SST으로 종류를 지정 하는 신뢰할 수 있는 컴퓨터에서 합니다. 자세한 내용은 `Export-Certificate` cmdlet에 대 한 [인증서 내보내기](https://technet.microsoft.com/en-us/library/hh848628.aspx) 참조 (영문) 항목을 참조 합니다.

SST 파일을 만든 후 `Set-Smimeconfig` cmdlet에서 *-SMIMECertificateIssuingCA* 매개 변수를 사용하여 가상 인증서 저장소에 해당 파일을 저장합니다. 예를 들면 다음과 같습니다. `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## 인증서가 유효한지 확인

Exchange 2013 SP1에서는 먼저 SST 파일을 확인한 다음 인증서 유효성을 검사합니다. 유효성 검사가 실패하면 로컬 컴퓨터 인증서 저장소를 확인하여 인증서 유효성을 검사합니다. 이 동작은 Exchange 2013 SP1에서 새롭게 제공되며 이전 버전의 Exchange와는 다릅니다. Exchange Online에서는 유효성 검사에 SST만 사용됩니다.

## 추가 정보

[메시지 서명 및 암호화를 위한 S/MIME](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/ko-kr/library/dn554257\(v=exchg.150\))


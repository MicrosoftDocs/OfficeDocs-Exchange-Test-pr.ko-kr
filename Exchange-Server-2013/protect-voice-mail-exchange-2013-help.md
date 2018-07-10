---
title: '음성 메일 보호: Exchange 2013 Help'
TOCTitle: 음성 메일 보호
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52057953
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 보호

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

일부 레거시 Private Branch eXchange (PBX) 및 IP PBX 전화 통신 시스템에는 호출자가 음성 메일 메시지를 표시 개인, 다른 사용자에 게 착신 전환에서 메시지의 받는 사람된을 차단 하도록 허용 합니다. 통합 된 음성 메일 시스템에서 음성 메시지를 사용 하면 의도 하지 않은 수신기에 노출 되지 않도록 비공개로 음성 메시지를 방지 하기 위해 시도 중 여러 방법으로 액세스할 수 있습니다.

조직에 대 한 음성 메시지를 보호 하기 위해 Active Directory 권한 관리 서비스 (AD RMS)를 사용 하 여 통합된 메시징 (UM)를 구성할 수 있습니다. 이 기능을 보호 된 음성 메일 이라고 합니다.

음성 메시지를 보호할 때 받는 사람이 메시지를 전달에서 차단 되지 않습니다 하지만 UM도 의도 한 받는 사람 또는 메시지의 받는 사람에 게는 해당 콘텐츠에 액세스할 수 있습니다. 보호 된 음성 메시지 MicrosoftOutlook 2010 를 사용 하 여 액세스 이상 수 Outlook Web App 또는 Outlook 음성 액세스 합니다.

**목차**

Overview of Protected Voice Mail

Active Directory의 개요 권한 관리 서비스

Client support and end-user features

Protected voice mail structure

Composing a Protected Voice Mail message

UM mailbox policies

Text message notifications and Protected Voice Mail

## 보호된 음성 메일 개요

보호 된 음성 메일 기능은 Exchange 2010 및 그 이후 버전의 UM (통합 메시징)을 사용할 수 있습니다. UM 사서함 정책에 대해 구성할 수 및 셸 Exchange 2010 에서 또는 Exchange 관리 콘솔을 사용 하 여 또는 셸 Exchange 2013 에서 Exchange 관리 센터 (EAC) 또는 cmdlet을 사용 하 여 모든 보호 된 음성 메일 설정을 구성할 수 있습니다.

보호된 음성 메일은 IRM(정보 권한 관리)을 음성 메시지에 적용하여 구현됩니다. 음성 메시지가 UM을 통해 보호될 경우 다음과 같은 기능이 적용됩니다.

  - 사용자가 보호된 음성 메시지에 회신할 수 있습니다.

  - 음성 메시지를 받는 사람이 음성 메시지를 전달할 수 없습니다.

  - 사용자가 음성 메시지의 복사본을 저장할 수 없습니다.

  - 사용자가 음성 메시지에 첨부된 오디오를 저장하거나 복사할 수 없습니다.

  - 음성 메시지는 받는 사람만이 열 수 있습니다.

전화 응답 음성 메시지와 개인 간 음성 메시지(Outlook Voice Access를 통해 사용자에게 전송된 음성 메시지) 모두 UM을 통해 보호할 수 있습니다. 그러나 다음 유형의 메시지에는 보호가 적용되지 않습니다.

  - 팩스 메시지

  - 비음성 메시지. 예를 들어, 전자 메일 메시지 또는 모임 요청이 비음성 메시지에 해당되며 이러한 메시지는 Outlook Voice Access(음성 회신)를 사용하여 생성한 경우에도 비음성 메시지로 분류됩니다.

맨 위로 이동

## Active Directory의 개요 권한 관리 서비스

AD RMS, Windows Server 2008 및 이상 버전의 구성 요소는 그렇게 보낸 파일 보기를 적용 하려는 사용자만 수행할 수 있도록 파일을 보호 하는데 사용할 수 있는. 사용자는 파일에 액세스할 수 있어야 하는 권한을 지정 하 여 파일을 보호 하는 AD RMS입니다. 권한을 열고, 수정, 인쇄, 전달, 사용자를 허용 하도록 구성할 수 있습니다 하거나 권한 관리 정보를 사용 하 여 다른 작업을 수행 합니다. AD RMS와 네트워크 외부에 배포 된 경우 데이터를 보호 수 있습니다.

AD RMS 시스템에는 서버와는 다음과 같은 클라이언트 구성 요소를 모두에 있습니다.

  - Windows Server 2008 R2 수 있는 서버 또는 인증서를 처리 하는 Active Directory 권한 관리 서비스 서버 역할을 실행 중 이며 라이선스는 설치 이후 버전입니다.

  - 데이터베이스 서버입니다.

  - AD RMS 클라이언트입니다. 최신 버전의 AD RMS 클라이언트의 부분에서는 Windows 7 및 Windows 8 운영 체제도 포함 됩니다.

예: Windows Server 2008 또는 이후 버전 Microsoft 서버에서 실행 되는 여러 웹 서비스의 서버 구성 요소 구성 됩니다. 클라이언트 구성 요소는 클라이언트 또는 서버 운영 체제에서 실행할 수 있습니다 하 고 암호화 하 고 콘텐츠를 해독 하 고, 서식 파일 및 해지 목록 검색 하 고 라이선스 및 서버에서 인증서를 취득 하기 위해 응용 프로그램을 사용할 수 있는 기능을 포함 합니다.

AD RMS 및 AD RMS 클라이언트를 사용 하 여 이동 되는 위치에 관계 없이 정보를 사용 하 여 남아 있는 영구 사용 정책을 통해 정보를 보호 함으로써 조직의 보안 전략을 추가할 수 있습니다. AD RMS를 사용 하 여 중요 한 정보를 안전 하 게 방지할 수 있습니다-재무 보고서, 제품 사양, 고객 데이터 및 기밀 전자 메일 및 음성 메일 메시지와 같은-에서 실수로 또는 의도적으로 잘못 된 자동으로 시작 합니다. 자세한 내용은 [AD RMS 개요](https://go.microsoft.com/fwlink/p/?linkid=199436)를 참조 하십시오.

Exchange UM에서 메시지와 첨부 파일에 일관 된 보호를 적용할 정보 권한 관리 (IRM) 기능을 사용할 수 있습니다.

IRM 기능 및 보호 된 음성 메일을 사용 하 여 조직 및 사용자에 게를 제어할 수 받는 사람에 게 전자 메일 및 음성 메일 메시지에 액세스할 수 있는 권한. IRM 다른 받는 사람에 게 메시지를 전달, 메시지 또는 첨부 파일, 인쇄 또는 복사 및 붙여넣기 하 여 메시지 또는 첨부 파일 콘텐츠를 추출 하는 등의 받는 사람 작업을 제한 하려면도 사용할 수 있습니다.

## IRM 요구 사항

Exchange에서 IRM을 구현할 수 전에 먼저 배포 및 AD RMS 인프라를 구성 해야 있습니다. 자세한 내용은 [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=199439)을 참조 하십시오. Exchange 조직에서 보호 된 음성 메일을 지원 하기 위해 IRM을 구현 하려면 배포에는 다음 요구 사항을 충족 해야 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 클러스터</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard 또는 Enterprise SP1 또는 Windows Server 2012 Standard 또는 Datacenter 합니다. 시스템 요구 사항에 대 한 자세한 내용은 <a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</a>을 참조 하십시오.</p></li>
<li><p><strong>서비스 연결 지점 (SCP)</strong> Exchange 2013 및 AD RMS 인식 응용 프로그램 Active Directory 에 등록 된 SCP를 사용 하 여 AD RMS 클러스터 및 Url을 검색 하도록 합니다. AD RMS를 사용 하면 AD RMS 설치 내에서 SCP를 등록할 수 있습니다. AD RMS를 설정 하려면 사용 하는 계정은 Enterprise Admins 보안 그룹의 구성원이 아니면 설치 후 SCP 등록을 수행할 수 있습니다. Active Directory 포리스트의 AD RMS에 대 한 SCP를 하나만 있습니다.   </p></li>
<li><p><strong>사용 권한</strong>   Exchange servers 그룹에 있는 서버 또는 개별 Exchange 서버에 할당 되어야 합니다 읽기 및 실행 권한을 AD RMS 서버 인증 파이프라인입니다. 기본 경로 AD RMS 서버의 \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx 합니다.</p></li>
<li><p><strong>AD RMS 고급 사용자</strong>   Exchange 검색에 대 한 전송 암호 해독, 저널 보고서 암호 해독, Outlook Web App IRM 및 IRM을 사용 하도록 페더레이션 배달 사서함, AD RMS 클러스터에 AD RMS 고급 사용자 그룹에 Exchange 설치 프로그램에서 만든 시스템 사서함을 추가 해야 합니다. 자세한 내용은 <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.</a>을 참조 하십시오.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## IRM 구성 및 테스트

셸을 사용 하 여 IRM 기능을 구성 해야 합니다. 개별 IRM 기능을 구성 하려면 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) cmdlet을 사용 합니다. IRM 기능을 구성 하는 방법에 대 한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)을 참조 하십시오.

Exchange 서버를 설정한 후에 IRM 배포의 끝-테스트를 수행 하려면 [Test-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979798\(v=exchg.150\)) cmdlet을 사용할 수 있습니다. 이 cmdlet는 조직에 대 한 IRM 구성을 확인 하 고 보호 된 음성 메일을 사용 하도록 설정 하기 전에 실행 해야 합니다. **Test-IRMConfiguration** cmdlet은 다음 테스트를 수행합니다.

  - Exchange 조직에 대 한 IRM 구성을 검사합니다.

  - 버전 및 핫픽스 정보에 대 한 AD RMS 서버를 확인합니다.

  - 권한 계정 인증서와 클라이언트 사용 허가자 인증서 (CLC)를 검색 하 여 RMS에 대 한 Exchange 서버를 활성화할 수 있는지 여부를 확인 합니다.

  - AD RMS 서버에서 AD RMS 권한 정책 템플릿을 가져옵니다.

  - 지정된 보낸 사람이 IRM으로 보호된 메시지를 보낼 수 있는지 확인합니다.

  - 지정된 받는 사람에 대한 슈퍼 사용자 사용권을 검색합니다.

  - 지정 된 받는 사람에 대해 이전 라이선스를 가져옵니다.

맨 위로 이동

## 클라이언트 지원 및 최종 사용자 기능

보호 된 음성 메일 메시지를 들을 수 하는데 사용 되는 전자 메일 클라이언트 소프트웨어는 IRM을 지원 하 고 UM 암호로 보호 된 음성 메시지를 읽으려면 하는 방법을 알고 해야 합니다. 지원 되는 전자 메일 클라이언트 MicrosoftOutlook 2010 또는 이상 버전, Outlook Web App 및 Outlook 음성 액세스를 포함 합니다. 다음 표에 전자 메일 클라이언트와 지원 되는 여부의 목록을 포함 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>전자 메일 클라이언트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>보호된 음성 메시지는 Outlook 2010 이상 버전에서 지원됩니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App Exchange 2010 또는 이후 버전의 보호 된 음성 메일 메시지를 지원합니다. Outlook Web App, Outlook Web Access 라고의 이전 버전을 지원 하지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Outlook 음성 액세스 Exchange 2010 및 그 이후 버전의 보호 된 음성 메일을 지원합니다. Outlook 음성 액세스 Exchange 2007 에 포함 된 음성 메일 보호를 지원 하지 않습니다.</p></li>
<li><p>사용자의 사서함 Exchange 2010 또는 이후 버전에서 사서함 서버에 있어야 합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 또는 Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile은 보호된 음성 메일을 지원하지 않습니다. 그러나 Windows Phone 7 및 Windows Phone 8에서는 보호된 음성 메일을 지원합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>보호 된 음성 메일 Exchange 2010 s p 1과 이상 버전에서 지원 됩니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>다른 전자 메일 클라이언트</p></td>
<td><ul>
<li><p>보호된 음성 메일이 지원되지 않습니다.</p></li>
</ul></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 보호된 음성 메시지 구조

각각의 보호된 음성 메일 메시지에는 실제로 메시지 두 개가 관련됩니다. 첫 번째 메시지는 암호화되지 않은 외부 메시지입니다. 이 메시지에는 이름이 message.rpmsg인 첨부 파일이 포함됩니다. 첨부 파일에는 IRM으로 보호된 음성 메시지와 내부 권한 관리 제어 데이터가 포함됩니다. 권한 관리 제어 데이터에는 콘텐츠 키와 음성 메시지에 액세스할 수 있는 사람 및 액세스 방법을 지정하는 권한 정보가 포함됩니다.

보호된 음성 메시지는 **음성 메일** 검색 폴더에 있는 사용자의 받은 편지함에 표시됩니다. 사용자는 일반 음성 메시지를 들을 때와 마찬가지로 포함된 오디오 플레이어를 이용해 음성 메시지를 들을 수 있습니다. 다른 점이 있다면 전달 단추가 사용하지 않도록 설정되고 메시지 맨 위에 보호된 메시지이므로 전달할 수 없음을 알리는 메모가 표시됩니다.

보호된 음성 메일을 지원하지 않는 전자 메일 클라이언트의 경우 외부 메시지의 본문이 표시됩니다. 관리자는 UM 사서함 정책을 사용하여 클라이언트 소프트웨어가 보호된 음성 메일을 지원하지 않을 때 텍스트를 포함할 수 있습니다. UM 사서함 정책을 구성하여 전자 메일 메시지에 포함되는 기본 텍스트를 사용자 지정할 수 있습니다. 예를 들어, *"이 음성 메일 메시지는 보호되어 있으므로 열 수 없습니다. 이 음성 메시지를 보거나 들으려면 https://mail.contoso.com에서 사서함에 로그인하거나 +1 (425) 555-1234번으로 Outlook Voice Access에 전화하십시오." 등의 사용자 지정 텍스트를 사용하여 UM 사서함 정책을 구성할 수 있습니다.*

맨 위로 이동

## 보호된 음성 메일 메시지 작성

다음과 같은 두 가지 경우에 보호된 음성 메시지를 만들 수 있습니다.

  - **전화 응답**   전화 응답은 발신자가 UM 사용 가능 사용자에게 전화를 걸었는데 해당 사용자가 전화를 받을 수 없거나 음성 메일로 전화를 직접 전달하는 경우 수행됩니다. 전화 응답 시나리오에서는 발신자가 음성 메시지를 녹음하고 나면 음성 메일 시스템에서 일련의 음성 안내를 재생합니다.
    
    그러면 발신자가 우물정자(\#)를 눌러 음성 메시지를 비공개로 표시하는 옵션을 포함한 추가 메시지 옵션 중에서 선택할 수 있습니다. 발신자는 \# 키를 누르고 UM에서 제공하는 지침에 따라 메시지를 비공개로 표시하거나, 비공개 음성 메시지에서 비공개 표시를 제거하거나, 음성 메시지를 중요도 높음으로 표시할 수 있습니다. 다음 다이어그램은 발신자가 사용자를 위해 비공개 음성 메시지를 남길 경우 사용할 수 있는 메뉴 옵션을 보여줍니다.
    

    > [!NOTE]
    > 전화 응답 통화의 경우 발신자가 인증되지 않으므로 UM은 메시지를 받는 사람의 UM 사서함 정책에 대한 보호된 음성 메일 설정을 사용합니다.

    
    **전화 응답을 사용하여 보호된 음성 메일 메시지 만들기**
    
    ![전화 응답을 사용하여 보호된 음성 사서함 만들기](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "전화 응답을 사용하여 보호된 음성 사서함 만들기")  

  - **Outlook Voice Access**   Outlook Voice Access를 사용하면 UM 사용 가능 사용자가 아날로그/디지털 전화 또는 휴대폰을 이용해 Outlook Voice Access 번호로 전화를 걸어 사서함에 액세스할 수 있습니다. UM 사용 가능 사용자가 사용할 수 있는 통합 메시징 사용자 인터페이스는 TUI(전화 사용자 인터페이스)와 VUI(음성 사용자 인터페이스)의 두 가지가 있습니다.
    
    Outlook Voice Access 사용자는 디렉터리에서 연락처를 검색하여 해당 연락처로 음성 메시지를 전송할 수 있습니다. UM 사용 가능 받는 사람이 보호된 음성 메일을 사용하도록 설정된 경우 발신자가 메시지를 녹음한 후 비공개로 표시할 수 있습니다. 또는 관리자가 인증된 사용자가 보낸 모든 음성 메시지가 UM에 의해 보호되도록 UM 사서함 정책을 구성할 수 있습니다.
    

    > [!NOTE]
    > 발신자가 인증된 경우 음성 메시지 받는 사람에 대한 UM 사서함 정책 설정에 관계없이 발신자와 연결된 UM 사서함 정책의 보호된 음성 메일 설정이 적용됩니다.

    
    **음성 사용자 인터페이스를 사용하여 보호된 음성 메일 메시지 만들기**
    
    ![음성 인터페이스를 사용하여 보호된 음성 사서함 만들기](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "음성 인터페이스를 사용하여 보호된 음성 사서함 만들기")  
    
    **전화 사용자 인터페이스를 사용하여 보호된 음성 메일 메시지 만들기**
    
    ![터치톤 입력을 사용하여 보호된 음성 사서함 만들기](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "터치톤 입력을 사용하여 보호된 음성 사서함 만들기")  

맨 위로 이동

## UM 사서함 정책

UM 사용이 가능한 사서함의 컬렉션에 PIN 정책 설정, 전화를 걸 제한과 보호 된 음성 메일 설정 등의 UM 정책 설정 집합이 적용 하는 통합 메시징 사서함 정책을 만들 수 있습니다. UM 사서함 정책에 대 한 자세한 내용은, [UM 사서함 정책 관리](manage-a-um-mailbox-policy-exchange-2013-help.md)를 참조 하십시오.

EAC를 사용하거나 셸의 **Set-UMMailboxPolicy** cmdlet을 사용하여 보호된 음성 메일 옵션을 구성할 수 있습니다. 다음 표는 보호된 음성 메일에 대해 구성할 수 있는 설정을 보여줍니다.

**보호된 음성 메일 설정**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>셸 매개 변수</th>
<th>EAC에서 설정 사용 가능 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>예</p></td>
<td><p><em>ProtectAuthenticatedVoiceMail</em> 매개 변수는 UM 사용 가능 사용자가 Outlook Voice Access를 사용하여 사서함에 액세스할 때 보호된 음성 메시지를 전송할 수 있는지 여부를 지정합니다. 기본 설정은 <code>None</code>입니다. 즉, 음성 메시지가 작성될 때 보호가 적용되지 않으며 발신자에게 음성 메시지를 비공개로 표시할 수 있는 옵션이 제공되지 않습니다. 값이 <code>Private</code>로 설정되면 발신자가 비공개로 표시한 메시지만 보호됩니다. 값이 <code>All</code>로 설정되면 발신자가 선택한 옵션에 관계없이 모든 음성 메시지가 보호됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>예</p></td>
<td><p><em>ProtectUnauthenticatedVoiceMail</em> 매개 변수는 UM 사서함 정책에 연결된 UM 사용 가능 사용자에 대해 전화를 받는 사서함 서버에서 보호된 음성 메시지를 만드는지 여부를 지정합니다. 이 설정은 메시지가 UM 자동 전화 교환에서 UM 사용 가능 사용자에게로 전송된 경우에도 적용됩니다. 기본 설정은 <code>None</code>입니다. 즉, 음성 메시지에 보호가 적용되지 않으며 발신자에게 메시지를 비공개로 표시할 수 있는 옵션이 제공되지 않습니다. 값이 <code>Private</code>로 설정되면 발신자가 비공개로 표시한 메시지만 보호됩니다. 값이 <code>All</code>로 설정되면 발신자가 메시지를 비공개로 설정했는지 여부에 관계없이 모든 음성 메시지가 보호됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>예</p></td>
<td><p><em>ProtectedVoiceMailText</em> 매개 변수는 보호된 음성 메일 메시지의 외부 메시지 본문에 포함할 텍스트를 지정합니다. 이 텍스트는 보호된 음성 메일 메시지를 지원하지 않는 모든 전자 메일 클라이언트 응용 프로그램에 표시됩니다. 기본 메시지는 이 속성이 <code>Null</code>로 설정되어 있거나 비어 있는 경우 항상 UM에서 제공합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>예</p></td>
<td><p><em>RequireProtectedPlayOnPhone</em> 매개 변수는 UM 사서함 정책과 연결된 사용자가 전화를 통해(전화에서 재생 사용) 보호된 음성 메시지를 청취해야 하는지 여부를 지정합니다. 기본값은 <code>$false.</code>입니다. 값을 <code>$true</code>로 설정하면 Outlook 또는 Outlook Web App의 보호된 음성 메일 양식의 오디오 미디어 플레이어가 비활성화된 상태로 표시됩니다. 음성 메시지의 미리 보기 텍스트는 항상 액세스할 수 있습니다. 사용자가 미디어 플레이어 소프트웨어를 사용하여 오디오 파일을 재생하거나 포함된 미디어 플레이어를 사용하여 음성 메시지를 들을 수는 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>예</p></td>
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em> 매개 변수는 Outlook Voice Access에서 전자 메일에 액세스할 수 있도록 인증된 발신자가 전자 메일과 모임 요청에 대한 음성 회신을 작성할 수 있는지 여부를 지정합니다.</p></td>
</tr>
</tbody>
</table>


보호된 음성 메일 설정을 관리하는 방법에 대한 자세한 내용은 [보호 된 음성 메일 절차](protected-voice-mail-procedures-exchange-2013-help.md) 또는 [Set-UMMailboxPolicy](https://technet.microsoft.com/ko-kr/library/bb124903\(v=exchg.150\))를 참조하십시오.

맨 위로 이동

## 문자 메시지 알림 및 보호된 음성 메일

음성 메시지가 수신될 경우 휴대폰으로 문자 메시지 알림(SMS 알림이라고도 함)이 전송되도록 UM 계정을 구성하는 사용자는 문자 메시지 본문의 일부로 오디오 기록(음성 메일 미리 보기) 텍스트도 수신하게 됩니다. 그러나 보호된 음성 메시지의 경우 음성 메시지의 콘텐츠가 항상 보호되어야 하므로 보안 문제가 발생할 수 있습니다.

따라서 UM이 보호된 음성 메시지에 대한 문자 메시지 알림을 만들 때 음성 메시지가 비공개로 표시되어 있는지를 확인합니다. 비공개로 표시된 경우 휴대폰으로 전송할 문자 메시지에 문자화된 오디오 텍스트를 추가하지 않습니다. 그 대신 다음 텍스트가 문자 메시지에 포함됩니다. "이 보호된 음성 메일 메시지에 액세스하려면 Outlook Voice Access를 사용하십시오."

맨 위로 이동


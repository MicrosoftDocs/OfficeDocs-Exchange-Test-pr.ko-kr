---
title: '메일 흐름 및 클라이언트 액세스 구성: Exchange 2013 Help'
TOCTitle: 메일 흐름 및 클라이언트 액세스 구성
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50483048
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 메일 흐름 및 클라이언트 액세스 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

SSL 인증서 구성 방법을 포함하여 Exchange Server 2013 메일 흐름 및 클라이언트 액세스에 대한 설치 후 작업.

조직에 Exchange Server 2013을 설치한 후에는 메일 흐름 및 클라이언트 액세스를 위해 Exchange Server 2013을 구성해야 합니다. 이러한 추가 단계가 없으면 인터넷으로 메일을 보낼 수 없으며 Microsoft Office Outlook 및 Exchange ActiveSync 장치와 같은 외부 클라이언트에서 Exchange 조직에 연결할 수 없습니다.

이 항목의 단계에서는 단일 Active Directory 사이트와 단일 SMTP(Simple Mail Transport Protocol) 네임스페이스를 포함하는 기본 Exchange 배포를 가정합니다.


> [!IMPORTANT]
> 이 항목에서는 Ex2013CAS, contoso.com, mail.contoso.com 및 172.16.10.11과 같은 값을 예로 사용합니다. 이러한 값을 조직에서 실제 사용하는 서버 이름, FQDN 및 IP 주소로 바꿉니다.



메일 흐름, 클라이언트 및 장치와 관련된 추가 관리 작업은 [메일 흐름](mail-flow-exchange-2013-help.md) 및 [클라이언트 및 모바일](clients-and-mobile-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 50분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 클라이언트 액세스 서버에 SSL(Secure Sockets Layer) 인증서를 구성하기 전까지는 EAC(Exchange 관리 센터)에 연결하면 인증서 경고가 나타납니다. 이 작업을 수행하는 방법은 이 항목 뒷부분에 나와 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!IMPORTANT]
> 각 조직에 대해 적어도 클라이언트 액세스 서버 한 개와 사서함 서버 한 개가 Active Directory 포리스트에 있어야 합니다. 또한 사서함 서버가 포함된 각 Active Directory 사이트에 클라이언트 액세스 서버도 하나 이상 포함되어야 합니다. 서버 역할을 구분하려면 먼저 사서함 서버 역할을 설치하는 것이 좋습니다.




> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 송신 커넥터 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "송신 커넥터" 항목

인터넷으로 메일을 보내려면 먼저 사서함 서버에 송신 커넥터를 만들어야 합니다. 다음을 수행하세요.

1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니/다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  **메일 흐름** \> **송신 커넥터**로 이동합니다. **송신 커넥터** 페이지에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **새 송신 커넥터** 마법사에서 송신 커넥터 이름을 지정하고 **인터넷**을 선택합니다. **다음**을 클릭합니다.

5.  **받는 사람 도메인에 연결된 MX 레코드**가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

6.  **주소 공간** 아래에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다. **도메인 추가** 창에서 **유형** 필드에 **SMTP**가 선택되어 있는지 확인합니다. **FQDN(정규화된 도메인 이름)** 필드에 \*를 입력합니다. **저장**을 클릭합니다.

7.  **범위가 지정된 송신 커넥터**가 선택되어 있지 않은지 확인하고 **다음**을 클릭합니다.

8.  **원본 서버**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. **서버 선택** 창에서 사서함 서버를 선택합니다. 서버를 선택한 다음 **추가**를 클릭하고 **확인**을 클릭합니다.

9.  **마침**을 클릭합니다.


> [!NOTE]
> Exchange 2013을 설치하면 기본 인바운드 수신 커넥터가 만들어집니다. 이 수신 커넥터는 외부 서버로부터의 익명 SMTP 연결을 수락합니다. 이렇게 작동하도록 하려는 경우 추가 구성 작업을 수행할 필요가 없습니다. 외부 서버로부터의 인바운드 연결을 제한하려는 경우에는 클라이언트 액세스 서버의 <STRONG>기본 프런트 엔드 &lt;클라이언트 액세스 서버&gt;</STRONG> 수신 커넥터를 수정합니다.



## 이 단계의 작동 여부는 어떻게 확인합니까?

아웃바운드 송신 커넥터가 만들어졌는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **메일 흐름** \> **송신 커넥터**에 새 송신 커넥터가 나타나는지 확인합니다.

2.  Outlook Web App을 열고 외부의 받는 사람에게 전자 메일 메시지를 보냅니다. 받는 사람이 메시지를 받으면 송신 커넥터가 구성된 것입니다.

## 2단계: 허용 도메인 추가

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "허용 도메인" 항목

기본적으로 Active Directory 포리스트에 새 Exchange 2013 조직을 배포하면 Exchange에서는 Setup /PrepareAD가 실행된 Active Directory 도메인의 도메인 이름을 사용합니다. 받는 사람이 다른 도메인과 메시지를 주고받게 하려면 해당 도메인을 허용 도메인으로 추가해야 합니다. 또한 이 도메인은 다음 단계에서 기본 전자 메일 주소 정책에 기본 SMTP 주소로 추가됩니다.


> [!IMPORTANT]
> 인터넷에서 보내는 전자 메일을 수락할 각 SMTP 도메인에는 공용 DNS(Domain Name System) MX 리소스 레코드가 필요합니다. 그리고 각 MX 레코드는 조직의 전자 메일을 받는 인터넷 연결 서버로 확인되어야 합니다.



1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  **메일 흐름** \> **허용 도메인**으로 이동합니다. **허용 도메인** 페이지에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **새 허용 도메인** 마법사에서 허용 도메인의 이름을 지정합니다.

5.  **허용 도메인** 필드에서 추가할 SMTP 받는 사람 도메인(예: contoso.com)을 지정합니다.

6.  **신뢰할 수 있는 도메인**을 선택하고 **저장**을 클릭합니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

허용 도메인이 만들어졌는지 확인하려면 다음을 수행합니다.

  - EAC에서 **메일 흐름** \> **허용 도메인**에 새 허용 도메인이 나타나는지 확인합니다.

## 3단계: 기본 전자 메일 주소 정책 구성

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "전자 메일 주소 정책" 항목

이전 단계에서 허용 도메인을 추가했으며 해당 도메인을 조직의 모든 받는 사람에게 추가하려는 경우 기본 전자 메일 주소 정책을 업데이트해야 합니다.

1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  **메일 흐름** \> **전자 메일 주소 정책**으로 이동합니다. **전자 메일 주소 정책** 페이지에서 **기본 정책**을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **기본 정책 전자 메일 주소 정책** 페이지에서 **전자 메일 주소 형식**을 클릭합니다.

5.  **전자 메일 주소 형식**에서 변경할 SMTP 주소를 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

6.  **전자 메일 주소 형식** 페이지의 **전자 메일 주소 매개 변수** 필드에서 Exchange 조직의 모든 받는 사람에게 적용할 SMTP 받는 사람 도메인을 지정합니다. 이 도메인은 이전 단계에서 추가한 허용 도메인과 일치해야 합니다. 예를 들어 @contoso.com과 같이 입력합니다. **저장**을 클릭합니다.

7.  **저장**을 클릭합니다.

8.  **기본 정책** 세부 정보 창에서 **적용**을 클릭합니다.


> [!NOTE]
> 각 사용자의 기본 전자 메일 주소와 일치하는 UPN(사용자 계정 이름)을 구성하는 것이 좋습니다. 사용자의 전자 메일 주소와 일치하는 UPN을 지정하지 않을 경우 사용자가 직접 전자 메일 주소와 함께 도메인\사용자 이름 또는 UPN을 지정해야 합니다. 사용자의 UPN이 전자 메일 주소와 일치하면 Outlook Web App, ActiveSync 및 Outlook에서는 자동으로 사용자의 전자 메일 주소를 해당 UPN과 일치시킵니다.



## 이 단계의 작동 여부는 어떻게 확인합니까?

기본 전자 메일 주소 정책이 구성되었는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함을 선택하고 받는 사람 세부 정보 창에서 **사용자 사서함** 필드가 *\<alias\>*@<em>\<new accepted domain\</em>으로 설정되어 있는지 확인합니다. 예를 들어 david@contoso.com과 같은지 확인합니다.

3.  필요한 경우 다음을 수행하여 새 사서함을 만들고 해당 사서함에 새 허용 도메인이 포함된 전자 메일 주소가 지정되었는지 확인합니다.
    
    1.  **받는 사람** \> **사서함**으로 이동하여 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭한 다음 **사용자 사서함**을 선택합니다.
    
    2.  새 사용자 사서함 페이지에서 새 사서함을 만드는 데 필요한 정보를 제공합니다. **저장**을 클릭합니다.
    
    3.  새 사서함을 선택하고 받는 사람 세부 정보 창에서 **사용자 사서함** 필드가 *\<alias\>*@<em>\<new accepted domain\></em>으로 설정되어 있는지 확인합니다. 예를 들어 david@contoso.com과 같은지 확인합니다

## 4단계: 외부 URL 구성

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "*\<Service\>* 가상 디렉터리 설정" 항목

클라이언트가 인터넷에서 새 서버에 연결할 수 있으려면 클라이언트 액세스 서버의 가상 디렉터리에 외부 도메인 또는 URL을 구성한 다음 공용 DNS(도메인 이름 서비스) 레코드를 구성해야 합니다. 아래 단계에서는 각 가상 디렉터리의 외부 URL에 동일한 외부 도메인을 구성합니다. 하나 이상의 가상 디렉터리 외부 URL에 서로 다른 외부 도메인을 구성하려면 외부 URL을 직접 구성해야 합니다. 자세한 내용은 [가상 디렉터리 관리](virtual-directory-management-exchange-2013-help.md)를 참조하세요.

1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  **서버** \> **서버**로 이동하여 인터넷 연결 클라이언트 액세스 서버의 이름을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **외부에서 Outlook 사용**을 클릭합니다.

5.  **외부 호스트 이름 지정** 필드에 클라이언트 액세스 서버에 대한 외부에서 액세스 가능한 FQDN을 지정합니다(예: mail.contoso.com).

6.  이 단계에서 클라이언트 액세스 서버에 대한 내부에서 액세스 가능한 FQDN도 설정합니다. **내부 호스트 이름 지정** 필드에 이전 단계에서 사용한 FQDN을 삽입합니다(예: mail.contoso.com).

7.  **저장**을 클릭합니다.

8.  **서버** \> **가상 디렉터리**로 이동한 다음 **외부 액세스 도메인 구성**![구성 아이콘](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "구성 아이콘")을 클릭합니다.

9.  **외부 URL에 사용할 클라이언트 액세스 서버 선택**에서 **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

10. 구성할 클라이언트 액세스 서버를 선택하고 **추가**를 클릭합니다. 구성할 클라이언트 액세스 서버를 모두 추가한 후 **확인**을 클릭합니다.

11. **외부 클라이언트 액세스 서버에 사용할 도메인 이름 입력**에 적용할 외부 도메인을 입력합니다(예: mail.contoso.com). **저장**을 클릭합니다.
    

    > [!NOTE]
    > 일부 조직에서는 기본 서버 FQDN 변경으로부터 사용자를 보호하기 위해 Outlook Web App FQDN을 고유하게 설정합니다. 많은 조직에서 Outlook Web App FQDN에 mail.contoso.com 대신에 owa.contoso.com을 사용합니다. 고유한 Outlook Web App FQDN을 구성하려면 이전 단계를 완료한 후 다음을 수행합니다. 이 검사 목록에서는 고유한 Outlook Web App FQDN을 구성했다고 가정합니다. 
    > <OL>
    > <LI>
    > <P><STRONG>owa(기본 웹 사이트)</STRONG>를 선택하고 <STRONG>편집</STRONG>&nbsp;<IMG title="편집 아이콘" alt="편집 아이콘" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">을 클릭합니다.</P>
    > <LI>
    > <P><STRONG>외부 URL</STRONG>에 <STRONG>https://</STRONG>를 입력하고 사용할 고유한 Outlook Web App FQDN을 입력한 다음 <STRONG>/owa</STRONG>를 추가합니다(예: https://owa.contoso.com/owa).</P>
    > <LI>
    > <P><STRONG>저장</STRONG>을 클릭합니다.</P>
    > <LI>
    > <P><STRONG>ecp(기본 웹 사이트)</STRONG>를 선택하고 <STRONG>편집</STRONG>&nbsp;<IMG title="편집 아이콘" alt="편집 아이콘" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">을 클릭합니다.</P>
    > <LI>
    > <P><STRONG>외부 URL</STRONG>에 <STRONG>https://</STRONG>를 입력하고 이전 단계에서 지정한 것과 동일한 Outlook Web App FQDN을 입력한 다음 <STRONG>/ecp</STRONG>를 추가합니다(예: https://owa.contoso.com/ecp).</P>
    > <LI>
    > <P><STRONG>저장</STRONG>을 클릭합니다.</P></LI></OL>



클라이언트 액세스 서버 가상 디렉터리에서 외부 URL을 구성한 후에는 자동 검색, Outlook Web App 및 메일 흐름에 대해 공용 DNS 레코드를 구성해야 합니다. 공용 DNS 레코드는 인터넷 연결 클라이언트 액세스 서버의 외부 IP 주소 또는 FQDN을 가리켜야 하고, 클라이언트 액세스 서버에서 구성한 외부에서 액세스할 수 있는 FQDN을 사용해야 합니다. 아래에는 메일 흐름과 외부 클라이언트 연결을 사용하려면 만들어야 하는 권장 DNS 레코드의 예가 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 레코드 형식</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## 이 단계의 작동 여부는 어떻게 확인합니까?

클라이언트 액세스 서버 가상 디렉터리에 외부 URL이 구성되었는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **가상 디렉터리**로 이동합니다.

2.  **서버 선택** 필드에서 인터넷 연결 클라이언트 액세스 서버를 선택합니다.

3.  가상 디렉터리를 선택한 다음 가상 디렉터리 세부 정보 창에서 **외부 URL** 필드가 아래와 같은 올바른 FQDN 및 서비스로 채워져 있는지 확인합니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>가상 디렉터리</th>
    <th>외부 URL 값</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>자동 검색</strong></p></td>
    <td><p>외부 URL이 표시되지 않음</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


공용 DNS 레코드가 구성되었는지 확인하려면 다음을 수행합니다.

1.  명령 프롬프트를 열고 `nslookup.exe`를 실행합니다.

2.  공용 DNS 영역을 쿼리할 수 있는 DNS 서버로 변경합니다.

3.  `nslookup`에서 사용자가 만든 각각의 FQDN 레코드를 조회합니다. 각 FQDN에 대해 반환되는 값이 올바른지 확인합니다.

4.  `nslookup`에서 `set type=mx`를 입력한 다음 1단계에서 추가한 허용 도메인을 찾습니다. 반환된 값이 클라이언트 액세스 서버의 FQDN과 일치하는지 확인합니다.

## 5단계: 내부 URL 구성

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "*\<Service\>* 가상 디렉터리 설정" 항목

클라이언트가 인트라넷에서 새 서버에 연결할 수 있으려면 클라이언트 액세스 서버의 가상 디렉터리에 내부 도메인 또는 URL을 구성한 다음 개인 DNS(도메인 이름 서비스) 레코드를 구성해야 합니다.

아래의 절차에서는 사용자가 인트라넷과 인터넷에서 동일한 URL을 사용하여 Exchange 서버에 액세스하도록 할지 또는 서로 다른 URL을 사용해야 하는지를 선택할 수 있습니다. 이미 적용되어 있거나 구현하려는 주소 지정 체계에 따라 선택이 달라집니다. 새 주소 지정 체계를 구현하는 경우 내부 및 외부 URL에 동일한 URL을 사용하는 것이 좋습니다. 동일한 URL을 사용하면 사용자가 하나의 주소만 기억하면 되기 때문에 Exchange 서버에 더 쉽게 액세스할 수 있습니다. 선택 내용에 관계없이 구성한 주소 공간에 대해 개인 DNS 영역을 구성해야 합니다. DNS 영역 관리에 대한 자세한 내용은 [DNS 서버 관리](http://go.microsoft.com/fwlink/p/?linkid=190631)를 참조하세요.

가상 디렉터리의 내부 및 외부 URL에 대한 자세한 내용은 [가상 디렉터리 관리](virtual-directory-management-exchange-2013-help.md)를 참조하세요.

## 내부 및 외부 URL을 동일하게 구성

1.  클라이언트 액세스 서버에서 Exchange 관리 셸을 엽니다.

2.  다음 단계에서 사용할 변수에 클라이언트 액세스 서버의 호스트 이름을 저장합니다. 예를 들어 Ex2013CAS와 같습니다.
    
    ```powershell
$HostName = "Ex2013CAS"
```

3.  셸에서 다음 명령을 각각 실행하여 각 내부 URL이 가상 디렉터리의 외부 URL과 일치하도록 구성합니다.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  또한 셸에서 자동 검색을 통해 OAB 배포를 위한 적절한 가상 디렉터리를 선택할 수 있게 OAB(오프라인 주소록)를 구성합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

클라이언트 액세스 서버 가상 디렉터리에 내부 URL을 구성한 다음에는 Outlook Web App 및 기타 연결에 대한 개인 DNS 레코드를 구성해야 합니다. 구성에 따라 클라이언트 액세스 서버의 FQDN(정규화된 도메인 이름)이나 내부 또는 외부 IP 주소를 가리키도록 개인 DNS 레코드를 구성해야 합니다. 다음은 내부 클라이언트 연결을 사용하기 위해 만들어야 하는 권장 DNS 레코드의 예입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 레코드 형식</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 이 단계의 작동 여부는 어떻게 확인합니까?

클라이언트 액세스 서버 가상 디렉터리에 내부 URL을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **가상 디렉터리**로 이동합니다.

2.  **서버 선택** 필드에서 인터넷 연결 클라이언트 액세스 서버를 선택합니다.

3.  가상 디렉터리를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **내부 URL** 필드가 아래 표시된 대로 올바른 FQDN 및 서비스로 채워져 있는지 확인합니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>가상 디렉터리</th>
    <th>내부 URL 값</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>자동 검색</strong></p></td>
    <td><p>내부 URL이 표시되지 않음</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


개인 DNS 레코드를 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  명령 프롬프트를 열고 `nslookup.exe`를 실행합니다.

2.  개인 DNS 영역을 쿼리할 수 있는 DNS 서버로 변경합니다.

3.  `nslookup`에서, 만든 각 FQDN의 레코드를 조회합니다. 각 FQDN에 대해 반환되는 값이 올바른지 확인합니다.

## 다른 내부 및 외부 URL 구성

1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **서버** \> **가상 디렉터리**로 이동합니다.

3.  **서버 선택** 필드에서 인터넷 연결 클라이언트 액세스 서버를 선택합니다.

4.  변경할 가상 디렉터리를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

5.  **내부 URL**에서 <strong>https://</strong>와 첫 번째 슬래시(<strong>/</strong> ) 사이의 호스트 이름을 사용할 새 FQDN으로 바꿉니다. 예를 들어 EWS 가상 디렉터리 FQDN을 Ex2013CAS.corp.contoso.com에서 internal.contoso.com으로 변경하려는 경우 내부 URL을 https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx에서 https://internal.contoso.com/ews/exchange.asmx로 변경합니다.

6.  **저장**을 클릭합니다.

7.  변경할 각 가상 디렉터리에 대해 5-6단계를 반복합니다.
    

    > [!NOTE]  
    > ECP 및 OWA 가상 디렉터리 내부 URL은 동일해야 합니다.<BR>자동 검색 가상 디렉터리에는 내부 URL을 설정할 수 없습니다.



8.  마지막으로 셸을 열고 자동 검색을 통해 OAB 배포를 위한 적절한 가상 디렉터리를 선택하도록 OAB(오프라인 주소록)를 구성해야 합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

클라이언트 액세스 서버 가상 디렉터리에 내부 URL을 구성한 다음에는 Outlook Web App 및 기타 연결에 대한 개인 DNS 레코드를 구성해야 합니다. 구성에 따라 클라이언트 액세스 서버의 FQDN이나 내부 또는 외부 IP 주소를 가리키도록 개인 DNS 레코드를 구성해야 합니다. 다음은 internal.contoso.com을 사용하도록 가상 디렉터리 내부 URL을 구성한 경우 내부 클라이언트 연결을 사용하기 위해 만들어야 하는 권장 DNS 레코드의 예입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 레코드 형식</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 이 단계의 작동 여부는 어떻게 확인합니까?

클라이언트 액세스 서버 가상 디렉터리에 내부 URL을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **가상 디렉터리**로 이동합니다.

2.  **서버 선택** 필드에서 인터넷 연결 클라이언트 액세스 서버를 선택합니다.

3.  가상 디렉터리를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **내부 URL** 필드가 올바른 FQDN으로 채워져 있는지 확인합니다. 예를 들어 internal.contoso.com을 사용하도록 내부 URL을 설정했을 수 있습니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>가상 디렉터리</th>
    <th>내부 URL 값</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>자동 검색</strong></p></td>
    <td><p>내부 URL이 표시되지 않음</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


개인 DNS 레코드를 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  명령 프롬프트를 열고 `nslookup.exe`를 실행합니다.

2.  개인 DNS 영역을 쿼리할 수 있는 DNS 서버로 변경합니다.

3.  `nslookup`에서, 만든 각 FQDN의 레코드를 조회합니다. 각 FQDN에 대해 반환되는 값이 올바른지 확인합니다.

## 6단계: SSL 인증서 구성

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "인증서 관리" 항목

Outlook Anywhere 및 Exchange ActiveSync와 같은 일부 서비스를 사용하려면 Exchange 2013 서버에 인증서를 구성해야 합니다. 다음 단계에서는 타사 CA(인증 기관)의 SSL 인증서를 구성하는 방법을 보여 줍니다.

1.  클라이언트 액세스 서버의 URL로 이동하여 EAC를 엽니다. 예를 들어 https://Ex2013CAS/ECP와 같습니다.

2.  **도메인\\사용자 이름** 및 **암호**에 사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  EAC에서 **서버** \> **인증서**로 이동합니다. **인증서** 페이지의 **서버 선택** 필드에서 클라이언트 액세스 서버가 선택되어 있는지 확인하고 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **새 Exchange 인증서** 마법사에서 **인증 기관의 인증서에 대한 요청 만들기**를 선택하고 **다음**을 클릭합니다.

5.  이 인증서의 이름을 지정하고 **다음**을 클릭합니다.

6.  와일드카드 인증서를 요청하려면 **와일드카드 인증서 요청**을 선택하고 **루트 도메인** 필드에 모든 하위 도메인의 루트 도메인을 지정합니다. 와일드카드 인증서를 요청하지 않고 대신 인증서에 추가할 각 도메인을 지정하려면 이 페이지를 비워 둡니다. **다음**을 클릭합니다.

7.  **찾아보기**를 클릭하고 인증서를 저장할 Exchange 서버를 지정합니다. 인터넷 연결 클라이언트 액세스 서버를 선택해야 합니다. **다음**을 클릭합니다.

8.  표시되는 목록의 각 서비스에 대해 사용자가 Exchange 서버에 연결하는 데 사용할 외부 또는 내부 서버 이름이 올바른지 확인합니다. 예를 들면 다음과 같습니다.
    
      - 내부 및 외부 URL을 동일하게 구성한 경우 **Outlook Web App(인터넷에서 액세스할 때)** 및 <strong>Outlook Web App(인트라넷에서 액세스할 때)</strong>에 owa.contoso.com이 표시되어야 합니다. **OAB(인터넷에서 액세스할 때)** 및 <strong>OAB(인트라넷에서 액세스할 때)</strong>에는 mail.contoso.com이 표시되어야 합니다.
    
      - 내부 URL을 internal.contoso.com으로 구성한 경우 <strong>Outlook Web App(인터넷에서 액세스할 때)</strong>에는 owa.contoso.com이 표시되고 <strong>Outlook Web App(인트라넷에서 액세스할 때)</strong>에는 internal.contoso.com이 표시되어야 합니다.
    
    이러한 도메인은 SSL 인증서 요청을 만드는 데 사용됩니다. **다음**을 클릭합니다.

9.  SSL 인증서에 포함할 도메인이 더 있으면 추가합니다.

10. 인증서의 일반 이름으로 사용할 도메인을 선택하고 **일반 이름으로 설정**을 클릭합니다 예를 들면 contoso.com과 같습니다. **다음**을 클릭합니다.

11. 조직에 대한 정보를 제공합니다. 이 정보는 SSL 인증서에 포함됩니다. **다음**을 클릭합니다.

12. 이 인증서 요청을 저장할 네트워크 위치를 지정합니다. **마침**을 클릭합니다.

인증서 요청을 저장한 후 CA(인증 기관)에 요청을 전송합니다. 조직에 따라 내부 CA 또는 타사 CA를 이용할 수 있습니다. 클라이언트 액세스 서버에 연결하는 클라이언트는 사용되는 CA를 신뢰해야 합니다. CA로부터 인증서를 받은 후에는 다음 단계를 완료합니다.

1.  EAC의 **서버** \> **인증서** 페이지에서, 이전 단계에서 만든 인증서 요청을 선택합니다.

2.  인증서 요청 세부 정보 창의 **상태**에서 **완료**를 클릭합니다.

3.  대기 중인 요청 완료 페이지에서 SSL 인증서 파일의 경로를 지정하고 **확인**을 클릭합니다.

4.  방금 추가한 새 인증서를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

5.  인증서 페이지에서 **서비스**를 클릭합니다.

6.  이 인증서에 할당할 서비스를 선택합니다. 최소한 **SMTP**와 **IIS**는 선택해야 합니다. **저장**을 클릭합니다.

7.  <strong>기존 기본 SMTP 인증서를 덮어쓰시겠습니까?</strong>라는 경고 메시지가 나타나면 **예**를 클릭합니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

새 인증서가 추가되었는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **인증서**로 이동합니다.

2.  새 인증서를 선택하고 인증서 세부 정보 창에서 다음 사항을 확인합니다.
    
      - **상태**가 **유효**로 나타나야 합니다
    
      - **서비스에 할당**에 적어도 **IIS** 및 **SMTP**가 표시되어야 합니다

## 이 작업의 작동 여부는 어떻게 확인합니까?

메일 흐름 및 외부 클라이언트 액세스가 구성되었는지 확인하려면 다음을 수행합니다.

1.  Outlook, Exchange ActiveSync 장치 또는 둘 모두에서 새 프로필을 만듭니다. Outlook 또는 모바일 장치에 새 프로필이 만들어졌는지 확인합니다.

2.  Outlook 또는 모바일 장치에서 외부 받는 사람에게 새 메시지를 보냅니다. 외부 받는 사람이 메시지를 받는지 확인합니다.

3.  외부 받는 사람의 사서함에서 메시지(방금 전에 Exchange 사서함에서 보낸 메시지)에 회신합니다. Exchange 사서함에 해당 메시지가 수신되었는지 확인합니다.

4.  https://owa.contoso.com/owa로 이동하여 인증서 경고가 없는지 확인합니다.


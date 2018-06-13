---
title: 'Exchange 하이브리드 배포의 IRM: Exchange 2013 Help'
TOCTitle: Exchange 하이브리드 배포의 IRM
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50484634
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 하이브리드 배포의 IRM

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

**요약:** Exchange 하이브리드 환경에서 IRM이 작동하는 방법 및 Exchange Online과 온-프레미스 Exchange 서버 간에 작동하도록 IRM을 구성하는 방법입니다.

IRM(정보 권한 관리)은 전자 메일 메시지와 첨부 파일을 온라인과 오프라인에서 지속적으로 보호하여 중요한 정보 유출을 방지할 수 있도록 도와줍니다. 엔터프라이즈용 Office 365에서 Exchange 온-프레미스 조직과 Exchange Online은 모두 IRM을 지원합니다. 하지만 두 구현 간에는 차이점이 있으며 Exchange Online 조직에서 IRM을 먼저 구성해야 해당 조직의 사용자가 사용할 수 있습니다.

IRM은 Windows Server 2008 이상의 구성 요소인 AD RMS(Active Directory Rights Management Services)를 사용합니다. AD RMS를 사용하면 사용자가 전자 메일 메시지, 첨부 파일 등의 권한으로 보호된 콘텐츠를 만든 다음 해당 콘텐츠의 사용 방법과 배포 대상을 제어할 수 있습니다. 사용자는 콘텐츠 사용 방법을 결정하는 템플릿을 지정할 수 있습니다. 예를 들어, 사용자가 전자 메일 메시지를 다른 받는 사람에게 전달할 수 없거나 메시지의 정보를 복사할 수 없도록 지정할 수 있습니다.

Exchange 2010의 IRM에 대한 자세한 내용은 다음을 참조하세요. [정보 권한 관리 이해](https://technet.microsoft.com/ko-kr/library/dd638140\(v=exchg.141\).aspx).

[정보 권한 관리](https://technet.microsoft.com/ko-kr/library/dd638140\(v=exchg.150\))에서 Exchange 2013 및 Exchange 2016의 IRM에 대해 자세히 알아보세요.

AD RMS에 대한 자세한 내용은 [Active Directory Rights Management Services 개요](http://go.microsoft.com/fwlink/p/?linkid=215243)를 참조하십시오.

## Exchange 온-프레미스의 IRM과 Exchange Online의 IRM 간 차이점

온-프레미스 Exchange 조직에서 사용할 수 있는 IRM 기능은 Exchange Online 조직에서 사용할 수 있는 기능과 다릅니다. 다음 표에는 각 조직에서 사용할 수 있는 기능이 요약되어 있습니다. 이러한 기능에 대한 자세한 내용은 [정보 권한 관리](https://technet.microsoft.com/ko-kr/library/dd638140\(v=exchg.150\))를 참조하세요.

### 사용할 수 있는 IRM 기능

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>Exchange 2007 및 이전 버전에서 사용 가능</th>
<th>Exchange 2010에서 사용 가능</th>
<th>Exchange Online 및 Exchange 2013 이상에서 사용 가능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook에서 수동 메시지 보호</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App에서 수동 메시지 보호</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Outlook에서 IRM으로 보호된 메시지 보기</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App에서 IRM으로 보호된 메시지 보기</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>IRM 사전 라이선스 에이전트</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>RMS 정책 템플릿</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>전송 암호 해독</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>저널 보고서 암호 해독</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 검색 암호 해독</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>자동 Outlook 보호 규칙</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>자동 전송 보호 규칙</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


## 하이브리드 배포에서의 IRM

Exchange는 Exchange 서버가 설치되어 있는 Active Directory 포리스트의 AD RMS 서버를 사용합니다. 온-프레미스 Exchange 서버의 경우 온-프레미스 AD RMS 서버가 사용됩니다. Exchange Online 조직의 경우 Office 365 데이터 센터 내에서 유지 관리되는 AD RMS 서버가 사용됩니다. 각 Exchange 조직이 사용하는 AD RMS 구성은 다른 AD RMS 배포에 독립적입니다.

AD RMS 구성 및 IRM 구성은 온-프레미스 Exchange 조직과 Exchange Online 조직 간에 자동으로 복제되지 않습니다. 정의한 AD RMS 템플릿이 Exchange Online 조직에 자동으로 복사되지 않습니다. Exchange Online 조직에서 동일한 AD RMS 템플릿을 사용할 수 있으려면 온-프레미스 조직에서 템플릿을 수동으로 내보낸 다음 Office 365 조직에 적용해야 합니다. 이 항목의 뒷부분에 나오는 하이브리드 배포의 IRM 구성을 참조하세요.

## 사용자 환경

사용자에게 적용되는 IRM 구성은 사용자가 사용하는 클라이언트와 사용자 사서함의 위치에 따라 달라집니다. 다음 표는 사용자가 사용할 AD RMS 서버를 보여 줍니다.

### 활성 AD RMS 서버

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트</th>
<th>온-프레미스 사서함</th>
<th>Exchange Online 사서함</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 데스크톱 클라이언트</p></td>
<td><p>온-프레미스 AD RMS</p></td>
<td><p>온-프레미스 AD RMS</p></td>
</tr>
<tr class="even">
<td><p>웹에서 Outlook</p></td>
<td><p>온-프레미스 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSync 장치</p></td>
<td><p>온-프레미스 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
</tbody>
</table>


온-프레미스 조직과 Exchange Online 조직에서 구성한 AD RMS 구성에 따라 Outlook 2007 및 웹에서 Outlook를 사용하는 사용자에게 다른 AD RMS 템플릿이 표시될 수도 있습니다. 따라서 온-프레미스 조직과 Exchange Online 조직에 동일한 템플릿을 적용하는 것이 좋습니다.

사용자 사서함이 온-프레미스 조직에 있든, Exchange Online 조직에 있든 관계없이 Outlook 클라이언트 사용자의 IRM 환경이 동일해야 합니다.

사서함이 Exchange 온-프레미스 서버에 있는 웹에서 Outlook 사용자는 Internet Explorer용 권한 관리 추가 기능을 설치한 후에만 권한으로 보호된 메시지를 열 수 있으며, 권한으로 보호된 메시지를 새로 만들거나 회신할 수는 없습니다.

사서함이 Exchange Online에 있는 웹에서 Outlook 사용자는 추가 소프트웨어 없이 권한으로 보호된 메시지를 열 수 있으며, 권한으로 보호된 메시지를 새로 만들고 회신할 수 있습니다.

## 서버 기능

온-프레미스 Exchange 서버는 사용자가 메시지를 열 때 자격 증명을 제공할 필요가 없도록 AD RMS 사전 라이선스 에이전트를 사용하여 권한으로 보호된 메시지의 암호를 해독합니다. 온-프레미스 Exchange 서버는 온-프레미스 AD RMS 서버에 연결하여 사용 정책과 권한을 확인하고 메시지 암호 해독을 위한 권한 부여를 요청합니다.

Exchange Online 조직은 Exchange Online AD RMS를 사용하는 여러 IRM 관련 기능을 추가로 제공합니다. 저널 보고서 암호 해독과 같은 이러한 기능은 Exchange 서비스가 추가 처리를 위해 권한으로 보호된 메시지의 콘텐츠를 사용할 수 있게 합니다. 예를 들어, 보다 편리한 검색을 위해 저널링된 메시지의 암호 해독 콘텐츠를 권한으로 보호된 원본 메시지와 함께 저장할 수 있습니다. 뿐만 아니라 Outlook 보호 규칙 또는 전송 규칙을 통해 메시지에 IRM 템플릿을 자동으로 적용하여 메시지가 정보 보호와 관련해서 조직 정책을 준수하도록 할 수 있습니다.

## 하이브리드 배포의 IRM 구성

Exchange의 IRM은 Exchange 서버가 있는 Active Directory 포리스트에 배포되는 AD RMS를 사용합니다. AD RMS 구성은 온-프레미스 조직과 Exchange Online 조직 간에 자동으로 동기화되지 않습니다. 온-프레미스 AD RMS 서버에서 TPD(트러스트된 게시 도메인)라는 AD RMS 구성을 수동으로 내보낸 다음 Exchange Online 조직으로 가져와야 합니다. TPD에는 템플릿을 비롯하여 Exchange Online 조직이 IRM을 사용하는 데 필요한 AD RMS 구성이 포함됩니다.

자세한 내용은 [AD RMS 트러스트된 게시 도메인 고려 사항](http://go.microsoft.com/fwlink/p/?linkid=215244)을 참조하십시오.

Exchange Online 조직에 온-프레미스 AD RMS 구성을 적용하는 것 외에도 온-프레미스 네트워크 외부의 Outlook 및 ActiveSync 클라이언트가 AD RMS 서버에 연결할 수 있는지 확인해야 합니다. 이러한 클라이언트가 온-프레미스 네트워크 외부에서 권한으로 보호된 메시지에 액세스하려는 경우 이 작업을 수행해야 합니다.

온-프레미스 네트워크를 구성하고 TPD 데이터를 내보낸 후 TPD 데이터를 가져오고 IRM을 사용하도록 설정하여 Exchange Online 조직을 구성해야 합니다.


> [!NOTE]
> 온-프레미스 AD RMS 구성을 수정할 때마다 Exchange Online 조직에 새 구성을 수동으로 적용해야 합니다. 이렇게 하려면 온-프레미스 AD RMS 서버에서 TPD 데이터를 내보낸 다음 Exchange Online 조직으로 가져옵니다.



## Exchange 하이브리드 배포에서 IRM을 구성하는 방법

온-프레미스 Exchange 조직에 IRM을 사용하고 Exchange Online 사용자가 IRM도 사용하게 하려면 다음을 수행해야 합니다.

1.  온-프레미스 AD RMS(Active Directory 권한 관리 서비스) 서버를 구성합니다.

2.  Exchange Online 조직에서 IRM을 사용하도록 설정합니다.

3.  가져온 AD RMS 템플릿을 Exchange Online 조직의 사용자에게 배포합니다.

## 온-프레미스 AD RMS 서버를 구성하려면 어떻게 해야 합니까?

하이브리드 배포에서 IRM을 구성하려면 Windows PowerShell을 사용하여 온-프레미스 AD RMS 서버에 액세스해야 합니다. 자세한 내용은 다음을 참조하십시오. [Windows PowerShell을 사용하여 AD RMS 관리](http://go.microsoft.com/fwlink/p/?linkid=214938)

다음 작업을 수행하여 TPD(트러스트된 게시 도메인) 데이터를 온-프레미스 AD RMS 서버에서 내보낸 다음 외부 클라이언트에 대해 AD RMS 서버 액세스를 구성합니다.

1.  온-프레미스 조직에서 TPD 데이터를 내보냅니다. 자세한 내용은 다음을 참조하십시오. [트러스트된 게시 도메인 내보내기](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  외부 클라이언트에서 AD RMS 서버 액세스를 구성합니다. 자세한 내용은 다음을 참조하십시오. [엑스트라넷 클러스터 URL 추가](http://go.microsoft.com/fwlink/p/?linkid=214945)

## Exchange Online 조직에서 IRM을 사용하도록 설정하려면 어떻게 해야 합니까?

온-프레미스 AD RMS 서버에서 TPD 데이터를 내보낸 후 Exchange Online 조직으로 해당 데이터를 가져오고 IRM을 사용하도록 설정해야 합니다.

1.  Exchange Online 조직에서 TPD 데이터를 가져옵니다.
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Exchange Online 조직에서 IRM을 사용하도록 설정합니다.
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## Exchange Online 조직에 AD RMS 템플릿을 배포하려면 어떻게 해야 합니까?

Exchange Online 조직에서 IRM을 사용하도록 설정한 후에 가져온 AD RMS 템플릿을 배포해야 합니다. 다음 Exchange Online 사용자 및 기능은 AD RMS 템플릿을 사용합니다.

  - 웹에서 Outlook 사용자

  - Exchange ActiveSync 사용자

  - 전송 규칙

  - 저널 보고서 암호 해독

  - Outlook 보호 규칙

<!-- end list -->

1.  Exchange Online 조직에서 AD RMS 템플릿 목록을 검색합니다.
    
        Get-RMSTemplate -Type All

2.  Exchange Online 조직의 사용자와 기능에 AD RMS 템플릿을 배포합니다.
    
        Set-RMSTemplate <template name> -Type Distributed
    

    > [!NOTE]
    > "전달하지 않음" AD RMS 템플릿은 수정할 수 없습니다.



3.  배포할 각 AD RMS에 대해 2단계를 반복합니다.

## 작동 여부는 어떻게 확인합니까?

웹에서 Outlook 사용자는 AD RMS 템플릿을 새 메시지에 적용할 수 있습니다. 웹에서 Outlook 및 Exchange ActiveSync 사용자는 AD RMS 템플릿을 적용한 메시지를 읽을 수 있습니다. 또한, **Get-RMSTemplate** cmdlet을 실행하면 온-프레미스 조직에서 가져온 AD RMS 템플릿이 모두 나열됩니다.

Exchange Online 조직에서 다음 명령을 실행합니다.

    Get-RMSTemplate 

자세한 내용은 다음을 참조하십시오. [Outlook Web App에서 정보 권한 관리](https://technet.microsoft.com/ko-kr/library/dd876891\(v=exchg.150\))


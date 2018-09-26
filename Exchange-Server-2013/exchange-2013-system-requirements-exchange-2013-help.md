---
title: 'Exchange 2013 시스템 요구 사항: Exchange 2013 Help'
TOCTitle: Exchange 2013 시스템 요구 사항
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50482626
ms.date: 02/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 시스템 요구 사항

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange 2013을 설치하기 전에 알아야 하는 Exchange 2013 요구 사항을 알아봅니다. 예를 들어 하드웨어, 네트워크 및 운영 체제 요구 사항에 대해 알아봅니다.

Microsoft Exchange Server 2013을 설치하기 전에 이 항목을 검토하여 네트워크, 하드웨어, 소프트웨어, 클라이언트 및 기타 요소가 Exchange 2013의 요구 사항을 충족하는지 확인하는 것이 좋습니다. 또한 Exchange 2013과 이전 버전의 Exchange에 지원되는 동시 사용 시나리오를 이해해야 합니다.

## 지원되는 동시 사용 시나리오

다음 표에서는 Exchange 2013과 Exchange 이전 버전의 동시 사용이 지원되는 시나리오를 보여 줍니다.

### Exchange 2013과 Exchange Server 이전 버전의 동시 사용

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 버전</th>
<th>Exchange 조직 동시 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 이하 버전</p></td>
<td><p>지원되지 않음</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>1Edge 전송 서버를 포함하여 조직의 모든 Exchange 2007 서버에 Exchange 2007 SP3(서비스 팩 3)용 업데이트 롤업 10이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2(누적 업데이트 2)가 설치된 경우.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>2Edge 전송 서버를 포함하여 조직의 모든 Exchange 2010 서버에 Exchange 2010 SP3이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2가 설치된 경우.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2010 및 Exchange 2007 혼합 조직</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>1Edge 전송 서버를 포함하여 조직의 모든 Exchange 2007 서버에 Exchange 2007 SP3용 업데이트 롤업 10이 설치된 경우</p></li>
<li><p>2Edge 전송 서버를 포함하여 조직의 모든 Exchange 2010 서버에 Exchange 2010 SP3이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2가 설치된 경우.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Exchange 2007 허브 전송 서버와 Exchange 2013 SP1 Edge 전송 서버 간에 구독을 만들려면 Exchange 2007 허브 전송 서버에 Exchange 2007 SP3 업데이트 롤업 13 이상을 설치해야 합니다.

2   Exchange 2010 허브 전송 서버와 Exchange 2013 SP1 Edge 전송 서버 간에 구독을 만들려면 Exchange 2010 허브 전송 서버에 Exchange 2010 SP3 업데이트 롤업 5 이상을 설치해야 합니다.

## 지원되는 하이브리드 배포 시나리오

Exchange 2013에서는 최신 버전의 Office 365로 업그레이드된 Office 365 테넌트를 사용한 하이브리드 배포가 지원됩니다. 특정 하이브리드 배포에 대한 자세한 내용은 [하이브리드 배포 필수 구성 요소](https://technet.microsoft.com/ko-kr/library/hh534377\(v=exchg.150\)) 항목을 참조하세요.

## 네트워크 및 디렉터리 서버

다음 표에서는 Exchange 2013 조직의 네트워크 및 디렉터리 서버에 대한 요구 사항을 보여줍니다.

**Exchange 2013에 대한 네트워크 및 디렉터리 서버 요구 사항**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 요소</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>스키마 마스터</p></td>
<td><p>기본적으로 스키마 마스터는 포리스트에 설치된 첫 번째 Active Directory 도메인 컨트롤러에서 실행됩니다. 스키마 마스터가 다음 중 하나를 실행하고 있어야 합니다.</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 또는 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 또는 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 또는 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2008 Standard 또는 Enterprise(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2003 Standard Edition SP2(서비스 팩 2) 이상(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 이상(32비트 또는 64비트)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>글로벌 카탈로그 서버</p></td>
<td><p>Exchange 2013을 설치할 계획인 각 Active Directory 사이트에는 다음 중 하나를 실행하는 글로벌 카탈로그 서버가 하나 이상 있어야 합니다.</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 또는 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 또는 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 또는 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2008 Standard 또는 Enterprise(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2003 Standard Edition SP2(서비스 팩 2) 이상(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 이상(32비트 또는 64비트)</p></li>
</ul>
<p>글로벌 카탈로그 서버에 대한 자세한 내용은 <a href="http://go.microsoft.com/fwlink/p/?linkid=178996">글로벌 카탈로그란?</a>을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p>도메인 컨트롤러</p></td>
<td><p>Exchange 2013을 설치할 계획인 각 Active Directory 사이트에는 다음 중 하나를 실행하는 쓰기 가능한 도메인 컨트롤러가 하나 이상 있어야 합니다.</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 또는 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 또는 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 또는 Enterprise SP1 이상</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2008 Standard 또는 Enterprise SP1 이상(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 이상</p></li>
<li><p>Windows Server 2003 Standard Edition SP2(서비스 팩 2) 이상(32비트 또는 64비트)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 이상(32비트 또는 64비트)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Active Directory 포리스트</p></td>
<td><p>Active Directory는 Windows Server 2003 포리스트 기능 모드 이상이어야 합니다2.</p></td>
</tr>
<tr class="odd">
<td><p>DNS 네임스페이스 지원</p></td>
<td><p>Exchange 2013에서는 다음 DNS(Domain Name System) 네임스페이스가 지원됩니다.</p>
<ul>
<li><p>연속</p></li>
<li><p>비연속</p></li>
<li><p>단일 레이블 도메인</p></li>
<li><p>분리</p></li>
</ul>
<p>Exchange에서 지원되는 DNS 네임스페이스에 대한 자세한 내용은 Microsoft 기술 자료 문서 2269838, <a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2269838">단일 레이블 도메인, 분리된 네임스페이스 및 연속하지 않는 네임스페이스와의 Microsoft Exchange 호환성</a>을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>IPv6 지원</p></td>
<td><p>Exchange 2013에서 IPv6은 IPv4도 함께 설치하여 사용할 때만 지원됩니다. 이 구성에서 Exchange 2013을 배포하고 네트워크에서 IPv4 및 IPv6이 지원되는 경우 모든 Exchange 서버는 IPv6 주소를 사용하는 장치, 서버 및 클라이언트와 데이터를 주고받을 수 있습니다. 자세한 내용은 <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 IPv6 지원</a>을 참조하세요.</p></td>
</tr>
</tbody>
</table>


1Windows Server 2012 R2는 Exchange 2013 SP1 이상에서만 지원됩니다.

2Windows Server 2012 R2 포리스트 기능 모드는 Exchange 2013 SP1 이상에서만 지원됩니다.

## 디렉터리 서버 아키텍처

64비트 Active Directory 도메인 컨트롤러를 사용하면 Exchange 2013의 디렉터리 서비스 성능이 향상됩니다.


> [!NOTE]
> 멀티 도메인 환경에서, Active Directory 언어 로캘이 일본어로 설정된 Windows Server 2008 도메인 컨트롤러의 경우 인바운드 복제 중 개체에 저장되는 일부 특성을 수신하지 못할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 문서 949189, <A href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=949189">일본어 로캘을 사용하여 구성된 Windows Server 2008 도메인 컨트롤러는 인바운드 복제 중 개체의 특성에 업데이트를 적용하지 못할 수 있습니다.</A>를 참조하세요.



## 디렉터리 서버에 Exchange 2013 설치

보안 및 성능상의 이유로, Active Directory 디렉터리 서버가 아닌 구성원 서버에만 Exchange 2013을 설치하는 것이 좋습니다. 그러나 Exchange 2013을 실행하는 컴퓨터에서는 DCPromo를 실행할 수 없습니다. Exchange 2013을 설치한 후에는 구성원 서버에서 디렉터리 서버로 또는 그 반대로 역할을 변경할 수 없습니다.

## 하드웨어

Exchange 2013 서버에 권장되는 하드웨어 요구 사항은 설치되는 서버 역할 및 서버에서 부담할 예상 부하를 비롯한 여러 가지 요소에 따라 달라집니다.

배포의 크기를 적절하게 조정하고 배포를 구성하는 방법에 대한 자세한 내용은 [Exchange 2013 크기 조정 및 구성 권장 사항](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md)을 참조하세요.

가상화된 환경에서의 Exchange 배포에 대한 자세한 내용은 [Exchange 2013 가상화](exchange-2013-virtualization-exchange-2013-help.md)를 참조하세요.

**Exchange 2013 하드웨어 요구 사항**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 요소</th>
<th>요구 사항</th>
<th>참고</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>프로세서</p></td>
<td><ul>
<li><p>Intel 64 아키텍처(이전의 Intel EM64T)를 지원하는 Intel 프로세서 x64 아키텍처 기반 컴퓨터</p></li>
<li><p>AMD64 플랫폼을 지원하는 AMD 프로세서</p></li>
<li><p>Intel Itanium IA64 프로세서는 지원되지 않음</p></li>
</ul></td>
<td><p>지원되는 운영 체제에 대해서는 이 항목 뒷부분의 &quot;운영 체제&quot; 섹션을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>메모리</p></td>
<td><p>설치된 Exchange 역할에 따라 다름:</p>
<ul>
<li><p><strong>사서함</strong>   최소 8GB</p></li>
<li><p><strong>클라이언트 액세스</strong>   최소 4GB</p></li>
<li><p><strong>사서함 및 클라이언트 액세스 결합</strong>   최소 8GB</p></li>
<li><p><strong>Edge 전송</strong>   최소 4GB</p></li>
</ul></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>페이징 파일 크기</p></td>
<td><p>최소 및 최대 페이지 파일 크기는 32GB에 10MB를 더한 크기여야 하며, 32GB RAM을 초과하여 사용하는 경우 최대 크기가 32778MB여야 합니다.</p></td>
<td><p>페이지 파일 권장 사항에 대한 자세한 내용은 <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Exchange 2013 크기 조정 및 구성 권장 사항</a>의 &quot;페이지 파일&quot; 섹션을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>디스크 공간</p></td>
<td><ul>
<li><p>Exchange를 설치할 드라이브에 30GB 이상 필요</p></li>
<li><p>설치할 각 UM(통합 메시징) 언어 팩에 대해 500MB의 사용 가능한 추가 디스크 공간 필요</p></li>
<li><p>시스템 드라이브에 200MB의 사용 가능한 디스크 공간</p></li>
<li><p>500MB 이상의 여유 공간이 있는 메시지 큐 데이터베이스 저장용 하드 디스크</p></li>
</ul></td>
<td><p>저장소 권장 사항에 대한 자세한 내용은 <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Exchange 2013 저장소 구성 옵션</a>을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p>드라이브</p></td>
<td><p>DVD-ROM 드라이브(로컬 또는 네트워크 액세스 가능)</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>화면 해상도</p></td>
<td><p>1024 x 768픽셀 이상</p></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>파일 형식</p></td>
<td><p>다음 파티션에 적용되는 NTFS 파일 시스템으로 포맷된 디스크 파티션</p>
<ul>
<li><p>시스템 파티션</p></li>
<li><p>Exchange 이진 파일 또는 Exchange 진단 로깅에 의해 생성된 파일을 저장하는 파티션</p></li>
</ul>
<p>다음 유형의 파일을 포함하는 디스크 파티션은 ReFS로 서식을 지정할 수 있습니다.</p>
<ul>
<li><p>트랜잭션 로그 파일이 있는 파티션</p></li>
<li><p>데이터베이스 파일이 있는 파티션</p></li>
<li><p>콘텐츠 인덱싱 파일이 있는 파티션</p></li>
</ul></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## 운영 체제

다음 표에는 Exchange 2013에 대해 지원되는 운영 체제가 나열되어 있습니다.


> [!IMPORTANT]   
> Windows Server Core 모드에서 실행되는 컴퓨터에 Exchange 2013 설치는 지원되지 않습니다. 컴퓨터에서 Windows Server의 전체 설치가 실행 중이어야 합니다. Windows Server Core 모드에서 실행 중인 컴퓨터에 Exchange 2013을 설치하려면 다음 중 하나를 수행하여 서버를 Windows Server 전체 설치로 변환해야 합니다. 
> <UL>
> <LI>
> <P><STRONG>Windows Server 2008 R2</STRONG>&nbsp;&nbsp;&nbsp;Windows Server를 다시 설치하고 <STRONG>전체 설치</STRONG> 옵션을 선택합니다.</P>
> <LI>
> <P><STRONG>Windows Server 2012 R2</STRONG> 또는 <STRONG>Windows Server 2012</STRONG>&nbsp;&nbsp;&nbsp;다음 명령을 실행하여 Windows Server Core 모드 서버를 전체 설치로 변환합니다.</P>

```powershell
Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart
```
</LI></UL>



**Exchange 2013에 대해 지원되는 운영 체제**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 요소</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사서함, 클라이언트 액세스 및 Edge 전송 서버 역할</p></td>
<td><p>다음 운영 체제 중 하나</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 또는 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 또는 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard SP1(서비스 팩 1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise SP1(서비스 팩 1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 이상</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>관리 도구</p></td>
<td><p>다음 운영 체제 중 하나</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 또는 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 또는 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 이상</p></li>
<li><p>64비트 버전의 Windows 8.12</p></li>
<li><p>64비트 버전의 Windows 8</p></li>
<li><p>64비트 버전의 Windows 7 서비스 팩 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2는 Exchange 2013 SP1 이상에서만 지원됩니다.

2   Windows 8.1은 Exchange 2013 SP1 이상에서만 지원됩니다.

**Exchange 2013에 대해 지원되는 Windows Management Framework 버전**

Exchange 2013에서는 Exchange를 설치하려는 Windows 릴리스에 구축된 Windows Management Framework 버전만 지원합니다. Exchange를 실행하는 서버에서 독립 실행형 다운로드로 사용할 수 있는 Windows Management Framework 버전은 설치하지 마세요.

## .NET Framework

설치하려는 Exchange 릴리스에서 지원하는 .NET Framework의 최신 버전을 사용하는 것이 좋습니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 버전</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 지원되는 클라이언트

Exchange 2013에서는 다음 버전의 Outlook 및 Entourage for Mac을 지원합니다.

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 for Mac, Web Services Edition

  - Office 365용 Outlook for Mac

  - Outlook for Mac 2011

Exchange에서 지원하는 Outlook 릴리스 목록에 대해서는 [Outlook 업데이트](https://go.microsoft.com/fwlink/p/?linkid=513459)를 참조하세요.


> [!IMPORTANT]
> 사용자가 Exchange에 연결할 때 가능한 최상의 환경을 사용할 수 있도록 최신 서비스 팩과 업데이트를 설치하는 것이 좋습니다.



Outlook 2007 이전의 Outlook 클라이언트는 지원되지 않습니다. Entourage 2008 for Mac RTM 및 Entourage 2004와 같이 DAV가 필요한 Mac 운영 체제의 전자 메일 클라이언트는 지원되지 않습니다.

Outlook Web App은 다양한 운영 체제 및 장치의 브라우저를 지원합니다. 자세한 내용은 [Exchange 2013에서 Outlook Web App의 새 기능](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)을 참조하세요.


---
title: 'Edge 전송 서버 계획: Exchange 2013 Help'
TOCTitle: Edge 전송 서버 계획
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61545105
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버 계획

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Edge 전송 서버 역할은 Exchange 서비스 팩 1에 다시 도입되었습니다. Edge 전송은 Exchange 조직에 향상된 스팸 방지 보호 기능을 제공합니다. 또한 Edge 전송 서버는 조직 간의 전송 시 정책을 메시지에 적용합니다. 이 서버 역할은 경계 네트워크 및 Active Directory 포리스트 외부에서 배포됩니다. Edge 전송 서버는 구성 및 받는 사람 정보를 위해 클라이언트 액세스 또는 사서함 서버와 같은 방식으로 Active Directory에 직접 액세스하지 않습니다. Edge 전송 서버는 AD LDS(Active Directory Lightweight Directory Service)를 사용하여 구성 및 받는 사람 정보를 로컬로 저장합니다.

기존 Exchange 2013 조직에 Edge 전송 서버를 추가할 수 있습니다. Edge 전송 서버를 설치할 때 추가 Active Directory 준비 단계를 수행할 필요가 없습니다.


> [!NOTE]
> 기존 Exchange 2010 또는 Exchange 2007 조직에 Edge 전송을 추가 하는 경우에 레거시 서버에서 Edge 전송 Exchange 2013 을 설치 하기 전에 특정 롤업 업데이트를 설치 해야 합니다. 자세한 내용은 <A href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</A>를 참조 합니다.



Edge 전송 서버를 배포할 계획이 있는 경우 다음 문제를 고려해야 합니다.

  - **서버 용량** 서버 용량 계획에는 Edge 전송 서버의 성능 모니터링 수행 계획이 포함됩니다. 성능 모니터링은 서버의 작동 부하를 이해하는 데 도움을 줍니다. 이 정보를 통해 현재 하드웨어 구성의 용량을 결정합니다.

  - **전송 기능** Edge 전송 서버는 네트워크 경계면에서 스팸 방지 보호를 제공할 수 있습니다. 계획 프로세스의 일부로 Edge 전송 서버에서 사용하려는 스팸 방지 기능 및 구성 방법을 결정해야 합니다.

  - **보안**Edge 전송 서버 역할은 공격 영역을 최소화하도록 설계되었습니다. 따라서 서버에 대한 실제 액세스 및 네트워크 액세스 모두를 제대로 보안하고 관리하는 것이 중요합니다. 보안 계획은 권한이 있는 서버 및 사용자에서만 IP 연결을 사용할 수 있는지 확인하는 데 도움을 줍니다. 자세한 내용은 [배포 보안 검사 목록](deployment-security-checklist-exchange-2013-help.md)를 참조하세요.
    
    경계 네트워크 내에 Edge 전송 서버를 배치하는 것이 좋습니다. 서버에서 전자 메일을 주고받고 Microsoft Exchange EdgeSync Service로부터 받는 사람 및 구성 데이터 업데이트를 받을 수 있게 하려면 다음 표에 나와 있는 포트를 통한 통신을 허용해야 합니다.
    
    ### Edge 전송 서버에 사용할 통신 포트 설정
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>네트워크 인터페이스</th>
    <th>개방 포트</th>
    <th>프로토콜</th>
    <th>참고</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>인터넷 인바운드 및 아웃바운드</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>이 포트는 인터넷에서 들어오고 나가는 메일 흐름에 필요합니다.</p></td>
    </tr>
    <tr class="even">
    <td><p>내부 네트워크 인바운드 및 아웃바운드</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>이 포트는 Exchange 조직에서 들어오고 나가는 메일 흐름에 필요합니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p>로컬 전용</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>이 포트는 AD LDS에 대한 로컬 연결을 설정하는 데 사용됩니다.</p></td>
    </tr>
    <tr class="even">
    <td><p>내부 네트워크에서 인바운드</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>보안 LDAP</p></td>
    <td><p>이 포트는 EdgeSync 동기화에 필요합니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p>내부 네트워크에서 인바운드</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>이 포트를 여는 것은 선택 사항입니다. 이 포트를 열면 원격 데스크톱 연결을 통해 Edge 전송 서버를 관리할 수 있으므로 내부 네트워크에서 Edge 전송 서버를 보다 유연하게 관리할 수 있습니다.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > Edge 전송 서버 역할은 비표준 LDAP 포트를 사용합니다. 이 항목에 지정된 포트는 Edge 전송 서버 역할을 설치할 때 구성되는 LDAP 통신 포트입니다.



  - **EdgeSync**   Edge 구독을 만들어 Edge 전송 서버를 Exchange 조직에 가입시키는 것이 권장 배포 프로세스입니다. Edge 구독을 만들면 받는 사람 및 구성 데이터가 Active Directory에서 AD LDS로 복제됩니다. Edge 전송 서버가 Active Directory 사이트에 가입합니다. 그런 다음 해당 사이트의 사서함 서버에서 실행되는 MicrosoftExchange EdgeSync 서비스가 Active Directory에서 데이터를 동기화하여 AD LDS를 주기적으로 업데이트합니다. Edge 구독 프로세스는 Edge 전송 서버를 통해 Exchange 조직에서 인터넷으로 메일 흐름을 사용하는 데 필요한 송신 커넥터를 자동으로 프로비전합니다. Edge 전송 서버에서 받는 사람 조회 또는 수신 허용 목록 집계를 사용하는 경우 Edge 전송 서버를 조직에 가입시켜야 합니다.

## Edge 전송 서버 역할에 대한 DNS 설정 구성

Edge 전송 서버는 Exchange 조직 외부에 경계 네트워크의 독립형 서버로 배포되거나 경계 네트워크 Active Directory 도메인의 구성원으로 배포됩니다. Exchange 2013을 설치하기 전에 Edge 전송 서버 역할에 대한 올바른 DNS 접미사를 수동으로 구성해야 합니다. DNS 접미사가 구성되지 않은 경우 설치가 중지됩니다.

Edge 전송 서버는 경계 네트워크에 배포되므로 여러 네트워크 세그먼트에 연결된 네트워크 인터페이스가 있습니다. 이러한 네트워크 세그먼트마다 고유한 IP 구성을 가집니다. 외부 또는 공용 네트워크 세그먼트에 연결된 네트워크 인터페이스는 이름 확인을 위해 공용 DNS 서버를 사용하도록 구성해야 합니다. 이를 통해 서버는 MX 리소스 레코드에 대한 SMTP 도메인 이름을 확인하고 메일을 인터넷으로 라우팅할 수 있습니다.

내부 또는 개인 네트워크 세그먼트에 연결된 네트워크 인터페이스는 조직에 있는 사서함 서버의 이름을 확인할 수 있는 DNS 서버를 사용하도록 구성하거나 호스트 파일을 사용할 수 있도록 해야 합니다. Edge 전송 서버 및 사서함 서버는 DNS 호스트 확인을 사용하여 서로 간에 찾을 수 있어야 합니다.

Edge 전송 서버를 통해 사서함 서버의 이름을 확인하려면 다음 방법 중 하나를 사용합니다.

  - Edge 전송 서버의 내부 네트워크 어댑터에 구성된 DNS 서버의 정방향 조회 영역에서 사서함 서버에 대한 리소스 레코드를 수동으로 만듭니다.

  - 사서함 서버에 대한 호스트 레코드를 포함하도록 Edge 전송 서버의 호스트 파일을 편집합니다. 호스트 파일은 4.3 BSD(Berkeley Software Distribution) UNIX /etc/hosts 파일과 동일한 형식의 로컬 텍스트 파일입니다. 이 파일은 호스트 이름을 IP 주소에 매핑하며 파일은 \\%Systemroot%\\System32\\Drivers\\Etc 폴더에 저장됩니다.

사서함 서버에서 Edge 전송 서버의 이름을 확인하도록 하려면 다음 방법 중 하나를 사용합니다.

  - 사서함 서버에 구성된 DNS 서버의 정방향 조회 영역에서 Edge 전송 서버에 대한 리소스 레코드를 수동으로 만듭니다.

  - Edge 전송 서버의 호스트 레코드를 포함하려면 가입된 Active Directory 사이트에 있는 사서함 서버의 호스트 파일을 편집합니다.

Edge 전송 서버에 대한 DNS 설정을 구성하려면 다음 단계를 수행합니다.

1.  각 네트워크 인터페이스의 DNS 서버 설정이 네트워크 세그먼트에 대해 올바른지 확인합니다.

2.  다음 단계에 따라 Edge 전송 서버 이름에 대한 DNS 접미사를 구성합니다.
    
    1.  제어판을 열고 **시스템 속성**을 선택합니다.
    
    2.  **컴퓨터 이름** 탭을 선택합니다.
    
    3.  **변경**을 선택합니다.
    
    4.  **컴퓨터 이름 변경** 페이지에서 **자세히**를 클릭합니다.
    
    5.  **이 컴퓨터의 주 DNS 접미사** 필드에 Edge 전송 서버의 DNS 도메인 이름 및 접미사를 입력합니다.
    
    이 이름은 Edge 전송 서버 역할이 설치된 후 변경할 수 없습니다.

## DNS 설정 재정의

메일을 올바르게 라우팅하고 배달하려면 Exchange 서버에서 기본 DNS 설정을 재정의해야 할 수 있습니다. 이렇게 하려면 전송 서버 속성의 **내부 DNS 조회** 및 **외부 DNS 조회** 설정을 수정합니다. 이러한 설정은 전자 메일 메시지를 라우팅하기 위해 네트워크 어댑터의 설정을 무시합니다.


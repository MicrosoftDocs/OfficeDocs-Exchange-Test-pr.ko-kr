---
title: 'Outlook Web App에서 정보 권한 관리: Exchange 2013 Help'
TOCTitle: Outlook Web App에서 정보 권한 관리
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50483242
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App에서 정보 권한 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

정보 근로자가 전자 메일을 사용하여 중요한 정보를 교환하는 경우가 점점 더 늘어나고 있습니다. 이 정보를 안전하게 보호하려면 조직에서 IRM(정보 권한 관리)을 사용하여 메시징 콘텐츠에 영구 보호를 적용할 수 있습니다. Microsoft Exchange Server 2010 이전에는 IRM 보호의 효과적인 사용이 Outlook 클라이언트로 제한되어 있었습니다. Exchange Server 2007에서 Microsoft Outlook Web Access 사용자는 IRM 보호 콘텐츠를 액세스하려면 Microsoft Internet Explorer용 정보 권한 관리 추가 기능을 다운로드해야 했습니다.

Exchange 2013에서 Outlook Web App의 IRM을 사용하면 사용자가 Exchange에서 제공된 IRM 기능을 액세스하여 메시징 콘텐츠에 영구 IRM 보호를 적용할 수 있습니다.

다음 IRM 기능은 Outlook Web App에서 사용할 수 있습니다.

  - **IRM으로 보호된 메시지 보내기**   다음 그림과 같이 Outlook Web App 사용자는 권한 드롭다운 목록을 사용하고 메시지에 적용할 권한 정책 템플릿을 선택할 수 있습니다. 이를 통해 IRM으로 보호된 메시지를 Outlook Web App 내에서 보낼 수 있습니다. 메시지는 클라이언트 액세스 서버가 IRM으로 보호합니다.
    
    ![OWA에서 IRM으로 보호된 메시지 보내기](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "OWA에서 IRM으로 보호된 메시지 보내기")  

  - **IRM 보호 첨부 파일**   사용자가 Outlook Web App에서 IRM으로 보호된 메시지를 보내는 경우 메시지에 첨부된 모든 파일이 동일한 IRM 보호를 받을 수 있고 메시지로 동일한 권한 정책 템플릿을 사용하여 보호됩니다. Exchange 2013에서 IRM 보호는 .xps 파일 및 전자 메일 메시지뿐만 아니라 Microsoft Office Word, Excel 및 PowerPoint에 연결된 파일에 적용됩니다. IRM 보호는 IRM으로 보호되고 있지 않은 첨부 파일에만 적용됩니다. Active Directory AD RMS(Rights Management Services) 권한 정책 템플릿에 대한 자세한 내용은 [정보 권한 관리](information-rights-management-exchange-2013-help.md) 항목을 참조하십시오.
    

    > [!NOTE]
    > Outlook Web App의 IRM은 이 섹션의 지원되는 파일의 첨부 파일만 보호합니다. 지원되지 않는 파일 형식을 사용하는 첨부 파일은 보호되지 않습니다. Outlook Web App 사용자가 메시지를 보호하고 지원되지 않는 형식의 파일을 첨부하는 경우 지원되는 파일 형식만 보호된다고 사용에게 알려주는 알림이 표시됩니다.

    

    > [!IMPORTANT]
    > IRM 보호는 S/MIME을 사용하여 암호화되거나 이미 서명된 메시지에 적용할 수 없습니다. IRM 보호를 적용하려면 S/MIME 서명 및 암호화를 메시지에서 제거해야 합니다. IRM으로 보호된 메시지에도 동일하게 적용됩니다. 사용자는 S/MIME을 사용하여 메시지를 암호화하거나 서명할 수 없습니다.



  - **IRM으로 보호된 메시지 읽기**   조직의 AD RMS 클러스터를 사용하여 보낸 사람이 보호한 메시지는 Outlook Web App의 미리 보기 창에서 렌더링됩니다. 추가 기능을 설치할 필요가 없으며 컴퓨터를 AD RMS 배포에서 등록할 필요가 없습니다. 사용자가 메시지를 열거나 미리 보기 창에서 보는 경우 메시지는 이전 라이선스 에이전트가 추가한 사용 라이선스를 사용하여 암호화됩니다. 암호 해독 후 미리 보기 창에서 메시지가 표시됩니다. 이전 라이선스를 사용할 수 없는 경우 Outlook Web App는 AD RMS 서버에서 이전 라이선스를 요청한 다음 메시지를 렌더링합니다. Outlook Web App의 IRM 보호 첨부 파일을 읽을 때 Web-Ready 문서 보기를 사용할 수 없습니다.
    

    > [!NOTE]
    > Outlook Web App의 IRM은 사용자가 Outlook 및 다른 Office 응용 프로그램이 수행하는 방식으로 Print Screen 기능을 사용하여 화면을 캡처하지 못하게 합니다. 이는 AD&nbsp;RMS 권한 정책 템플릿에 지정되지 않은 경우 메시지 콘텐츠를 복사할 수 없게 하는 EXTRACT 권한에 영향을 줍니다.



  - **크로스 브라우저, 여러 플랫폼 IRM 지원**   Outlook Web App 에서 IRM 크로스 브라우저, IRM 지원 되는 여러 플랫폼을 제공 합니다. Outlook Web App 에서 IRM Exchange 2013, Apple Macintosh 및 Linux 운영 체제에 포함 하 여 사용할 수 있는 모든 브라우저에서 지원 됩니다. 지원 되는 브라우저 및 운영 체제에 대 한 자세한 내용은, [Outlook Web App 지원 되는 브라우저](https://go.microsoft.com/fwlink/p/?linkid=129362)를 참조 하십시오.

  - **WebReady 문서 보기**   Exchange 2013에서 WebReady 문서 보기를 사용하여 사용자는 지원되는 IRM 보호 첨부 파일을 볼 수 있습니다. 이를 통해 첨부 파일 관련 응용 프로그램을 다운로드하지 않고 지원되는 첨부 파일을 확인할 수 있습니다.

IRM 관리와 관련된 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

## Outlook Web App에서 IRM 사용

Outlook Web App에서 IRM을 사용하도록 설정하려면 페더레이션 사서함(Exchange 2013 설치에서 만든 시스템 사서함)을 AD RMS의 Super Users 그룹에 추가해야 합니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조하십시오. 이를 통해 Exchange 2013 서버는 IRM으로 보호된 메시지에 액세스할 수 있습니다.

또한 Outlook Web App 관리 셸의 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) cmdlet을 사용하여 Exchange의 IRM도 사용 가능하도록 설정할 수 있습니다. 그러면 Outlook Web App 조직의 Exchange 2013에서 IRM을 사용하도록 설정합니다. Outlook Web App 가상 디렉터리의 Outlook Web App에서 IRM 사용하거나 사용하지 않도록 설정할 수 있습니다. 다음과 같은 세부적인 수준에서 Outlook Web App의 IRM을 제어할 수도 있습니다.

  - **Outlook Web App 가상 디렉터리별**   Outlook Web App 가상 디렉터리에 대해 Outlook Web App의 IRM을 사용하거나 사용하지 않도록 설정하려면 **Set-OWAVirtualDirectory** cmdlet을 사용하고 *IRMEnabled* 매개 변수를 `$false` 또는 `$true`(기본값)로 설정합니다. 그러면 Exchange 2013 클라이언트 액세스 서버에 있는 가상 디렉터리 하나에 대해서는 Outlook Web App의 IRM을 사용하지 않도록 설정하고, 다른 클라이언트 액세스 서버의 다른 가상 디렉터리에 대해서는 사용하도록 설정할 수 있습니다.

  - **Outlook Web App 사서함 정책별**   Outlook Web App 사서함 정책에 대해 Outlook Web App의 IRM을 사용하거나 사용하지 않도록 설정하려면 **Set-OWAMailboxPolicy** cmdlet을 사용하고 *IRMEnabled* 매개 변수를 `$false` 또는 `$true`(기본값)로 설정합니다. 그러면 한 사용자 집합에 대해서는 Outlook Web App의 IRM을 사용하도록 설정하고, 다른 사용자 집합에 대해서는 다른 Outlook Web App 사서함 정책을 할당하여 사용하지 않도록 설정할 수 있습니다.

자세한 내용은 [클라이언트 액세스 서버에서 정보 권한 관리를 사용 하지 않도록 설정 하거나 사용](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)를 참조하십시오.


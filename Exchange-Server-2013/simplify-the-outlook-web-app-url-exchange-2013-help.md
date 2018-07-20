---
title: 'Outlook Web App URL 단순화: Exchange 2013 Help'
TOCTitle: Outlook Web App URL 단순화
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54651821
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App URL 단순화

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-07-16_

**요약:**  이 문서의 절차를 사용하여 조직의 사용자가 Exchange 2013에서 OWA에 액세스하는 URL을 단순화합니다.

사용자가 Exchange Server 2013 사서함에 액세스하는 데 사용하는 MicrosoftOutlook Web App URL을 단순화할 수 있습니다.

사용자의 Outlook Web App 액세스를 단순화하기 위해 사용자를 https로 자동 리디렉션하도록 일반적으로 IIS에서 기본 웹 사이트인 Outlook Web App 웹 페이지를 구성할 수 있습니다. "IIS 관리자를 사용하여 Outlook Web Access URL을 단순화하고 SSL로 강제 리디렉션" 섹션의 절차는 http://*server*에 대한 요청을 https://*server*/owa로 리디렉션합니다. 클라이언트와 서버 간에 전송되는 정보의 보안 유지를 위해 기본 웹 사이트는 설치 시 SSL(Secure Sockets Layer)이 필요하도록 설정됩니다.

Windows Server 2008의 최상위 디렉터리에서 리디렉션을 구성하면 설정이 하위 디렉터리로 전파됩니다. 예를 들어 기본 웹 사이트에서 /owa 가상 디렉터리에 대한 리디렉션을 구성하면 구성하는 설정이 /Autodiscover, /Exchange 및 /Public 등의 모든 가상 디렉터리의 HTTP 리디렉션 페이지에도 표시됩니다. 따라서 리디렉션할 가상 디렉터리를 제외한 모든 가상 디렉터리에서 리디렉션을 제거해야 합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 Outlook Web App 사용 권한 섹션에 있는 "IIS 관리자" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 1단계: IIS 관리자를 사용하여 Outlook Web Access URL을 단순화하고 SSL로 강제 리디렉션

1.  IIS 관리자를 시작합니다.

2.  로컬 컴퓨터를 확장하고 **사이트**를 확장한 다음 **기본 웹 사이트**를 클릭합니다.

3.  기본 웹 사이트 홈 창 아래쪽에서 **기능 보기** 옵션이 아직 선택되어 있지 않은 경우 이를 클릭합니다.

4.  **IIS** 섹션에서 **HTTP 리디렉션**을 두 번 클릭합니다.

5.  **요청을 이 대상으로 리디렉션** 확인란을 선택합니다.

6.  /owa 가상 디렉터리의 절대 경로를 입력합니다. 예를 들어 **https://mail.contoso.com/owa**를 입력합니다.

7.  **동작 리디렉션** 아래에서 **요청을 이 디렉터리(하위 디렉터리 제외)의 콘텐츠로만 리디렉션** 확인란을 선택합니다.

8.  **상태 코드** 목록에서 **찾음(302)**을 클릭합니다.

9.  작업 창에서 **적용**을 클릭합니다.

10. **기본 웹 사이트**를 클릭합니다.

11. 기본 웹 사이트 홈 창에서 **SSL 설정**을 두 번 클릭합니다.

12. **SSL 설정**에서 **SSL 필요**의 선택을 취소합니다.
    

    > [!NOTE]
    > <STRONG>SSL 필요</STRONG>의 선택을 취소하지 않으면 사용자가 보안되지 않은 URL을 입력했을 때 사용자에게 리디렉션되지 않습니다. 대신 액세스 거부 오류 메시지가 표시됩니다.



## 2단계: 가상 디렉터리에서 리디렉션 제거

가상 디렉터리에서 리디렉션을 제거하려면 다음 단계를 수행합니다.

1.  명령 프롬프트 창을 엽니다.

2.  \<*Window directory*\>\\System32\\Inetsrv로 이동합니다.

3.  다음 명령을 실행합니다.
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  `iisreset/noforce` 명령을 실행하여 완료합니다.

최상위 디렉터리에서 리디렉션을 구성하면 web.config 파일이 \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab에 만들어질 수 있습니다. 이 경우 나중에 리디렉션을 제거하면 **보내기 및 받기**를 클릭했을 때 Outlook이 작동하지 않을 수 있습니다. 리디렉션 제거 후에 이 문제가 발생하지 않도록 하려면 \<*drive*\>\\Program Files\\Microsoft\\Exchange Server\\\<*version*\>\\ClientAccess\\oab에서 web.config 파일을 삭제합니다.

## 작동 여부는 어떻게 확인합니까?

Outlook Web App URL이 단순화되고 SSL 연결로 리디렉션되었는지 확인하려면 다음을 수행합니다.

1.  웹 브라우저를 열고 Outlook Web App의 새 URL을 입력합니다(http://\<*URL*\> 형식).

2.  SSL 연결을 통해 Outlook Web App 로그인 페이지로 리디렉션됩니다.


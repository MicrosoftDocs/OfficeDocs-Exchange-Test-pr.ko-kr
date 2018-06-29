---
title: '복제 된 구성을 사용 하 여 Edge 전송 서버 구성: Exchange 2013 Help'
TOCTitle: 복제 된 구성을 사용 하 여 Edge 전송 서버 구성
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61183417
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 복제 된 구성을 사용 하 여 Edge 전송 서버 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-13_

%ExchangeInstallPath%Scripts에 위치한 제공된 Exchange 관리 셸 스크립트를 사용하여 Edge 전송 서버의 구성을 복제할 수 있습니다. 이러한 프로세스를 *복제된 구성*이라고 합니다. *복제된 구성*은 이전에 구성한 원본 서버의 구성 정보에 기반하여 새 Edge 전송 서버를 배포하는 기능입니다. 이전에 구성한 원본 서버의 구성 정보는 복사되어 XML 파일로 내보낸 후 대상 서버로 가져옵니다. 이 프로세스의 개요는 [Edge 전송 서버 복제 된 구성](edge-transport-server-cloned-configuration-exchange-2013-help.md)를 참조하세요.

Edge 전송 서버 구성 정보는 AD LDS(Active Directory Lightweight Directory Services)에 저장되며 여러 Edge 전송 서버 간에 복제되지 않습니다. 복제된 구성을 사용하면 경계 네트워크에서 배포되는 모든 Edge 전송 서버가 같은 구성을 사용하도록 할 수 있습니다.

복제된 구성 작업을 수행할 때는 다음의 두 셸 스크립트를 사용합니다.

  - **ExportEdgeConfig.ps1**   Edge 전송 서버의 모든 사용자 구성 설정 및 데이터를 내보낸 다음 XML 파일에 저장합니다.

  - **ImportEdgeConfig.ps1**   구성 유효성 검사 단계에서 내보낸 XML 파일을 검사하여 서버별 내보내기 설정이 대상 서버에 유효한지 확인합니다. 설정을 수정해야 하는 경우 이 스크립트는 대상 서버 정보를 지정하기 위해 수정할 수 있는 응답 파일에 잘못된 설정을 씁니다. 이 응답 파일은 구성 가져오기 단계에서 사용됩니다. 구성 가져오기 단계에서 이 스크립트는 ExportEdgeConfig.ps1 스크립트로 만든 중개용 XML 파일에 저장된 모든 사용자 구성 설정과 데이터를 가져옵니다.

두 스크립트는 모두 %ExchangeInstallPath%Scripts 폴더에 있습니다.

## 시작하기 전에

  - 이 작업의 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "Edge 전송 서버" 항목

  - 복제된 구성에서는 서버의 Edge 구독 설정을 복제하지 않습니다. EdgeSync 인증서도 복제되지 않습니다. 각 Edge 전송 서버마다 EdgeSync 프로세스를 별도로 실행해야 합니다. EdgeSync에서는 복제된 구성 정보와 EdgeSync 복제 정보에 포함된 모든 설정을 덮어씁니다.

  - 모든 송신 커넥터가 자격 증명을 사용하도록 구성되어 있으면 암호가 중간 XML 파일에 암호화된 문자열로 기록됩니다. ImportEdgeConfig.ps1 및 ExportEdgeConfig.ps1 스크립트에 *-key* 매개 변수를 사용하여 암호화 및 암호 해독에 사용할 32바이트 문자열을 지정할 수 있습니다. *-key* 매개 변수를 사용하지 않으면 기본 암호화 키가 사용됩니다.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 원본 서버의 파일로 원본 서버 구성 데이터 내보내기

1.  ExportEdgeConfig.ps1 스크립트를 원본 서버에 있는 사용자 프로필의 루트 폴더에 복사합니다.

2.  원본 서버에 있는 파일로 원본 서버 구성 데이터를 내보내려면 다음 구문을 사용합니다.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    예를 들어 원본 서버 구성 데이터를 C:\\CloneConfigData.xml 파일로 내보내려면 다음 명령을 실행합니다.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## 이 단계의 작동 여부는 어떻게 확인합니까?

"Edge 구성 데이터를 \<출력 파일 경로\>(으)로 내보냈습니다."라는 확인 메시지가 표시되면 원본 구성 데이터를 파일로 올바르게 내보낸 것입니다.

## 2단계: 구성 파일의 유효성을 검사하고 대상 서버에 응답 파일 만들기

1.  이전 단계에서 내보낸 원본 서버 구성 파일을 대상 Edge 전송 서버에 복사합니다.

2.  ImportEdgeConfig.ps1 스크립트를 대상 서버에 있는 사용자 프로필의 루트 폴더에 복사합니다.

3.  구성 파일의 유효성을 검사하고 결과를 사용하여 대상 서버에 응답 파일을 만들려면 다음 구문을 사용합니다.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    예를 들어 C:\\CloneConfigData.xml 구성 파일의 유효성을 검사하고 C:\\CloneConfigAnswer.xml 응답 파일을 만들려면 다음 명령을 실행합니다.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  응답 파일을 열어 대상 서버에 대해 잘못된 설정을 수정합니다. 응답 파일에 수정할 내용이 없으면 입력할 필요가 없습니다. 변경 내용을 저장합니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

"응답 파일을 만들었습니다."라는 확인 메시지가 표시되면 구성 파일의 유효성이 검사되고 응답 파일이 만들어진 것입니다.

## 3단계: 대상 서버에서 구성 파일 가져오기

대상 서버에서 구성 파일을 가져오려면 다음 구문을 사용합니다.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

예를 들어 C:\\CloneConfigAnswer.xml 응답 파일을 사용하여 C:\\CloneConfigData.xml 구성 파일을 가져오려면 다음 구문을 실행합니다.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## 이 단계의 작동 여부는 어떻게 확인합니까?

"Edge 구성 파일 정보를 가져왔습니다."라는 확인 메시지가 표시되면 대상 서버에서 구성 파일을 가져온 것입니다.


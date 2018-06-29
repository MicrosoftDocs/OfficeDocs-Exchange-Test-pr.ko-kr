---
title: '명령 출력 (영문): Exchange 2013 Help'
TOCTitle: 명령 출력 (영문)
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50483555
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 명령 출력 (영문)

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Exchange 관리 셸에서는 명령 출력 형식을 지정하는 데 사용할 수 있는 여러 가지 방법을 제공합니다. 이 항목에서는 다음 주제에 대해 설명합니다.

  - How to format data **Format-List**, **Format-Table** 및 **Format-Wide** cmdlet을 사용하여 사용자가 보는 데이터의 형식을 지정하는 방법을 제어합니다.

  - How to output data **Out-Host** 및 **Out-File** cmdlet을 사용하여 데이터를 셸 콘솔 창으로 출력할지, 파일로 출력할지를 결정합니다. 이 항목에는 Microsoft Internet Explorer에 데이터를 출력하는 샘플 스크립트가 포함되어 있습니다.

  - How to filter data   다음 필터링 방법 중 하나를 사용하여 데이터를 필터링합니다.
    
      - 특정 cmdlet에서 사용할 수 있는 서버 쪽 필터링
    
      - 명령 결과를 **Where-Object** cmdlet으로 파이프하여 모든 cmdlet에서 사용할 수 있는 클라이언트 쪽 필터링

이 항목에서 설명하는 기능을 사용하려면 다음 개념을 잘 이해하고 있어야 합니다.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [셸 변수](https://technet.microsoft.com/ko-kr/library/bb124036\(v=exchg.150\))

  - [비교 연산자](https://technet.microsoft.com/ko-kr/library/bb125229\(v=exchg.150\))

## 데이터 형식을 지정하는 방법

파이프라인의 끝에서 형식 지정 cmdlet을 호출하는 경우 기본 형식 지정을 다시 정의하여 표시되는 데이터와 데이터가 표시되는 방식을 제어할 수 있습니다. 형식 지정 cmdlet은 **Format-List**, **Format-Table** 및 **Format-Wide**입니다. 각 cmdlet에는 다른 형식 지정 cmdlet과는 다른 고유한 개별 출력 스타일이 있습니다.

## Format-List

**Format-List** cmdlet은 파이프라인의 입력값을 사용하여 각 개체의 지정된 모든 속성을 수직 열 목록으로 출력합니다. *Property* 매개 변수를 사용하여 표시하려는 속성을 지정할 수 있습니다. 매개 변수를 지정하지 않고 **Format-List** cmdlet을 호출하면 모든 속성이 출력됩니다. **Format-List** cmdlet은 줄을 자르는 대신 줄 바꿈합니다. **Format-List** cmdlet을 사용하는 가장 좋은 방법 중 하나는 추가 정보 또는 보다 중요한 정보를 검색할 수 있도록 cmdlet의 기본 출력을 다시 정의하는 것입니다.

예를 들어 **Get-Mailbox** cmdlet을 호출하면 표 형식으로 제한된 양의 정보만 볼 수 있습니다. **Get-Mailbox** cmdlet 출력을 **Format-List** cmdlet으로 파이프하고 보려는 추가 정보 또는 보다 중요한 정보에 대한 매개 변수를 추가하면 원하는 출력을 검색할 수 있습니다.

또한 속성 이름의 일부분과 함께 와일드카드 문자 "\*"를 지정할 수 있습니다. 와일드카드 문자를 포함하는 경우 각 속성 이름을 개별적으로 입력하지 않고 일치하는 여러 속성을 검색할 수 있습니다. 예를 들어 `Get-Mailbox | Format-List -Property Email* `는 `Email`로 시작하는 모든 속성을 반환합니다.

다음 예는 **Get-Mailbox** cmdlet에서 반환하는 동일한 데이터를 볼 수 있는 다른 방법을 보여 줍니다.

    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited

첫 번째 예에서는 기본 출력이 표 형식으로 표시되고 미리 결정된 속성 집합이 포함되도록 특정 형식을 지정하지 않고 **Get-Mailbox** cmdlet을 호출합니다.

    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}

두 번째 예에서는 **Get-Mailbox** cmdlet 출력이 특정 속성과 함께 **Format-List** cmdlet으로 파이프됩니다. 보이는 것처럼 출력 형식과 내용이 크게 다릅니다.

    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True

마지막 예에서 **Get-Mailbox** cmdlet 출력은 두 번째 예에서와 같이 **Format-List** cmdlet으로 파이프됩니다. 그러나 마지막 예에서는 와일드카드 문자를 사용되어 `Email`로 시작하는 일치하는 모든 속성을 검색합니다.

두 개 이상의 개체가 **Format-List** cmdlet으로 전달되면 개체에 대해 지정된 모든 속성이 개체별로 그룹화되어 표시됩니다. 표시 순서는 cmdlet의 기본 매개 변수에 따라 다릅니다. 기본 매개 변수는 주로 *Name* 매개 변수 또는 *Identity* 매개 변수입니다. 예를 들어 **Get-Childitem** cmdlet을 호출하면 기본적으로 파일 이름이 사전순으로 표시됩니다. 이러한 동작을 변경하려면 **Format-List** cmdlet을*GroupBy* 매개 변수 및 출력 그룹화 기준인 속성 값 이름과 함께 호출해야 합니다. 예를 들어 다음 명령은 디렉터리의 모든 파일을 나열하고 확장명으로 그룹화합니다.

    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835

이 예에서 **Format-List** cmdlet은 *GroupBy* 매개 변수에서 지정한 *Extension* 속성으로 항목을 그룹화합니다. 파이프라인 스트림에 있는 개체의 유효한 모든 속성과 함께 *GroupBy* 매개 변수를 사용할 수 있습니다.

## Format-Table

**Format-Table** cmdlet을 사용하여 항목을 레이블 헤더 및 속성 데이터 열과 함께 테이블 형식으로 표시할 수 있습니다. 기본적으로 **Get-Process** 및 **Get-Service** cmdlet과 같은 여러 cmdlet은 테이블 형식으로 출력합니다. **Format-Table** cmdlet의 매개 변수에는 *Properties* 및 *GroupBy* 매개 변수가 포함됩니다. 이러한 매개 변수는 **Format-List** cmdlet에서 작동하는 것과 동일하게 작동합니다.

또한 **Format-Table** cmdlet은 *Wrap* 매개 변수를 사용합니다. 이 매개 변수를 사용하면 긴 줄의 속성 정보가 줄의 끝에서 잘리는 대신 완전히 표시됩니다. *Wrap* 매개 변수를 사용하여 반환되는 정보를 표시하는 방법에 대해 알아보려면 다음 두 예에서 **Get-Command** 명령 출력을 비교합니다.

첫 번째 예에서 **Get-Process** cmdlet에 대한 명령 정보를 표시하기 위해 **Get-Command** cmdlet을 사용하면 *Definition* 속성에 대한 정보가 잘립니다.

    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...

두 번째 예에서는 *Wrap* 매개 변수를 명령에 추가하여 *Definition* 속성의 전체 내용을 표시합니다.

    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]

또한 **Format-List** cmdlet과 같이 속성 이름의 일부분과 함께 와일드카드 문자 "`*`"를 지정할 수 있습니다. 와일드카드 문자를 포함하면 각 속성 이름을 개별적으로 입력하지 않고 일치하는 여러 속성을 검색할 수 있습니다.

## Format-Wide

**Format-Wide** cmdlet을 사용하면 다른 형식 cmdlet보다 더 간편하게 출력을 제어할 수 있습니다. 기본적으로 **Format-Wide** cmdlet은 출력 줄에 가능한 많은 속성 값 열을 표시하려고 합니다. 매개 변수를 추가하여 표시되는 열 수와 출력 공간 사용 방법을 제어할 수 있습니다.

대부분의 기본적인 사용에서 매개 변수를 지정하지 않고 **Format-Wide** cmdlet을 호출하면 페이지에 맞춰 열을 표시하도록 출력을 정렬합니다. 예를 들어 **Get-Childitem** cmdlet을 실행하여 출력을 **Format-Wide** cmdlet으로 파이프하면 정보가 다음과 같이 표시됩니다.

    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt

일반적으로 매개 변수를 지정하지 않고 **Get-Childitem** cmdlet을 호출하면 디렉터리의 모든 파일 이름이 속성 표로 표시됩니다. 이 예에서는 **Get-Childitem** cmdlet 출력을 **Format-Wide** cmdlet으로 파이프하여 출력이 두 개의 이름 열로 표시됩니다. **Format-Wide** cmdlet 다음에 오는 속성 이름에 의해 지정된 속성 유형이 한 번에 하나만 표시될 수 있습니다. *Autosize* 매개 변수를 추가하면 두 개의 열 표시에서 화면 너비에 맞춰 모든 열 표시로 출력이 변경됩니다.

    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt

이 예에서 표는 두 개의 열이 아니라 다섯 개의 열로 정렬됩니다. *Column* 매개 변수를 사용하면 다음과 같이 최대 열 수를 지정하여 정보를 표시하므로 보다 강력하게 출력을 제어할 수 있습니다.

    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt

이 예에서는 *Column* 매개 변수를 사용하여 열 수를 네 개로 지정했습니다.

## 데이터를 출력하는 방법

## Out-Host 및 Out-File cmdlet

**Out-Host** cmdlet은 파이프라인의 끝에 나타나지 않는 기본 cmdlet입니다. 모든 형식 지정 적용되면 **Out-Host** cmdlet은 최종 출력을 콘솔 창으로 보내 표시합니다. **Out-Host** cmdlet은 기본 출력이므로 명시적으로 호출할 필요가 없습니다. 명령의 마지막 cmdlet으로 **Out-File** cmdlet을 호출하여 콘솔 창으로 출력 보내기를 다시 정의할 수 있습니다. 그러면 다음 예에서와 같이 **Out-File** cmdlet은 명령에서 지정한 파일에 출력을 씁니다.

    Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt

이 예에서 **Out-File** cmdlet은 **Get-ChildItem | Format-Wide -Column 4** 명령으로 표시되는 정보를 `OutputFile.txt`라는 파일에 씁니다. 또한 리디렉션 연산자인 오른쪽 꺾쇠 괄호(`>`)를 사용하여 파이프라인 출력을 파일로 리디렉션할 수 있습니다. 원본 파일을 바꾸지 않고 명령의 파이프라인 출력을 기존 파일에 추가하려면 다음 예에서와 같이 오른쪽 이중 꺾쇠 괄호(`>>`)를 사용합니다.

    Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt

이 예에서는 형식 지정을 위해 **Get-Childitem** cmdlet의 출력을 **Format-Wide** cmdlet으로 파이프한 다음 `OutputFile.txt` 파일의 끝에 씁니다. `OutputFile.txt` 파일이 없는 경우 오른쪽 이중 꺾쇠 괄호(`>>`)를 사용하여 파일을 만듭니다.

파이프라인에 대한 자세한 내용은 [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))을 참조하십시오.

이전 예에서 사용한 구문에 대한 자세한 내용은 [구문](https://technet.microsoft.com/ko-kr/library/bb123552\(v=exchg.150\))을 참조하십시오.

## Internet Explorer에서 데이터 보기

Exchange 관리 셸에서의 스크립팅 유연성과 용이성으로 인해 명령에서 반환하는 데이터를 사용하여 형식을 지정하고 자유로운 방식으로 출력할 수 있습니다.

다음 예에서는 간단한 스크립트를 사용하여 명령에서 반환하는 데이터를 출력하고 Internet Explorer에 표시하는 방법을 보여 줍니다. 이 스크립트는 파이프라인을 통과하는 개체를 사용하여 Internet Explorer 창을 연 다음 Internet Explorer에 데이터를 표시합니다.

    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write(\"$Input\")
    $Ie

이 스크립트를 사용하려면 스크립트가 실행될 컴퓨터의 `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` 디렉터리에 스크립트를 저장합니다. 파일 이름을 `Out-Ie.ps1`이라고 지정합니다. 파일을 저장한 다음 일반 cmdlet으로 스크립트를 사용할 수 있습니다.


> [!NOTE]
> Exchange 2013에서 스크립트를 실행하려면 범위가 지정되지 않은 관리 역할에 스크립트를 추가해야 하며, 직접 또는 관리 역할 그룹을 통해 관리 역할을 할당받아야 합니다. 자세한 내용은 <A href="understanding-management-roles-exchange-2013-help.md">관리 역할 이해 (영문)</A>를 참조하십시오.



`Out-Ie` 스크립트는 받은 데이터가 올바른 HTML임을 가정합니다. HTML로 보려는 데이터를 변환하려면 명령 결과를 **ConvertTo-Html** cmdlet으로 파이프해야 합니다. 그런 다음 명령 결과를 `Out-Ie` 스크립트로 파이프할 수 있습니다. 다음 예는 Internet Explorer 창에서 디렉터리 목록을 보는 방법을 보여 줍니다.

    Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie

## 데이터를 필터링하는 방법

셸을 사용하면 서버, 사서함, Active Directory 및 조직의 기타 개체에 대한 대량의 정보에 액세스할 수 있습니다. 이러한 정보에 액세스하면 사용자 환경에 대한 이해를 높일 수 있지만 지나치게 많은 정보가 부담이 될 수 있습니다. 셸을 사용하면 이러한 정보를 제어하고 필터링을 통해 보려는 데이터만 반환할 수 있습니다. 다음 두 가지 유형의 필터링을 사용할 수 있습니다.

  - **서버 쪽 필터링**   서버 쪽 필터링은 명령줄에서 지정한 필터를 사용하여 쿼리한 Exchange 서버에 해당 필터를 전송합니다. 해당 서버에서 쿼리를 처리하고 지정한 필터와 일치하는 데이터만 반환합니다.
    
    수십만 또는 수만 개의 결과를 반환할 수 있는 개체에 대해서만 서버 쪽 필터링을 수행합니다. 따라서 **Get-Mailbox** cmdlet과 같은 받는 사람 관리 cmdlet과 **Get-Queue** cmdlet과 같은 큐 관리 cmdlet에서만 서버 쪽 필터링을 지원합니다. 이러한 cmdlet은 *Filter* 매개 변수를 지원합니다. 이 매개 변수는 사용자가 지정한 필터 식을 가져와서 처리를 위해 서버로 전송합니다.

  - **클라이언트 쪽 필터링**   클라이언트 쪽 필터링은 현재 작업하고 있는 로컬 콘솔 창에 있는 개체에 대해 수행됩니다. 클라이언트 쪽 필터링을 사용하면 cmdlet은 로컬 콘솔 창에 대해 수행 중인 작업과 일치하는 모든 개체를 검색합니다. 그러면 셸은 반환되는 모든 결과에 클라이언트 쪽 필터링을 적용하여 필터와 일치하는 결과만 반환합니다. 모든 cmdlet이 클라이언트 쪽 필터링을 지원합니다. 명령 결과를 **Where-Object** cmdlet으로 파이프하여 클라이언트 쪽 필터링을 호출합니다.

## 서버 쪽 필터링

서버 쪽 필터링 구현은 서버 쪽 필터링이 지원되는 cmdlet에 따라 다릅니다. 서버 쪽 필터링은 반환된 개체의 특정 속성에 대해서만 사용하도록 설정됩니다. 자세한 내용은 다음 cmdlet에 대한 도움말을 참조하십시오.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## 클라이언트 쪽 필터링

클라이언트 쪽 필터링에는 어떤 cmdlet도 사용할 수 있습니다. 또한 이 기능에는 서버 쪽 필터링을 지원하는 cmdlet도 포함됩니다. 이 항목의 앞부분에서 설명한 것처럼 클라이언트 쪽 필터링은 파이프라인의 이전 명령에서 반환한 모든 데이터를 수락하고 지정한 필터와 일치하는 결과만 반환합니다. **Where-Object** cmdlet은 이 필터링을 수행하며 **Where**라고 줄여 쓸 수 있습니다.

데이터가 파이프라인을 통과하면 **Where** cmdlet이 이전 개체에서 데이터를 받아 다음 개체로 전달하기 전에 해당 데이터를 필터링합니다. 필터링은 **Where** 명령에서 정의한 스크립트 블록에 따라 다릅니다. 스크립트 블록은 개체의 속성 및 값에 따라 데이터를 필터링합니다.

**Clear-Host** cmdlet은 콘솔 창을 지우는 데 사용됩니다. 예를 들어 다음 명령을 실행하면 **Clear-Host** cmdlet에 대해 정의된 모든 별칭을 찾을 수 있습니다.

    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host

**Get-Alias** cmdlet과 **Where** 명령은 함께 작동하여 **Clear-Host** cmdlet에 대해 정의된 별칭 목록을 반환합니다. 다른 cmdlet에 대해 정의된 별칭 목록은 반환하지 않습니다. 다음 표에서는 예에서 사용된 **Where** 명령의 각 요소에 대해 간단하게 설명합니다.

### Where 명령 요소

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>요소</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>필터를 정의하는 스크립트 블록을 묶는 중괄호입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>이 특수한 변수는 자동으로 시작되어 파이프라인의 개체에 바인딩됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p><code>Definition</code> 속성은 별칭 정의 이름을 저장하는 현재 파이프라인 개체의 속성입니다. <code>$_</code> 변수와 함께 <code>Definition</code>을 사용하면 속성 이름 앞에 마침표가 옵니다.</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>이 &quot;같음&quot; 비교 연산자는 결과가 식에서 제공된 속성 값과 정확하게 일치해야 함을 지정하는 데 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>이 예에서 &quot;<strong>Clear-Host</strong>&quot;는 명령이 구문 분석하는 값입니다.</p></td>
</tr>
</tbody>
</table>


위의 예에서 **Get-Alias** cmdlet에서 반환하는 개체는 시스템에 있는 정의된 모든 별칭을 나타냅니다. 이러한 개체를 명령줄에서 확인할 수 없지만 별칭은 파이프라인을 통해 수집되어 **Where** cmdlet으로 전달됩니다. **Where** cmdlet은 스크립트 블록의 정보를 사용하여 별칭 개체에 필터를 적용합니다.

특수한 변수 `$`\_는 전달되는 개체를 나타냅니다. `$_` 변수는 셸에서 자동으로 시작되며 현재 파이프라인 개체에 바인딩됩니다. 이 특수한 변수에 대한 자세한 내용은 [셸 변수](https://technet.microsoft.com/ko-kr/library/bb124036\(v=exchg.150\))를 참조하십시오.

표준 "점" 표기법(object.property)을 사용하여 평가할 개체의 정확한 속성을 정의하도록 `Definition` 속성이 추가됩니다. 그런 다음 `-eq` 비교 연산자가 이 속성 값을 `"Clear-Host"`와 비교합니다. 이 기준과 일치하는 `Definition` 속성을 가진 개체만 콘솔 창으로 전달되어 출력됩니다. 비교 연산자에 대한 자세한 내용은 [비교 연산자](https://technet.microsoft.com/ko-kr/library/bb125229\(v=exchg.150\))를 참조하십시오.

**Where** 명령을 통해 **Get-Alias** cmdlet에서 반환된 개체를 필터링하고 나면 필터링된 개체를 다른 명령에 파이프할 수 있습니다. 다음 명령에서는 Where 명령에서 반환되어 필터링된 개체만 처리합니다.


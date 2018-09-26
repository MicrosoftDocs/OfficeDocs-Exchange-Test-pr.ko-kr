---
title: 'Exchange 관리 셸에서 파일 가져오기 및 내보내기: Exchange 2013 Help'
TOCTitle: Exchange 관리 셸에서 파일 가져오기 및 내보내기
ms:assetid: b4b669e8-a3aa-4b0b-ad34-f1f15d9c9369
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638170(v=EXCHG.150)
ms:contentKeyID: 50556069
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 관리 셸에서 파일 가져오기 및 내보내기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013에서는 Windows PowerShell 명령줄 인터페이스 원격 기능을 사용하여 Exchange를 관리 중인 서버 또는 워크스테이션과 관리 중인 Exchange 2013을 실행하는 서버 간에 연결을 설정합니다. Exchange 2013에서는 이를 원격 Exchange 관리 셸 또는 원격 셸이라고 합니다. 로컬 Exchange 2013 서버를 관리하는 중인 경우에도 연결을 설정하기 위해 원격 셸이 사용됩니다. 로컬 및 원격 셸에 대한 자세한 내용은 [PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))를 참조하십시오.

Exchange 2013의 경우 Exchange 서버에서 파일을 가져오고 Exchange 서버로 파일을 내보내는 방법이 Exchange Server 2007과는 다릅니다. Exchange 2013에서는 원격 셸을 사용하기 때문입니다. 이 항목에서는 이 새 프로세스가 필요한 이유와 로컬 서버 또는 워크스테이션과 Exchange 2013 서버 간에 파일을 가져오고 내보내는 방법에 대해 설명합니다.

## Windows PowerShell 세션

원격 셸에서 파일을 가져오고 내보내기 위해 특수한 구문이 필요한 이유를 이해하려면 Exchange 2013에서 셸이 구현되는 방법을 알아야 합니다. 셸은 변수, cmdlet 등이 정보를 공유할 수 있는 환경인 Windows PowerShell 세션을 사용합니다. 새 셸 창을 열 때마다 새 세션을 만듭니다. 각 창에서 실행되는 cmdlet은 해당 창에 저장된 변수 및 기타 정보에 액세스할 수 있지만 열려 있는 다른 셸 창의 변수에는 액세스할 수 없습니다. 이는 각각 고유한 Windows PowerShell 세션 내에 포함되어 있기 때문입니다. Windows PowerShell 세션을 또한 runspace라고도 합니다.

Exchange 2013의 원격 셸은 두 개의 세션인 로컬 세션 및 원격 세션을 가집니다. 로컬 세션은 로컬 컴퓨터에서 실행 중인 Windows PowerShell 세션입니다. 이 세션은 Windows PowerShell과 함께 제공되는 모든 cmdlet을 포함합니다. 또한 로컬 파일 시스템에 액세스할 수 있습니다.

원격 세션은 원격 Windows 서버에서 실행 중인 Exchange PowerShell 세션입니다. 이 세션은 모든 Exchange cmdlet이 실행되는 위치입니다. Exchange 서버의 파일 시스템에 액세스할 수 있습니다.

원격 Exchange 서버에 연결할 경우 사용자 컴퓨터의 로컬 세션과 Exchange 서버의 원격 세션 간에 연결이 설정됩니다. 이 연결을 사용하면 로컬 컴퓨터에 Exchange cmdlet이 전혀 설치되지 않은 경우에도 로컬 세션의 원격 Exchange 서버에서 Exchange cmdlet을 실행할 수 있습니다. Exchange cmdlet이 로컬 컴퓨터에서 실행되는 것처럼 보이더라도 실제로는 Exchange 서버에서 실행됩니다.


> [!IMPORTANT]
> Exchange 2013&nbsp;서버에서 셸을 열 경우에도 동일한 연결 프로세스가 발생하고 두 개의 세션이 만들어집니다. 이는 셸을 Exchange 2013 서버에서 여는지 아니면 원격 클라이언트 워크스테이션에서 여는지 여부에 상관없이 동일한 새 구문을 사용하여 파일을 가져오고 내보내야 한다는 것을 의미합니다.



원격 Exchange 서버의 원격 세션에서 실행되는 Exchange cmdlet은 로컬 파일 시스템에 액세스할 수 없습니다. 이는 Exchange cmdlet을 단독으로 사용하여 파일을 로컬 파일 시스템에서 가져오거나 로컬 파일 시스템으로 내보낼 수 없다는 것을 의미합니다. 원격 Exchange 서버에서 실행되는 Exchange cmdlet이 데이터를 사용할 수 있도록 로컬 파일 시스템에서 또는 로컬 파일 시스템으로 파일을 전송하는 데 추가 구문을 사용해야 합니다. 필요한 구문에 대한 자세한 내용은 이 항목 뒷부분의 "원격 셸에서 파일 가져오기 및 내보내기"를 참조하십시오.

## 원격 셸에서 파일 가져오기 및 내보내기

사서함 및 클라이언트 액세스 서버는 원격 셸을 사용하며 로컬 컴퓨터의 파일 시스템에 액세스할 수 없으므로 파일을 가져오고 내보내려면 특정 구문을 사용해야 합니다.

## 원격 셸에서 파일 가져오기

Exchange 2013에서 파일을 가져오기 위한 구문은 로컬 컴퓨터나 서버의 Exchange 2013 서버에서 실행되는 cmdlet에 파일을 보내려고 할 때마다 사용됩니다. 로컬 컴퓨터의 파일에서 데이터를 수락하는 cmdlet에는 *FileData* 또는 이와 비슷한 매개 변수가 사용됩니다. 사용할 올바른 매개 변수를 결정하려면 사용 중인 cmdlet에 대한 도움말 정보를 참조하십시오.

셸은 Exchange 2013 cmdlet에 보낼 파일과 데이터를 수락하는 매개 변수를 알아야 합니다. 이렇게 하려면 다음 구문을 사용합니다.

```powershell
<Cmdlet> -FileData ([Byte[]]$(Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0))
```

예를 들어 다음 명령은 가상의 **Import-SomeData** cmdlet에 있는 *FileData* 매개 변수에 C:\\MyData.dat 파일을 가져옵니다.

```powershell
Import-SomeData -FileData (Byte[]]$(Get-Content -Path "C:\MyData.dat" -Encoding Byte -ReadCount 0))
```

명령을 실행할 때 다음과 같은 작업이 수행됩니다.

1.  원격 셸은 명령을 수락합니다.

2.  원격 셸은 명령을 평가하고 *FileData* 매개 변수에 제공되는 값에 포함된 명령이 있는지 확인합니다.

3.  원격 셸은 **Import-SomeData** 명령의 평가를 중지하고 **Get-Content** 명령을 실행합니다. **Get-Content** 명령은 MyData.dat 파일에서 데이터를 읽습니다.

4.  원격 셸은 **Get-Content** 명령의 데이터를 일시적으로 `Byte[]` 개체로 저장하여 **Import-SomeData** cmdlet에 전달할 수 있게 합니다.

5.  **Import-SomeData** 명령 실행이 다시 시작됩니다. 원격 셸은 **Get-Content** cmdlet에 의해 만들어진 개체와 함께 **Import-SomeData** cmdlet을 실행하기 위한 요청을 원격 Exchange 2013 서버에 보냅니다.

6.  원격 Exchange 2013 서버에서 **Import-SomeData** cmdlet이 실행되고 **Get-Content** cmdlet에 의해 만들어진 임시 개체에 저장된 데이터가 *FileData* 매개 변수에 전달됩니다. **Import-SomeData** cmdlet은 입력을 처리하고 필요한 모든 작업을 수행합니다.

일부 cmdlet은 앞의 구문과 동일한 작업을 수행하는 다음 대체 구문을 사용합니다.

```powershell
[Byte[]]$Data = Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0
Import-SomeData -FileData $Data
```

이 대체 구문을 사용하여 동일한 프로세스가 발생합니다. 유일한 차이점은 전체 작업을 한 번에 수행하는 대신에 로컬 파일에서 검색된 데이터가 작성 후 참조할 수 있는 변수에 저장된다는 것입니다. 그런 다음 로컬 파일의 내용을 **Import-SomeData** cmdlet에 전달하기 위해 가져오기 명령에서 변수가 사용됩니다. 두 단계로 구성된 이 프로세스는 로컬 파일의 데이터를 둘 이상의 명령에서 사용하려는 경우에 유용합니다.

파일을 가져올 때 고려해야 할 제한 사항이 있습니다. 자세한 내용은 이 항목 뒷부분의 "파일 가져오기 제한"을 참조하십시오.

데이터를 Exchange 2013에 가져오는 방법에 대한 자세한 내용은 관리 중인 기능에 대한 도움말 항목을 참조하십시오.

## 파일 가져오기 제한

전송 중인 데이터의 무결성을 유지하기 위해 원격 셸에서 데이터를 가져올 때 제한을 설정해야 합니다. 진행 중인 전송은 중단될 경우 다시 시작할 수 없습니다. 또한 전송 중인 데이터가 원격 서버의 메모리에 저장되므로 너무 많은 데이터에 의해 야기되는 메모리 소모로부터 서버를 보호해야 합니다.

이러한 이유 때문에 로컬 컴퓨터 또는 서버에서 원격 Exchange 2013 서버에 전송되는 데이터 양은 다음으로 제한됩니다.

  - 실행되는 각 cmdlet의 경우 500MB

  - cmdlet에 전달되는 각 개체의 경우 75MB

이러한 제한 중 하나를 초과할 경우 cmdlet 및 연관된 파이프라인의 실행이 중지되고 오류가 발생합니다. 이러한 제한이 작동하는 방법을 이해하기 위해 다음 표의 예제를 가정해 봅니다.

### 가져오기 데이터 제한 예제

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>개체 수</th>
<th>개체 크기(MB)</th>
<th>총 크기(MB)</th>
<th>작업 결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10</p></td>
<td><p>40</p></td>
<td><p>400</p></td>
<td><p>개별 개체의 크기가 75MB를 초과하거나 cmdlet에 전달된 총 데이터 양이 500MB를 초과하지 않으므로 작업이 성공합니다.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>80</p></td>
<td><p>400</p></td>
<td><p>cmdlet에 전달된 총 데이터 양이 400MB에 불과하지만 각 개별 개체의 크기가 75MB 제한을 초과하므로 작업이 실패합니다.</p></td>
</tr>
<tr class="odd">
<td><p>120</p></td>
<td><p>5</p></td>
<td><p>600</p></td>
<td><p>각 개별 개체가 5MB에 불과하지만 cmdlet에 전달된 총 데이터 양이 500MB 제한을 초과하므로 작업이 실패합니다.</p></td>
</tr>
</tbody>
</table>


원격 Exchange 2013 서버 및 로컬 컴퓨터 간에 전송할 수 있는 데이터 양에 적용된 크기 제한으로 인해 가져오기를 지원했던 모든 cmdlet이 이 데이터 전송 방법을 지원하는 것은 아닙니다. 특정 cmdlet이 이 방법을 지원하는지 확인하려면 해당 cmdlet에 대한 도움말 정보를 참조하십시오.

이러한 제한은 Exchange 2013 서버에서 수행할 수 있는 대부분의 일반 작업을 수용해야 합니다. 제한이 낮아질 경우 일반 작업 중 일부는 새 제한을 초과하므로 실패할 수 있습니다. 제한이 높아질 경우 전송 중인 데이터를 전송하는 데 오래 걸리고 일시적으로 데이터 전송이 중단되는 상황에 처할 위험이 커질 수 있습니다. 또한 전송 도중 전체 데이터 블록을 서버에서 저장할 수 있도록 충분한 메모리를 설치하지 않은 경우 원격 서버에서 메모리가 소모될 수 있습니다. 이러한 각 가능성으로 인해 데이터가 손실될 수 있으므로 기본 제한을 변경하지 않는 것이 좋습니다.

## 원격 셸에서 파일 내보내기

Exchange 2013에서 파일을 내보내기 위한 구문은 원격 Exchange 2013 서버에서 실행되는 cmdlet에서 데이터를 수락하고 로컬 컴퓨터나 서버에 데이터를 저장하려고 할 때마다 사용됩니다. 로컬 파일에 저장할 수 있는 데이터를 제공하는 cmdlet은 **FileData** 또는 이와 비슷한 속성을 포함하는 개체를 출력합니다. cmdlet에 따라 **FileData** 속성은 특정 상황에서 출력되는 개체에서만 채워집니다. 사용할 올바른 속성 및 해당 속성을 사용할 수 있는 시점을 결정하려면 사용 중인 cmdlet에 대한 도움말 정보를 참조하십시오.

셸은 **FileData** 속성에 저장된 데이터를 로컬 컴퓨터에 저장하려고 한다는 것을 알아야 합니다. 이렇게 하려면 다음 구문을 사용합니다.

```command line
<cmdlet> | ForEach {     <cmdlet> | ForEach { $_.FileData | Add-Content <local path to file> -Encoding Byte }.FileData | Add-Content <local path to file> -Encoding Byte }
```

예를 들어 다음 명령은 가상의 **Export-SomeData** cmdlet에 의해 만들어진 개체의 **FileData** 속성에 저장된 데이터를 내보냅니다. 내보낸 데이터는 로컬 컴퓨터에 지정한 파일(이 경우에는 MyData.dat)에 저장됩니다.


> [!NOTE]
> 이 절차에서는 <STRONG>ForEach</STRONG> cmdlet, 개체 및 파이프라이닝을 사용합니다. 각각에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/aa998260(v=exchg.150)">파이프라이닝</A> 및 <A href="https://technet.microsoft.com/ko-kr/library/aa996386(v=exchg.150)">구조적 데이터</A> 항목을 참조하십시오.



```powershell
Export-SomeData | ForEach {     Export-SomeData | ForEach { $_.FileData | Add-Content C:\MyData.dat -Encoding Byte }.FileData | Add-Content C:\MyData.dat -Encoding Byte }
```

명령을 실행할 때 다음과 같은 작업이 수행됩니다.

1.  원격 셸은 명령을 수락합니다.

2.  원격 셸은 원격 Exchange 2013 서버에서 **Export-SomeData** cmdlet을 호출합니다.

3.  **Export-SomeData** cmdlet에 의해 만들어진 출력 개체는 파이프라인을 통해 다시 로컬 셸 세션으로 전달됩니다.

4.  그런 다음 출력 개체는 스크립트 블록을 가진 **ForEach** cmdlet에 파이프됩니다.

5.  스크립트 블록 내에서 파이프라인의 현재 개체에 있는 **FileData** 속성을 액세스합니다. **FileData** 속성에 포함된 데이터는 **Add-Content** cmdlet에 파이프됩니다.

6.  **Add-Content** cmdlet은 **FileData** 속성에서 파이프된 데이터를 로컬 파일 시스템의 MyData.dat 파일에 저장합니다.

Exchange 2013에서 데이터를 내보내는 방법에 대한 자세한 내용은 관리 중인 기능에 대한 도움말 항목을 참조하십시오.


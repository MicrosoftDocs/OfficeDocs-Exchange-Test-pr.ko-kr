---
title: '관리자 감사 로그 구조: Exchange 2013 Help'
TOCTitle: 관리자 감사 로그 구조
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50556026
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자 감사 로그 구조

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

관리자 감사 로그에는 Exchange 관리 셸과 EMC(Exchange 관리 콘솔)에서 실행된 모든 cmdlet 및 매개 변수의 레코드가 포함됩니다. EAC에서 관리자 감사 로그 보고서를 실행하거나 셸에서 **New-AdminAuditLogSearch** cmdlet을 실행하면 필요에 따라 로그가 만들어집니다. 감사 로그에 대한 자세한 내용은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)를 참조하십시오.

감사 로그는 XML 파일이며 여러 감사 로그 항목을 포함할 수 있습니다. 다음 표에서는 각 XML 태그와 관련 특성을 설명합니다.

관리자 감사 로그와 관련된 관리 작업은 [관리자가 관리 감사 로깅](manage-administrator-audit-logging-exchange-2013-help.md) 항목을 참조하십시오.

### 감사 로그 XML 태그 및 특성

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>요소</th>
<th>특성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>XML 문서 선언 태그입니다. 모든 감사 로그 XML 파일에 포함되며 XML 버전 번호와 문자 인코딩 값을 포함합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>이 태그는 XML 파일의 모든 감사 로그 항목을 포함합니다. <code>Event</code> 태그는 이 태그의 하위 태그입니다.</p>
<p>XML 파일당 <code>SearchResults</code> 태그는 하나만 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p></p></td>
<td><p>이 태그는 개별 cmdlet의 감사 로그 항목을 포함합니다. 즉, <code>Caller</code>, <code>Cmdlet</code>, <code>ObjectModified</code>, <code>RunDate</code>, <code>Succeeded</code>, <code>Error</code> 및 <code>OriginatingServer</code> 특성을 포함합니다. <code>CmdletParameters</code> 및 <code>ModifiedProperties</code> 태그는 이 태그의 하위 태그입니다.</p>
<p>감사 로그 항목당 하나의 <code>Event</code> 태그가 있습니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Caller</code></p></td>
<td><p>이 특성에는 <code>Cmdlet</code> 특성에서 cmdlet을 실행한 사용자의 사용자 계정이 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>이 특성에는 <code>Caller</code> 특성에서 사용자가 실행한 cmdlet의 이름이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>이 특성에는 <code>Cmdlet</code> 특성에 지정된 cmdlet에서 수정한 개체가 포함됩니다. <code>ModifiedProperties</code> 태그에는 이 개체에서 수정한 속성이 표시됩니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>이 특성에는 <code>Cmdlet</code> 특성에서 cmdlet을 실행한 날짜와 시간이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>이 특성은 <code>Cmdlet</code> 특성의 cmdlet이 성공적으로 실행되었는지 여부를 지정합니다. 값은 <code>True</code> 또는 <code>False</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Error</code></p></td>
<td><p><code>Cmdlet</code> 특성의 cmdlet이 성공적으로 완료되지 않은 경우 이 특성에는 오류 메시지가 포함됩니다. 오류가 발생하지 않은 경우 값이 <code>None</code>으로 설정됩니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>이 특성에는 <code>Cmdlet</code> 특성에 지정된 cmdlet을 실행한 서버가 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>이 태그에는 cmdlet을 실행할 때 지정된 매개 변수가 모두 포함됩니다. <code>Parameter</code> 태그는 이 태그의 하위 태그입니다.</p>
<p><code>Event</code> 태그당 하나의 <code>CmdletParameters</code> 태그가 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p></p></td>
<td><p>이 태그에는 cmdlet을 실행할 때 지정된 개별 매개 변수가 포함됩니다. 이 태그에는 <code>Name</code> 및 <code>Value</code> 특성이 포함됩니다.</p>
<p><code>CmdletParameters</code> 태그당 여러 <code>Parameter</code> 태그가 있을 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>이 특성에는 실행한 cmdlet에 지정된 매개 변수의 이름이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Value</code></p></td>
<td><p>이 특성에는 <code>Name</code> 특성에 지정된 매개 변수에서 제공하는 값이 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>이 태그에는 실행된 cmdlet에 의해 수정된 모든 속성이 포함됩니다. <code>Property</code> 태그는 이 태그의 하위 태그입니다.</p>
<p><code>Event</code> 태그당 하나의 <code>ModifiedProperties</code> 태그가 있습니다.</p>

> [!IMPORTANT]
> 이 태그는 <STRONG>Set-AdminAuditLogConfig</STRONG> cmdlet의 <EM>LogLevel</EM> 매개 변수가 <CODE>Verbose</CODE>로 설정된 경우에만 채워집니다.


</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p></p></td>
<td><p>이 태그에는 cmdlet을 실행할 때 지정된 개별 속성이 포함됩니다. 이 태그에는 <code>Name</code>, <code>OldValue</code> 및 <code>NewValue</code> 특성이 포함됩니다.</p>
<p><code>ModifiedProperties</code> 태그당 여러 <code>Property</code> 태그가 있을 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>이 특성에는 cmdlet을 실행할 때 수정된 속성의 이름이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>이 특성에는 변경 전에 <code>Name</code> 특성에 지정된 속성에 포함되었던 값이 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>이 특성에는 <code>Name</code> 특성의 속성이 변경된 값이 포함됩니다.</p></td>
</tr>
</tbody>
</table>


## 감사 로그 항목 예

다음은 일반적인 감사 로그 항목의 예입니다. 로그 항목의 정보를 기반으로 다음이 발생한 것을 알 수 있습니다.

  - 태평양 표준시(UTC-7) 2012-10-18 오후 03:48에 `Administrator` 사용자가 **Set-Mailbox** cmdlet을 실행했습니다.

  - **Set-Mailbox** cmdlet을 실행할 때 다음의 두 매개 변수가 제공되었습니다.
    
      - *Identity* 값 `david`
    
      - *ProhibitSendReceiveQuota* 값 `10GB`

  - `david` 개체에서 다음 두 속성이 수정되었습니다.
    

    > [!NOTE]
    > 이 예에서는 <CODE>Set-AdminAuditLogConfig</CODE> cmdlet의 <EM>LogLevel</EM> 매개 변수가 <CODE>Verbose</CODE>로 설정되었으므로 수정된 속성이 감사 로그에 저장됩니다.

    
      - *ProhibitSendReceiveQuota* 새 값 `10GB`, 기존 값 `35GB`를 대체함

  - 작업이 오류 없이 완료되었습니다.

<!-- end list -->

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <SearchResults>
  
    <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
      <CmdletParameters>
        <Parameter Name="Identity" Value="david" />
        <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
      </CmdletParameters>
      <ModifiedProperties>
        <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
      </ModifiedProperties>
    </Event>
  </SearchResults>
  ```


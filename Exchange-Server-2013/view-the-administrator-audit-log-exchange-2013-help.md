---
title: '관리자 감사 로그 보기: Exchange Online Protection Help'
TOCTitle: 관리자 감사 로그 보기
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56270188
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자 감사 로그 보기

 

_**적용 대상:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-05-03_

Microsoft EOP(Exchange Online Protection), Microsoft Exchange Online 및 Microsoft Exchange 2013에서는 EAC(Exchange 관리 센터)를 사용하여 *관리자 감사 로그*의 항목을 검색하고 볼 수 있습니다. 관리자 감사 로그에는 관리 권한이 할당된 관리자와 사용자가 수행하는 특정 작업이 Exchange 관리 셸 cmdlet을 기준으로 기록됩니다. 관리자 감사 로그의 항목은 실행된 cmdlet, 사용된 매개 변수, cmdlet을 실행한 사용자 및 영향을 받은 개체에 대한 정보를 제공합니다.


> [!NOTE]
> <UL>
> <LI>
> <P>관리자 감사 로깅은 기본적으로 사용됩니다.</P>
> <LI>
> <P><STRONG>Get</STRONG>, <STRONG>Search</STRONG> 또는 <STRONG>Test</STRONG> 동사로 시작하는 Exchange 관리 셸 cmdlet이 기준인 작업은 관리자 감사 로그에 기록되지 않습니다.</P>
> <LI>
> <P>감사 로그 항목은 90일 동안 보관되고, 90일이 지난 항목은 삭제됩니다.</P></LI></UL>



## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [EOP의 기능 사용 권한](https://technet.microsoft.com/ko-kr/library/jj723125\(v=exchg.150\))의 "보고서 보기" 항목

  - 앞에서 설명한 대로 관리자 감사 로깅은 기본적으로 사용됩니다. 사용하도록 설정되어 있는지 확인하려면 다음 명령을 실행하면 됩니다.
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    사용하지 않도록 설정된 경우 Exchange 2013에서 다음 명령을 실행하여 관리자 감사 로깅을 사용하도록 설정할 수 있습니다.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    Exchange Online Protection 및 Exchange Online에서는 관리자 감사 로깅이 항상 사용됩니다. 사용하지 않도록 설정할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 관리자 감사 로그 보기

1.  EAC에서 **준수 관리** \> **감사**로 이동하여 **관리자 감사 로그 보고서 실행**을 선택합니다.

2.  **시작 날짜**와 **종료 날짜**를 선택하고 **검색**을 선택합니다. 지정한 기간 동안 적용된 모든 구성 변경 내용이 표시됩니다. 이러한 변경 내용은 다음 정보를 사용하여 정렬할 수 있습니다.
    
      - **날짜**   구성이 변경된 날짜와 시간입니다. 날짜와 시간은 UTC(협정 세계시) 형식으로 저장됩니다.
    
      - **Cmdlet**   구성을 변경하는 데 사용된 cmdlet의 이름입니다.
    
      - **사용자**   구성을 변경한 사용자의 사용자 계정 이름입니다.
    
    여러 페이지에 항목이 5,000개까지 표시됩니다. 결과의 범위를 좁혀야 하는 경우 날짜 범위를 더 좁게 지정하세요. 개별 검색 결과를 선택하면 세부 정보 창에 다음 추가 정보가 표시됩니다.
    
      - **수정된 개체**   cmdlet에 의해 수정된 개체입니다.
    
      - **매개 변수(매개 변수:값)**   사용된 cmdlet 매개 변수 및 해당 매개 변수와 함께 지정된 값입니다.

3.  특정 감사 로그 항목을 인쇄하려면 세부 정보 창의 **인쇄** 단추를 선택합니다.

## 작업이 완료되었는지 어떻게 확인합니까?

관리자 감사 로그 보고서를 정상적으로 실행하면 지정한 날짜 범위 내에 적용된 구성 변경 내용이 검색 결과 창에 표시됩니다. 결과가 표시되지 않으면 날짜 범위를 변경한 다음 보고서를 다시 실행합니다.


> [!NOTE]
> 조직에서 구성을 변경한 경우 해당 내용이 감사 로그 검색 결과에 표시될 때까지 최대 15분이 걸릴 수 있습니다. 변경 내용이 관리자 감사 로그에 표시되지 않으면 몇 분간 기다렸다가 검색을 다시 실행하세요.



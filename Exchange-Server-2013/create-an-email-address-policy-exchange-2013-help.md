---
title: '전자 메일 주소 정책 만들기: Exchange 2013 Help'
TOCTitle: 전자 메일 주소 정책 만들기
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50484469
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 전자 메일 주소 정책 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-12-10_

전자 메일 메시지를 보내거나 받는 사람의 받는 전자 메일 주소가 있어야 합니다. 받는 사람 (포함 하는 사용자, 연락처 및 그룹)에 대 한 기본 및 보조 전자 메일 주소를 생성 하는 전자 메일 주소 정책 수신 하 고 전자 메일을 보낼 수 있도록 합니다.

전자 메일 주소 정책을 만들 때는 다음과 같은 전자 메일 주소 유형을 사용할 수 있습니다.

  - **미리 만든 SMTP 전자 메일 주소**. *미리 만든* SMTP 전자 메일 주소는 사용자에게 제공되고 일반적으로 사용되는 전자 메일 주소 유형입니다.

  - **사용자 지정 SMTP 전자 메일 주소**. 미리 만든 SMTP 전자 메일 주소를 사용하지 않으려는 경우 사용자 지정 SMTP 전자 메일 주소를 지정할 수 있습니다.
    
    사용자 지정 SMTP 전자 메일 주소를 만드는 경우 다음 표에 나와 있는 변수를 사용하여 전자 메일 주소의 로컬 부분에 대해 대체 값을 지정할 수 있습니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>변수</th>
    <th>값</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>이름</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>중간 이니셜</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>성</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>표시 이름</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange 별칭</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>성에서 처음 <em>x</em>글자를 사용합니다. 예를 들어, <em>x</em> =2이면 성의 처음 두 글자를 사용합니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>이름에서 처음 <em>x</em>글자를 사용합니다. 예를 들어, <em>x</em> =2이면 이름의 처음 두 글자를 사용합니다.</p></td>
    </tr>
    </tbody>
    </table>


  - **비 SMTP 전자 메일 주소**. 다음과 같은 형식의 비 SMTP 전자 메일 주소를 사용할 수 있습니다.
    
      - EX(레거시 DN 프록시 주소 접두사 표시 이름)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - EUM(Exchange 통합 메시징) 프록시 주소
    

    > [!IMPORTANT]
    > Exchange에서 모든 비 SMTP 전자 메일 주소는 사용자 지정 주소로 간주됩니다. Exchange는 X.400, GroupWise 또는 Lotus Notes 전자 메일 주소 유형에 대해 고유한 대화 상자 또는 속성 페이지를 제공하지 않습니다. 비 SMTP 사용자 지정 전자 메일 주소를 추가하는 경우에는 적절한 DLL(동적 연결 라이브러리) 파일이 있어야 합니다. 적절한 DLL 파일을 제공하지 않으면 사용자 지정된 전자 메일 주소 정책을 만들 수 없습니다. 이벤트 뷰어에 다음과 같은 오류가 로깅됩니다. "'i386' 시스템의 Microsoft Exchange Directory에 'SADF' 주소 유형에 대한 전자 메일 주소 설명 개체가 없습니다."



전자 메일 주소 정책을 만드는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

[전자 메일 주소 정책 만들기](create-an-email-address-policy-exchange-2013-help.md)

[받는 사람 필터를 사용 하 여 전자 메일 주소 정책 만들기](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [전자 메일 주소 및 주소록](email-addresses-and-address-books-exchange-2013-help.md)의 "전자 메일 주소 정책" 항목

  - 전자 메일 주소 정책에서 SMTP 주소 도메인을 사용할 수 있습니다, 전에 허용된 도메인을 구성 해야 합니다. 자세한 내용은 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

> [!CAUTION]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>


## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 전자 메일 주소 정책을 만들려면

1.  **메일 흐름** 으로 이동 \> **전자 메일 주소 정책**, 다음![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 하 고 있습니다.

2.  **전자 메일 주소 정책** 다음 필드에 입력 합니다.
    
      - **정책 이름**
    
      - **전자 메일 주소 형식**
    
      - **이 전자 메일 주소를 적용할 받는 사람 유형 지정**

3.  
    
    더 자세히이 정책에 적용 될 받는 사람을 제한 하려면 **규칙 추가** 클릭 합니다. 이 부울 **및** 문을 만듭니다.
    

    > [!WARNING]
    > 너무 많은 규칙을 적용하면 전자 메일 주소 정책이 사용자를 전혀 포함하지 않는 상태로 제한될 수 있습니다.



4.  정책이 적용될 받는 사람을 보려면 **정책을 적용할 받는 사람 미리 보기**를 클릭합니다.

5.  
    
    **저장**을 클릭하여 변경 내용을 저장하고 정책을 만듭니다.

6.  전자 메일 주소 정책을 업데이트해야 정책이 적용된다는 경고가 나타납니다. 정책을 만든 후에 선택한 다음 세부 정보 창에서 **적용**을 클릭합니다.

## 셸을 사용 하 여 전자 메일 주소 정책 만들기

이 예제에서는 함께 자신의 이름의 처음 두 글자를 사용 하 여 자신의 마지막 이름을 포함 하는 전자 메일 주소를 가진 남동쪽 사무실에 사서함 사용자를 포함 하는 전자 메일 주소 정책을 만듭니다.

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

자세한 구문 및 매개 변수 정보에 대 한 [New-EmailAddressPolicy](https://technet.microsoft.com/ko-kr/library/aa996800\(v=exchg.150\))를 참조 하십시오.


---
title: '전자 메일 주소 정책: Exchange 2013 Help'
TOCTitle: 전자 메일 주소 정책
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50483960
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일 주소 정책

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-07-21_

받는 사람(사용자, 리소스, 연락처 및 그룹 포함)은 Microsoft Exchange가 메시지를 배달하거나 라우팅할 수 있는 Active Directory에서 메일 사용이 가능한 개체입니다. 받는 사람이 전자 메일 메시지를 보내거나 받으려면 받는 사람에게 전자 메일 주소가 있어야 합니다. 전자 메일 주소 정책이 받는 사람의 기본 및 보조 전자 메일 주소를 생성하므로 받는 사람이 전자 메일을 받거나 보낼 수 있습니다.

기본적으로 Exchange에는 모든 메일 사용 가능 사용자에 대한 전자 메일 주소 정책이 있습니다. 이 기본 정책은 받는 사람의 별칭을 전자 메일 주소의 로컬 부분으로 지정하고 기본 허용 도메인을 사용합니다. 전자 메일 주소의 로컬 부분은 @ 기호 앞의 이름입니다. 그러나 받는 사람의 전자 메일 주소가 표시되는 방법을 변경할 수 있습니다. 예를 들어 주소가 *firstname*.*lastname*@contoso.com으로 표시되도록 지정할 수 있습니다.

또한 모든 받는 사람 또는 하위 집합에 대해서만 추가 전자 메일 주소를 지정하려는 경우 기본 정책을 수정하거나 추가 정책을 만들 수 있습니다. 예를 들어, David Hamilton의 사용자 사서함은 hdavid@mail.contoso.com 및 hamilton.david@mail.contoso.com으로 주소가 지정된 전자 메일 메시지를 받을 수 있습니다.

전자 메일 주소 정책과 관련된 관리 작업에 대한 자세한 내용은 [전자 메일 주소 정책 절차](email-address-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 받는 사람 정책의 동작

Exchange는 받는 사람 필터링 기준과 일치하는 모든 받는 사람에게 정책을 적용합니다.

  - 받는 사람 정책은 낮은 우선순위를 가장 높은 우선순위 순서 대로 적용 됩니다. 둘 이상의 정책 간에 충돌이 발생할 경우 우선순위가 가장 높은 정책을 적용 됩니다. 기본 받는 사람 정책은 항상 가장 낮은 우선순위 있으며 없는 다른 정책과 일치 하는 경우에 적용 됩니다.
    
    받는 사람 정책을 만들었지만 우선순위를 명시적으로 지정 하지 때 가장 높은 우선순위도 추가 됩니다. 이미 연결 된 기존 정책과 우선순위를 지정 하는 경우 기존 정책 및 모든 정책의 경우 낮은 우선순위를 이동할 하나에 의해 합니다. 새 정책은 지정한 우선순위에 삽입 됩니다.
    
    받는 사람 정책 기능은 전자 메일 주소 정책 및 허용 도메인이라는 두 가지 기능으로 구분됩니다. 허용 도메인에 대한 자세한 내용은 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조하십시오.

  - Exchange 관리 셸에서 **Update-EmailAddressPolicy** cmdlet을 실행하는 경우 받는 사람 개체가 전자 메일 주소 정책을 통해 업데이트됩니다.

  - 받는 사람 개체를 수정하고 저장할 때마다 Exchange는 전자 메일 주소 기준과 설정이 올바르게 적용되었는지 확인합니다. 전자 메일 주소 정책을 수정하고 저장하면 모든 관련 받는 사람이 변경 내용으로 업데이트됩니다. 또한 받는 사람 개체를 수정하면 해당 받는 사람의 전자 메일 주소 정책 구성원 자격이 다시 평가되어 적용됩니다.

## 전자 메일 주소 정책 만들기

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


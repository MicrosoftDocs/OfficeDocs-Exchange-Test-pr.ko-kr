---
title: 'IOS에 대 한 Outlook 및 기본 인증을 사용 하 여 Android에서 계정 설정: Exchange 2013 Help'
TOCTitle: IOS에 대 한 Outlook 및 기본 인증을 사용 하 여 Android에서 계정 설정
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518371
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IOS에 대 한 Outlook 및 기본 인증을 사용 하 여 Android에서 계정 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-04-30_

**요약:**  Exchange 2013 조직의 사용자가 자신의 Outlook iOS 및 기본 인증을 사용 하 여 Android 계정에 대 한을 신속 하 게 설정 하는 방법을 합니다.

IOS와 Android에 대 한 outlook은 Exchange 관리자 계정 구성을 ActiveSync 프로토콜을 통해 기본 인증을 사용 하는 온-프레미스 사용자에 게 "푸시" 하는 기능을 제공 합니다. 이 기능은 for Android iOS 또는 [기업에서 Android](https://developer.android.com/samples/apprestrictions/index.html) 채널에 대 한 [관리 되는 응용 프로그램 구성](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) 채널을 사용 하는 모바일 장치 관리 (MDM) 공급자와 함께 작동 합니다.

온-프레미스 사용자에 대 한 Microsoft Intune에 등록, Intune를 사용 하 여 Azure 포털의 계정 구성 설정을 배포할 수 있습니다.

만든 계정을 구성 하 고 사용자가 장치 iOS에 대 한 Outlook 등록 되 고 Android는 감지 하는 계정이 "" 찾은 다음 계정을 추가 하려면 사용자를 묻습니다. 설치 프로세스를 완료 하려면 입력 하 고 사용자에 게 필요한 유일한 정보는 자신의 암호입니다. 그런 다음, 사용자의 사서함 콘텐츠를 로드 합니다 하 고 사용자 응용 프로그램을 사용 하 여 시작할 수 있습니다.

다음 이미지 iOS에 대 한 Outlook 및 Android를 구성한 후 Azure 포털에서 Intune에서 최종 사용자 설치 프로세스의 예를 보여줍니다.

![온-프레미스의 iOS 및 Android용 Outlook 계정 설정](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "온-프레미스의 iOS 및 Android용 Outlook 계정 설정")

## IOS에 대 한 Outlook 및 Microsoft Intune를 사용 하 여 Android에 대 한 응용 프로그램 구성 정책 만들기

Microsoft Intune를 모바일 장치 관리 공급자로 사용 하는 경우 다음 단계를 배포할 수 있도록 해 ActiveSync 프로토콜을 통한 기본 인증을 활용 하 여 온-프레미스 사서함에 대 한 계정 구성 설정 합니다. 구성을 만든 다음 구성 설정에 할당하는 다음 섹션에서 설명한 대로 사용자 그룹으로 설정을 할당할 수 있습니다.


> [!NOTE]
> 작업 장치에 대 한 iOS와 Android를 사용 하는 조직에서 사용자를 하는 경우에 각 플랫폼에 대 한 별도 응용 프로그램 구성 정책을 만들려면 필요 합니다.



1.  Azure 포털에 로그인 합니다.

2.  선택 **서비스를 더 \> 모니터링 + 관리 \> Intune**합니다.

3.  관리 목록에서 **모바일 앱** 블레이드에서 **응용 프로그램 구성 정책**을 선택 합니다.

4.  **앱 구성 정책** 블레이드에서 **추가**선택 합니다.

5.  **추가 응용 프로그램 구성** 블레이드에서 앱 구성 설정에 대 한 **이름**및 선택적 **설명** 을 입력 합니다.

6.  **장치 등록** 형식에 대 한 **관리 되는 장치**를 선택 합니다.

7.  **플랫폼**대 한 **iOS** 또는 **작업에 대 한 Android**를 선택 합니다.

8.  **연결 된 응용 프로그램**선택 하 고을 **대상 앱** 블레이드 **iOS에 대 한 Microsoft Outlook** 또는 **Microsoft Outlook for Android**선택 합니다.

9.  **추가 응용 프로그램 구성** 블레이드도 돌아가려면 **확인** 클릭 합니다.

10. **구성 설정**을 선택 합니다. **구성 설정** 블레이드 iOS에 대 한 Outlook 및 Android에 대 한 구성을 제공 하는 키 값 쌍을 정의 합니다. 입력 하는 키 값 쌍은 키 값 쌍의 섹션에서이 문서의 뒷부분에 정의 됩니다.
    

    > [!NOTE]
    > 키 값 쌍을 입력 하려면 구성 디자이너를 사용 하 여 또는 XML 속성 목록을 입력 중 하나를 선택을 해야 합니다.



11. 작업이 완료 되 면 **확인**을 선택 합니다.

12. **추가 응용 프로그램 구성** 블레이드 **만들기**를 선택 합니다.

새로 만든된 구성 정책 **앱 구성 정책** 블레이드에 표시 됩니다.

## 구성 설정 할당

Azure Active Directory의 사용자 그룹에 이전 섹션에서 만든 설정을 할당 합니다. 사용자가 설치 된 Microsoft Outlook 응용 프로그램을 사용 하는 경우 응용 프로그램을 지정 했는지 설정에 의해 관리 됩니다. 이 작업을 수행 합니다.

1.  Intune 모바일 응용 프로그램 관리 대시보드 **모바일 앱** 블레이드에서 **응용 프로그램 구성 정책**을 선택 합니다.

2.  앱 구성 정책 목록에서을 할당 하려는 항목을 선택 하 고 **할당**을 선택 합니다.

3.  **배정** 블레이드에서 **그룹을 선택**합니다.를 선택 합니다.

4.  **그룹을 선택** 블레이드 앱 구성 정책을 할당 한 다음 **선택**, 한 다음 **저장**을 선택 하려면 원하는 Azure AD 그룹을 선택 합니다.

## 키 값 쌍

Azure 포털에서 또는 MDM 공급자를 통해 응용 프로그램 구성 정책을 만들면 하는 경우에 다음과 같은 키 값 쌍 필요 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>키</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>이 값 통해 장치에는 사용자에 게 표시 되는 표시 이름을 전자 메일 계정을 지정 합니다.</p>
<p><strong>허용 값</strong>: 문자열</p>
<p><strong>지정 하지 않으면 기본</strong>: &lt; 빈 &gt;</p>
<p><strong>예</strong>: user@companyname.com</p>
<p><strong>Intune 토큰 *</strong>: {{username}을 (를)</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>이 값을 보내고 받는 메일에 사용할 전자 메일 주소를 지정 합니다.</p>
<p><strong>허용 값</strong>: 문자열</p>
<p><strong>지정 하지 않으면 기본</strong>: &lt; 빈 &gt;</p>
<p><strong>예</strong>: user@companyname.com</p>
<p><strong>Intune 토큰 *</strong>: {{메일}을 (를)</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>이 값에는 계정을 인증에 사용 되는 전자 메일 프로필에 대 한 사용자 계정 이름을 지정 합니다.</p>
<p><strong>허용 값</strong>: 문자열</p>
<p><strong>지정 하지 않으면 기본</strong>: &lt; 빈 &gt;</p>
<p><strong>예</strong>: userupn@companyname.com</p>
<p><strong>Intune 토큰 *</strong>: {{userprincipalname}을 (를)</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>이 값은 사용자에 대 한 인증 방법을 지정합니다.</p>
<p><strong>허용 값</strong>: '사용자 이름 및 암호'; ' 인증서 '</p>
<p><strong>지정 하지 않으면 기본</strong>: '사용자 이름 및 암호'</p>
<p><strong>예</strong>: '사용자 이름 및 암호'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>이 값에는 Exchange 서버의 호스트 이름을 지정합니다.</p>
<p><strong>허용 값</strong>: 문자열</p>
<p><strong>지정 하지 않으면 기본</strong>: &lt; 빈 &gt;</p></td>
</tr>
</tbody>
</table>


**\*** Microsoft Intune 사용자 등록 MDM 사용자에 따라 올바른 값으로 확장 하는 토큰을 사용할 수 있습니다. 자세한 내용은 [관리 되는 iOS 장치에 대 한 추가 응용 프로그램 구성 정책](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios) 을 참조 하십시오.


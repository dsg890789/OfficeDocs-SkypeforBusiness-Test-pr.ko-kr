﻿---
title: 'Lync Server 2013: 보관에 대한 요구 사항 정의'
TOCTitle: 보관에 대한 조직 요구 사항 정의
ms:assetid: ce0fc0f6-7704-4b80-bf19-a1fa9818fc7a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ205276(v=OCS.15)
ms:contentKeyID: 49305065
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013에서 보관에 대한 요구 사항 정의

 

_**마지막으로 수정된 항목:** 2012-10-09_

조직에서 준수 규정을 따라야 하는 경우 보관을 배포하여 Lync Server 2013 메신저 대화 및 회의(모임)에 대한 보관 지원을 사용하도록 설정할 수 있습니다. 보관할 수 있는 콘텐츠 유형에 대한 자세한 내용은 계획 설명서에서 [Lync Server 2013의 보관 개요](lync-server-2013-overview-of-archiving.md)를 참조하십시오.

보관을 구현하려면 조직의 보관 요구 사항을 충족할 방식을 먼저 결정해야 합니다. 그러려면 다음을 결정해야 합니다.

  - **보관을 배포할 시기**. 처음 Lync Server 2013을 배포할 때 보관을 배포하거나, 기존 배포에 추가할 수 있습니다. 토폴로지 작성기를 사용하여 토폴로지에 추가한 후 게시하는 방법으로 보관을 배포합니다.

  - **내부 또는 외부 통신을 설정해야 하는지 여부**. 내부 사용자 간의 내부 통신, 내부 네트워크 밖에 있는 사용자가 한 명 이상 포함된 외부 통신 또는 둘 모두를 사용하도록 보관을 설정할 수 있습니다. 전체 조직에 대해 이러한 옵션을 지정하거나, 특정 사이트 및 풀에 대해 지정할 수 있습니다. 기본적으로는 두 옵션 모두 사용하지 않도록 설정됩니다.
    

    > [!NOTE]
    > Microsoft Exchange 통합을 사용하여 보관 데이터를 저장하는 경우 Exchange 설정에 따라 Lync 통신을 보관할지 여부가 제어됩니다. 여러 포리스트가 포함된 배포의 경우 Lync Server 및 Exchange 간의 설정을 동기화해야 합니다. 내부 또는 외부 통신을 보관하는 것은 Lync 정책을 통해서만 제어할 수 있습니다. Exchange 통합 보관의 경우 둘 모두를 보관하거나 둘 모두를 보관하지 않게 됩니다.



  - **보관을 사용하는 이유**. 전역 수준의 전역 배포에 대해 그리고 특정 사이트 및 사용자에 대해 보관을 사용하거나 사용하지 않도록 설정할 수 있습니다. 이러한 수준의 각각에 대해 피어 투 피어 메신저 세션의 보관, 단체 세션인 모임이나 회의의 보관, 또는 둘 모두의 보관 여부를 지정할 수 있습니다. 기본적으로 보관은 사용하지 않도록 설정되어 있습니다.

  - **조직의 사용자에게 있어 보관의 중요도**. 조직에 있어 보관이 중요한 경우 Lync Server 2013을 중요 모드로 실행하도록 지정할 수 있습니다. 그러면 보관이 실패하는 경우 메신저 및 회의 세션이 차단됩니다. 예를 들면 다음과 같습니다.
    
      - 보관 서비스에서 일시적으로 데이터베이스 큐에 메시지를 보낼 수 없거나 데이터베이스에 메시지를 삽입할 수 없는 경우 보관 지원이 복원될 때까지 메신저 대화와 회의 기능이 둘 다 배포에서 차단됩니다.
    
      - 회의 사용자가 파일을 업로드했지만 파일을 보관 파일 저장소에 복사할 수 없는 경우 문제가 해결될 때까지 회의 기능이 배포에서 차단됩니다. 그러나 메신저 기능은 차단되지 않습니다.
    
    이 옵션은 전역 수준, 사이트 수준 및 풀 수준에서 구성할 수 있습니다. 기본적으로 중요 모드는 사용되지 않습니다.

  - **Microsoft Exchange 통합을 사용하는지 여부**. 이 옵션은 Exchange 2013 저장소와 보관 저장소를 통합하므로 Lync Server 보관 데이터 및 Exchange 2013 보관 데이터가 Exchange에 함께 저장됩니다. Exchange 2013에 있는 사용자의 경우 사서함이 원본 위치 유지의 상태이면 해당 사용자의 보관 데이터 저장소로 Microsoft Exchange 통합을 사용할 수 있습니다. Exchange 2013이 배포되지 않은 경우, 통합을 원하지 않는 경우, Lync 사용자가 Exchange 2013에 있지 않은 경우 등에는 SQL Server를 사용하여 별도의 보관 데이터베이스를 배포하고 Lync 통신의 보관 데이터를 저장할 수 있습니다. 전역 수준, 사이트 수준, 풀 수준에서 Microsoft Exchange 통합 옵션을 구성할 수 있습니다. 기본적으로 Microsoft Exchange 통합은 사용하지 않도록 구성되어 있습니다.

  - **보관 데이터가 관리되는 방식**. 보관 데이터베이스는 장기 보존의 목적으로 고안된 것이 아니며 Lync Server 2013은 보관 데이터의 e-Discovery(검색) 솔루션을 제공하지 않으므로 데이터를 다른 저장소로 이동해야 합니다. Lync Server은 보관 데이터를 내보내는 데 사용할 수 있는 세션 내보내기 도구를 제공하므로 보관 데이터를 검색 가능한 대화 내용으로 만들 수 있습니다. 만드는 정책 수준(전역, 사이트, 사용자)에 대해 데이터 제거를 사용하도록 설정하고 다음 옵션 중 하나를 지정할 수 있습니다.
    
      - 내보낸 보관 데이터 및 최대 기간(일)이 지난 저장된 보관 데이터 삭제 - 지정할 수 있는 최소 일 수는 1일이고, 최대 일 수는 2,562일입니다.
    
      - 내보낸 보관 데이터만 삭제 - 이 옵션은 세션 내보내기 도구에서 내보내고 삭제 가능한 것으로 표시한 모든 레코드를 제거합니다.
    
    이 옵션은 전역 수준, 사이트 수준 및 풀 수준에서 구성할 수 있습니다. 기본적으로 제거는 사용되지 않습니다.

보관은 다음 방법을 사용하여 제어합니다.

  - **보관 정책** 하나 이상의 보관 정책을 사용하여 내부 및 외부 통신의 보관을 사용 또는 사용하지 않도록 설정할 수 있습니다. 기본적으로 사용하도록 설정되는 보관은 없습니다. 기본 전역 정책을 사용하여 배포에 내부 통신, 외부 통신 또는 둘 모두에 대해 보관을 사용 또는 사용하지 않도록 설정할 수 있습니다. 전역 정책은 삭제할 수 없습니다. 특정 사이트의 내부 및 외부 통신에 대해 보관을 사용 또는 사용하지 않도록 하나 이상의 선택적 사이트 정책을 지정할 수 있습니다. 또한 하나 이상의 사용자 정책을 지정하여 특정 사용자 및 사용자 그룹에 대해 보관을 사용 또는 사용하지 않도록 설정할 수 있습니다. 사용자 수준 정책은 사이트 정책보다 우선 적용되고, 사이트 수준 정책은 전역 수준 정책보다 우선 적용됩니다. 사용자 수준 정책은 정책을 사용하도록 구성된 특정 사용자에게만 구현됩니다. 그룹 메신저 대화 및 회의는 하나 이상의 참가자에 대한 정책이 보관을 사용하도록 구성된 경우에만 보관됩니다.
    

    > [!NOTE]
    > Microsoft Exchange 통합을 사용하는 경우 Exchange 2013 정책이 Exchange 2013 서버에 있는 모든 사용자에 대해 Lync Server 보관 정책보다 우선 적용됩니다.



  - **보관 구성**. 하나 이상의 보관 구성을 사용하여 이 문서에서 이전에 설명한 보관 옵션의 대부분을 지정할 수 있습니다. 단, 이전 글머리 기호에서 설명한 것처럼 보관 정책을 사용하여 구성되는 내부 및 외부 통신을 사용하도록 설정하는 옵션은 제외됩니다. 보관 구성에는 기본 전역 구성 및 선택적 사이트/풀 구성이 포함됩니다. 풀 수준 구성은 사이트 수준 구성보다 우선 적용되고, 사이트 수준 구성은 전역 수준 구성보다 우선 적용됩니다.

요구 사항을 분석하는 과정에서 전역 보관 구성 및 전역 보관 정책을 구성하는 방식을 결정해야 합니다. 또한 사이트 수준 보관 구성, 풀 수준 보관 구성, 사이트 수준 보관 정책 및 사용자 수준 보관 정책 등에 대한 요구 사항도 결정해야 합니다.

하나의 프런트 엔드 풀 또는 Standard Edition Server에 대해 보관을 배포한 경우 배포에 포함된 다른 모든 프런트 엔드 풀 및 Standard Edition Server에 대해서도 보관을 사용하도록 설정해야 합니다. 통신을 보관해야 하는 사용자가 다른 풀에서 호스팅된 그룹 메신저 대화나 모임에 초대될 수 있으므로 이 작업을 수행해야 합니다. 대화 또는 모임이 호스팅되는 풀에 보관이 설정되어 있지 않으면 일부 회의 데이터가 보관되지 않을 수 있습니다. 보관은 보관을 사용하도록 설정한 사용자에 대해 작동하지만 회의 콘텐츠 및 이벤트는 보관되지 않을 수 있습니다.


> [!NOTE]
> 조직의 보안 표준을 유지하면서 관리 작업을 위임할 수 있도록 설정하려면 Lync Server 2013에서 RBAC(역할 기반 액세스 제어)를&nbsp;사용해야 합니다. RBAC를 통해 사용자에게 미리 정의된 관리 역할을 할당함으로써 관리 권한이 부여됩니다. Lync 보관 정책 및 보관 구성을 구성하려면 사용자가 CsArchivingAdministrator 역할에 할당되어야 합니다. 단, 다른 컴퓨터에서 원격으로 구성되는 것이 아닌 보관이 배포된 서버에 직접 수행되는 경우는 제외됩니다. RBAC에 대한 자세한 내용은 계획 설명서에서 <A href="lync-server-2013-planning-for-role-based-access-control.md">Lync Server 2013의 역할 기반 액세스 제어 계획</A>를 참조하십시오. 보관 배포에 필요한 사용자 권한, 사용 권한 및 역할 목록은 계획 설명서와 배포 설명서에서 <A href="lync-server-2013-deployment-checklist-for-archiving.md">Lync Server 2013의 보관용 배포 검사 목록</A>를 참조하십시오.<BR>Microsoft Exchange 통합을 사용하는 경우 Exchange 정책을 구성하려면 적합한 관리자 권한 및 사용 권한이 있어야 합니다. 자세한 내용은 Exchange 2013 설명서를 참조하십시오.



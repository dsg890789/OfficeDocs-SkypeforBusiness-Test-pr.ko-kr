﻿---
title: 'Lync Server 2013: 장애 조치(failover) 경로 구성'
TOCTitle: 장애 조치(failover) 경로 구성
ms:assetid: 76e48df4-3b78-4fb7-b1f7-c1e604b81bad
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg398581(v=OCS.15)
ms:contentKeyID: 49304079
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013에서 장애 조치(failover) 경로 구성

 

_**마지막으로 수정된 항목:** 2015-03-09_

다음 예제에서는 관리자가 Dallas-GW1이 유지 관리를 위해 다운되거나 다른 이유로 인해 사용할 수 없는 경우 사용할 장애 조치(failover) 경로를 정의할 수 있는 방법을 보여 줍니다. 다음 표에서는 필요한 구성 변경을 보여 줍니다.

### 표 1. 사용자 정책

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>사용자 정책</th>
<th>전화 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 통화 정책</p></td>
<td><p>Local</p>
<p>GlobalPSTNHopoff</p></td>
</tr>
<tr class="even">
<td><p>레드몬드 시내 정책</p></td>
<td><p>RedmondLocal</p></td>
</tr>
<tr class="odd">
<td><p>달라스 통화 정책</p></td>
<td><p>DallasUsers</p>
<p>GlobalPSTNHopoff</p></td>
</tr>
</tbody>
</table>


### 표 2. 경로

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>경로 이름</th>
<th>발신 제한</th>
<th>전화 사용</th>
<th>트렁크</th>
<th>게이트웨이</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>레드몬드 시내 경로</p></td>
<td><p>^\+1(425|206|253)(\d{7})$</p></td>
<td><p>Local</p>
<p>RedmondLocal</p></td>
<td><p>Trunk1</p>
<p>Trunk2</p></td>
<td><p>Red-GW1</p>
<p>Red-GW2</p></td>
</tr>
<tr class="even">
<td><p>달라스 시내 경로</p></td>
<td><p>^\+1(972|214|469)(\d{7})$</p></td>
<td><p>Local</p></td>
<td><p>Trunk3</p></td>
<td><p>Dallas-GW1</p></td>
</tr>
<tr class="odd">
<td><p>범용 경로</p></td>
<td><p>^\+?(\d*)$</p></td>
<td><p>GlobalPSTNHopoff</p></td>
<td><p>Trunk1</p>
<p>Trunk2</p>
<p>Trunk3</p></td>
<td><p>Red-GW1</p>
<p>Red-GW2</p>
<p>Dallas-GW1</p></td>
</tr>
<tr class="even">
<td><p>달라스 사용자 경로</p></td>
<td><p>^\+?(\d*)$</p></td>
<td><p>DallasUsers</p></td>
<td><p>Trunk3</p></td>
<td><p>Dallas-GW1</p></td>
</tr>
</tbody>
</table>


표 1에서 GlobalPSTNHopoff의 전화 사용은 달라스 통화 정책의 DallasUsers 전화 사용 뒤에 추가됩니다. 이렇게 하면 DallasUsers 전화 사용의 경로를 사용할 수 없는 경우 달라스 통화 정책의 통화가 GlobalPSTNHopoff 전화에 대해 구성된 경로를 사용할 수 있습니다.


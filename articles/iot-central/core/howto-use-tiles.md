---
title: Azure IoT Central 응용 프로그램 대시보드에서 타일을 사용 하는 방법 | Microsoft Docs
description: 작성기로 응용 프로그램 대시보드, 장치 집합 대시보드 및 장치 대시보드에서 타일을 사용 하는 방법에 대해 알아봅니다.
author: v-krghan
ms.author: v-krghan
ms.date: 06/27/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: philmea
ms.openlocfilehash: 0803258c362279049a49a7eee00e7a4763621672
ms.sourcegitcommit: 4c3d6c2657ae714f4a042f2c078cf1b0ad20b3a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72952629"
---
# <a name="how-to-use-tiles"></a>타일을 사용 하는 방법
타일을 사용 하 여 응용 프로그램 대시보드, 장치 대시보드 및 장치 집합 대시보드를 사용자 지정할 수 있습니다. 여러 타일을 대시보드에 추가 하 고 응용 프로그램과 관련 된 정보를 표시 하도록 타일을 사용자 지정할 수 있습니다. 타일의 크기를 조정 하 고 모든 대시보드에서 레이아웃을 사용자 지정할 수도 있습니다. 아래 스크린샷에서는 다른 타일이 포함 된 응용 프로그램 대시보드를 보여 줍니다.

![애플리케이션 대시보드](media/howto-use-tiles/image1a.png)


다음 표에는 Azure IoT Central의 타일 사용이 요약 되어 있습니다.

 
| 타일 | 대시보드 | 설명
| ----------- | ------- | ------- |
| 링크 | 응용 프로그램 및 장치 집합 대시보드 |링크 타일은 제목 및 설명 텍스트를 표시 하는 클릭 가능한 타일입니다. 링크 타일을 사용 하 여 사용자가 응용 프로그램과 관련 된 URL을 탐색할 수 있도록 합니다. |
| 이미지 | 응용 프로그램 및 장치 집합 대시보드 |이미지 타일은 사용자 지정 이미지를 표시 하며 클릭할 수 있습니다. 이미지 타일을 사용 하 여 대시보드에 그래픽을 추가 하 고 필요에 따라 사용자가 응용 프로그램과 관련 된 URL로 이동할 수 있습니다.|
| 레이블 | 응용 프로그램 대시보드 |레이블 타일 대시보드에 사용자 지정 텍스트를 표시 합니다. 텍스트의 크기를 선택할 수 있습니다. 레이블 타일을 사용 하 여 관련 정보 (예: 설명, 연락처 세부 정보 또는 도움말)를 대시보드에 추가 합니다.|
| Map | 응용 프로그램 및 장치 집합 대시보드 |지도 타일 지도의 장치 위치와 상태를 표시 합니다. 예를 들어 장치가 있는 위치 및 팬이 켜져 있는지 여부를 표시할 수 있습니다.|
| 꺾은선형 차트 | 응용 프로그램 및 장치 대시보드 |꺾은선형 차트 타일 특정 기간 동안의 장치에 대 한 집계 측정 차트를 표시 합니다. 예를 들어 지난 1 시간 동안 장치의 평균 온도와 압력을 보여 주는 꺾은선형 차트를 표시할 수 있습니다.|
| 가로 막대형 차트 | 응용 프로그램 및 장치 대시보드 |가로 막대형 차트 타일 특정 기간 동안의 장치에 대 한 집계 측정값 차트를 표시 합니다. 예를 들어 지난 1 시간 동안 장치의 평균 온도와 압력을 보여 주는 가로 막대형 차트를 표시할 수 있습니다. |
| 이벤트 기록 | 응용 프로그램 및 장치 대시보드 |이벤트 기록 타일 시간 동안 장치에 대 한 이벤트를 표시 합니다. 예를 들어 지난 1 시간 동안 장치에 대해 발생 한 모든 온도 변화를 표시 하는 데 사용할 수 있습니다. |
| 상태 기록 | 응용 프로그램 및 장치 대시보드 |상태 기록 타일은 기간의 측정 값을 표시 합니다. 예를 들어 지난 1 시간 동안 장치에 대 한 온도 값을 표시 하는 데 사용할 수 있습니다.|
| KPI | 응용 프로그램 및 장치 대시보드 | KPI 타일 특정 기간에 대 한 집계 원격 분석 또는 이벤트 측정을 표시 합니다. 예를 들어, 지난 1 시간 동안 장치에 대해 도달한 최대 온도를 표시 하는 데 사용할 수 있습니다.|
| 마지막으로 알려진 값 | 응용 프로그램 및 장치 대시보드 |마지막으로 알려진 값 타일 원격 분석 또는 상태 측정의 최신 값을 표시 합니다. 예를 들어이 타일을 사용 하 여 장치에 대 한 온도, 압력 및 습도의 가장 최근 측정값을 표시할 수 있습니다.|
| 장치 집합 그리드 | 응용 프로그램 및 장치 집합 대시보드 | 장치 집합 표에 장치 집합에 대 한 정보가 표시 됩니다. 장치 집합 그리드 타일을 사용 하 여 장치 집합의 모든 장치에 대 한 이름, 위치 및 모델과 같은 정보를 표시 합니다.|


Azure IoT Central 응용 프로그램에서 대시보드를 구성 하는 방법에 대해 자세히 알아보려면 [대시보드에 타일 추가](./howto-add-tiles-to-your-dashboard.md)를 참조 하세요.

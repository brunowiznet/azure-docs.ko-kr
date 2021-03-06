---
title: Azure의 마이크로 서비스 소개
description: 마이크로 서비스 접근 방식을 통해 클라우드 애플리케이션을 빌드하는 것이 왜 현대 애플리케이션 개발에서 중요하며 Azure Service Fabric이 어떻게 이를 위한 플랫폼을 제공하는지에 대한 개요
ms.topic: conceptual
ms.date: 01/07/2020
ms.custom: sfrev
ms.openlocfilehash: af18a6cb45808c0af5ec2782a3fd2100e3b7bf99
ms.sourcegitcommit: 380e3c893dfeed631b4d8f5983c02f978f3188bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75750625"
---
# <a name="why-use-a-microservices-approach-to-building-applications"></a>응용 프로그램을 빌드하는 데 마이크로 서비스 접근 방식을 사용 하는 이유

소프트웨어 개발자의 경우 응용 프로그램을 구성 요소 파트로 팩터링 하는 것은 새로운 것이 아닙니다. 일반적으로 백 엔드 저장소, 중간 계층 비즈니스 논리 및 프런트 엔드 UI (사용자 인터페이스)를 사용 하 여 계층화 된 접근 방식이 사용 됩니다. 최근 몇 년 동안 변경 *된* 내용은 개발자가 클라우드 용 분산 응용 프로그램을 빌드하는 것입니다.

다음은 몇 가지 변화 하는 비즈니스 요구 사항입니다.

* 새로운 지역의 고객에 도달 하기 위해 대규모로 구축 및 운영 되는 서비스입니다.
* 민첩 한 방식으로 고객 요구에 대응할 수 있는 기능 및 기능을 빠르게 제공 합니다.
* 리소스 사용률 향상으로 비용을 줄여야 합니다.

이러한 비즈니스 요구가 애플리케이션을 구축하는 *방식* 에 영향을 미칩니다.

마이크로 서비스에 대 한 Azure 접근 방식에 대 한 자세한 내용은 [마이크로 서비스: 클라우드가 제공 하는 응용 프로그램 혁명](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/)을 참조 하세요.

## <a name="monolithic-vs-microservices-design-approach"></a>모놀리식와 마이크로 서비스 디자인 방법 비교

모든 애플리케이션은 시간에 따라 진화합니다. 성공적인 애플리케이션은 사람들에게 유용하게 되어 진화합니다. 실패 한 응용 프로그램은 진화 하지 않으며 결국 사용 되지 않습니다. 현재 요구 사항에 대 한 자세한 내용과 미래에 사용할 수 있는 문제는 다음과 같습니다. 예를 들어 회사에서 부서에 대 한 보고 응용 프로그램을 작성 하는 경우를 가정해 보겠습니다. 응용 프로그램이 회사의 범위 내에만 적용 되 고 보고서가 오랫동안 유지 되지 않는 것을 알 수 있습니다. 사용자의 접근 방식은 수십 억 명의 고객에 게 비디오 콘텐츠를 제공 하는 서비스를 구축 하는 것과는 다릅니다.

경우에 따라 개념 증명으로 도어를 가져오는 것이 주행 요소입니다. 나중에 응용 프로그램을 다시 디자인 하는 것을 알 수 있습니다. 과도 하 게 사용 되지 않는 작업을 엔지니어링 하는 점이 거의 없습니다. 반면 회사에서 클라우드를 빌드하는 경우에는 성장 및 사용이 예상 됩니다. 증가 및 확장은 예측할 수 없습니다. 향후 성공을 처리할 수 있는 경로를 알고 있는 동안 신속 하 게 프로토타입을 원합니다. 이것이 구축, 측정, 학습, 반복으로 이루어진 간결한 시작 접근 방식입니다.

클라이언트/서버 시대 중에는 각 계층의 특정 기술을 사용 하 여 계층화 된 응용 프로그램을 구축 하는 데 초점을 경향이 합니다. *모놀리식* 응용 프로그램 이라는 용어는 이러한 접근 방식을 설명 하기 위해 등장 했습니다. 인터페이스가 계층 사이에 속하는 경향이 있기 때문에 각 계층 내의 구성 요소 사이에는 더 긴밀히 연결된 설계가 적용되었습니다. 개발자는 라이브러리로 컴파일되어 몇 개의 실행 파일 및 Dll로 연결 된 클래스를 디자인 하 고 팩터링 했습니다.

모놀리식 디자인 접근 방식의 이점이 있습니다. 모놀리식 응용 프로그램을 디자인 하는 것이 더 간단 하며, 이러한 호출은 IPC (프로세스 간 통신)를 통해 자주 발생 하기 때문에 구성 요소 간의 호출이 더 빠릅니다. 또한 모든 사용자가 단일 제품을 테스트 하 여 인적 자원 사용을 보다 효율적으로 사용 하는 경향이 있습니다. 단점은 계층화 된 레이어 간의 밀접 한 결합이 있고 개별 구성 요소의 크기를 조정할 수 없다는 것입니다. 수정 이나 업그레이드를 수행 해야 하는 경우 다른 사용자가 테스트를 완료할 때까지 기다려야 합니다. 민첩 하 게 하는 것은 어려운 일입니다.

마이크로 서비스는 이러한 단점이를 해결 하 고 앞의 비즈니스 요구 사항과 더 밀접 하 게 부합 합니다. 그러나 장점과 부채도 모두 있습니다. 마이크로 서비스의 장점은 일반적으로 각각이 더 간단한 비즈니스 기능을 캡슐화하며 독립적으로 확장/축소, 테스트, 배포 및 관리할 수 있다는 점입니다. 마이크로 서비스 접근 방식을 사용 하는 경우의 중요 한 장점 중 하나는 팀이 기술에 비해 비즈니스 시나리오에 더 많은 영향을 주는 것입니다. 소규모 팀은 고객 시나리오를 기반으로 마이크로 서비스를 개발 하 고 사용 하려는 모든 기술을 사용 합니다.

다시 말해 조직에서는 마이크로 서비스 애플리케이션을 유지하기 위해 기술을 표준화할 필요가 없습니다. 자체 서비스를 보유한 개별 팀은 팀의 전문 지식을 바탕으로 합리적이거나 문제 해결에 가장 적합한 것을 수행할 수 있습니다. 실제로 특정 NoSQL 저장소 또는 웹 응용 프로그램 프레임 워크와 같은 권장 기술 집합이 좋습니다.

마이크로 서비스의 단점은 더 많은 개별 엔터티를 관리 하 고 더 복잡 한 배포 및 버전 관리를 처리 해야 한다는 것입니다. 마이크로 서비스 간의 네트워크 트래픽은 해당 네트워크 대기 시간과 마찬가지로 늘어납니다. 많은 번잡, 세부적인 서비스를 통해 성능이 저하 될 수 있습니다. 이러한 종속성을 확인 하는 데 도움이 되는 도구가 없는 경우 전체 시스템을 확인 하는 것은 어렵습니다.

표준은 고정 계약이 아닌 서비스에서 필요한 항목만 통신 하 고 허용할 하는 방법을 지정 하 여 마이크로 서비스 접근 방식을 작동 하도록 합니다. 서비스는 서로 독립적으로 업데이트 되므로 이러한 계약은 디자인에서 앞으로 정의 하는 것이 중요 합니다. 마이크로 서비스 접근 방식을 통한 설계와 연결된 또 다른 설명은 "세분화된 서비스 지향 아키텍처(SOA)"입니다.

***가장 간단 하 게 마이크로 서비스 디자인 방법은 통신에 대해 합의 된 각 및 합의 된 표준을 독립적으로 변경 하 여 서비스의 분리 된 페더레이션에 대 한 것입니다.***

더 많은 클라우드 응용 프로그램을 생성 하는 경우, 사용자는 전반적인 응용 프로그램을 독립적인 시나리오 중심 서비스로 분해 하는 것이 더 나은 장기적인 방법 이라는 것을 알게 되었습니다.

## <a name="comparison-between-application-development-approaches"></a>애플리케이션 개발 접근 방식 비교

![서비스 패브릭 플랫폼 애플리케이션 개발][Image1]

1) 모놀리식 응용 프로그램은 도메인별 기능을 포함 하며 일반적으로 웹, 비즈니스 및 데이터와 같은 기능 계층으로 구분 됩니다.

2) 모놀리식 응용 프로그램은 여러 서버/가상 머신/컨테이너에 복제 하 여 확장 합니다.

3) 마이크로 서비스 애플리케이션은 기능을 더 작은 개별 서비스로 구분합니다.

4) 마이크로 서비스 접근 방식에서는 각 서비스를 독립적으로 배포하여 확장하며 서버/가상 머신/컨테이너 간에 이러한 서비스의 인스턴스를 만듭니다.

마이크로 서비스 접근 방식을 사용 하 여 디자인 하는 것은 모든 프로젝트에 적합 하지는 않지만 앞에서 설명한 비즈니스 목표와 더 밀접 하 게 부합 합니다. 모놀리식 접근 방식으로 시작 하는 것은 나중에 마이크로 서비스 디자인으로 코드를 다시 사용할 수 있다는 것을 알고 있으면 적합할 수 있습니다. 모놀리식 애플리케이션을 시작하고, 확장성 또는 민첩성이 더 필요한 기능 영역부터 천천히 단계별로 분할하는 것이 더 일반적입니다.

마이크로 서비스 접근 방식을 사용 하는 경우 수많은 소규모 서비스의 응용 프로그램을 작성 합니다. 이러한 서비스는 컴퓨터의 클러스터에 걸쳐 배포 된 컨테이너에서 실행 됩니다. 소규모 팀은 시나리오에 중점을 둔 서비스를 개발 하 고, 전체 응용 프로그램을 개선할 수 있도록 각 서비스를 독립적으로 테스트, 버전, 배포 및 확장 하는 서비스를 개발 합니다.

## <a name="what-is-a-microservice"></a>마이크로 서비스란?

마이크로 서비스에 대한 정의는 여러 가지가 있습니다. 하지만 마이크로 서비스의 이러한 특징은 대부분 널리 허용 됩니다.

* 고객 또는 비즈니스 시나리오를 캡슐화합니다. 어떤 문제가 해결 되나요?
* 소규모 엔지니어링 팀에서 개발합니다.
* 모든 프레임 워크를 사용 하 여 모든 프로그래밍 언어로 작성 됩니다.
* 는 개별적으로 버전 관리, 배포 및 확장 되는 코드와 선택적 상태로 구성 됩니다.
* 잘 정의된 인터페이스와 프로토콜을 통해 타 마이크로 서비스와 상호 작용합니다.
* 해당 위치를 확인 하는 데 사용 되는 고유 이름 (Url)이 있어야 합니다.
* 일관되며 오류 시 사용 가능한 상태를 유지합니다.

합계를 계산 하려면:

***마이크로 서비스 애플리케이션은 독립적으로 버전 관리되며 확장성 있는 소규모 고객 중심 서비스로 구성됩니다. 이 서비스들은 잘 정의된 인터페이스가 있는 표준 프로토콜을 통해 서로 통신합니다.***

### <a name="written-in-any-programming-language-using-any-framework"></a>모든 프로그래밍 언어로 작성 된 모든 프레임 워크 사용

개발자는 현재 사용 중인 기술 및 서비스의 요구 사항에 따라 언어나 프레임 워크를 자유롭게 선택할 수 있습니다. 일부 서비스의 경우 그 밖의 C++ 성능 혜택을 얻을 수 있습니다. 또는 Java에서 C# 제공 하는 관리 되는 개발의 용이성은 더 중요할 수 있습니다. 경우에 따라 서비스를 클라이언트에 노출 하기 위해 특정 파트너 라이브러리, 데이터 저장소 기술 또는 메서드를 사용 해야 할 수 있습니다.

기술을 선택한 후 운영 또는 수명 주기 관리와 서비스 확장을 고려해 야 합니다.

### <a name="allows-code-and-state-to-be-independently-versioned-deployed-and-scaled"></a>개별적으로 버전 관리, 배포 및 확장되는 코드와 상태 허용

마이크로 서비스, 코드 및 필요에 따라 상태를 작성 하는 방법에 관계 없이 독립적으로 배포, 업그레이드 및 확장할 수 있습니다. 이 문제는 선택 된 기술에 도달 하기 때문에 해결 하기 어렵습니다. 크기 조정을 위해 코드와 상태를 분할 (또는 분할) 하는 방법을 이해 하는 것은 어려운 일입니다. 코드와 상태에서 일반적으로 사용 되는 다양 한 기술을 사용 하는 경우 마이크로 서비스의 배포 스크립트가 둘 다 크기를 조정할 수 있어야 합니다. 이러한 분리는 민첩성과 유연성에도 있으므로 한 번에 모두 업그레이드 하지 않고도 일부 마이크로 서비스를 업그레이드할 수 있습니다.

모놀리식 및 마이크로 서비스 접근 방식을 잠시 비교해 보겠습니다. 이 다이어그램은 상태를 저장 하는 방법의 차이점을 보여 줍니다.

#### <a name="state-storage-for-the-two-approaches"></a>두 방법에 대 한 상태 저장소

![서비스 패브릭 플랫폼 상태 스토리지][Image2]

***왼쪽에 있는 모놀리식 접근 방식에는 단일 데이터베이스와 특정 기술의 계층이 있습니다.***

***오른쪽의 마이크로 서비스 접근 방식에는 상태가 일반적으로 마이크로 서비스으로 범위가 지정 되 고 다양 한 기술이 사용 되는 상호 연결 된 마이크로 서비스 그래프가 있습니다.***

모놀리식 접근 방식에서 애플리케이션은 일반적으로 단일 데이터베이스를 사용합니다. 하나의 데이터베이스를 사용 하는 경우의 이점은 단일 위치에 있기 때문에 쉽게 배포할 수 있다는 것입니다. 각 구성 요소에는 상태 저장을 위한 단일 테이블이 있습니다. 팀은 상태를 엄격히 구분해야 하지만, 이는 어려운 일입니다. 누군가가 기존 customer 테이블에 열을 추가 하 고, 테이블 간에 조인을 수행 하 고, 저장소 계층에서 종속성을 만드는 경우를 들 수 있습니다. 이러한 경우가 발생하면, 개별 구성 요소를 확장할 수 없습니다.

마이크로 서비스 접근 방식에서는 각 서비스가 자체 상태를 관리 및 저장합니다. 각 서비스는 서비스의 수요에 맞게 코드와 상태를 함께 확장해야 합니다. 단점은 응용 프로그램 데이터의 뷰나 쿼리를 만들어야 하는 경우 여러 상태 저장소에 대해 쿼리해야 한다는 것입니다. 이 문제는 일반적으로 마이크로 서비스 컬렉션에 대 한 뷰를 작성 하는 별도의 마이크로 서비스에 의해 해결 됩니다. 데이터에 대해 여러 개의 임시 쿼리를 실행 해야 하는 경우 오프 라인 분석을 위해 각 마이크로 서비스의 데이터를 데이터 웨어하우징 서비스에 기록해 야 합니다.

마이크로 서비스는 버전 관리 됩니다. 마이크로 서비스의 서로 다른 버전을 함께 실행할 수 있습니다. 업그레이드 하는 동안 최신 버전의 마이크로 서비스가 실패할 수 있으며 이전 버전으로 롤백해야 합니다. 버전 관리는 다양 한 사용자가 서비스의 다른 버전을 경험 하는 A/B 테스트에도 유용 합니다. 예를 들어, 특정 고객 집합에 대해 마이크로 서비스를 업그레이드 하 여 더 광범위 하 게 배포 하기 전에 새 기능을 테스트 하는 것이 일반적입니다.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>잘 정의된 인터페이스와 프로토콜을 통해 타 마이크로 서비스와 상호 작용

지난 10 년 동안 서비스 지향 아키텍처의 통신 패턴을 설명 하는 광범위 한 정보가 게시 되었습니다. 일반적으로 서비스 통신은 직렬화 형식으로 HTTP 및 TCP 프로토콜과 XML 또는 JSON이 있는 REST 접근 방식을 사용합니다. 인터페이스 관점에서 보면 웹 디자인 접근 방식이 있습니다. 하지만 이진 프로토콜이 나 사용자 고유의 데이터 형식을 사용 하지 않도록 하는 것은 아닙니다. 이러한 프로토콜과 형식이 개방적으로 제공 되지 않는 경우 사용자는 마이크로 서비스를 사용 하는 데 더 많은 시간이 소요 됩니다.

### <a name="has-a-unique-name-url-used-to-resolve-its-location"></a>자신의 위치를 확인하기 위해 사용하는 고유 이름(URL)이 있음

마이크로 서비스는 어디서 실행되든지 주소 지정 가능해야 합니다. 컴퓨터 및 특정 마이크로 서비스을 실행 하는 컴퓨터에 대해 생각 하는 경우에는 작업이 신속 하 게 발생할 수 있습니다.

DNS가 특정 URL을 특정 머신으로 확인하는 것과 동일한 방법으로 마이크로 서비스는 현재 위치를 검색할 수 있는 고유의 이름이 필요합니다. 마이크로 서비스는 실행 중인 인프라와 독립적인 주소 지정 가능 이름이 필요 합니다. 즉, 서비스 레지스트리가 필요 하기 때문에 서비스를 배포 하는 방법 및 검색 방법 간에 상호 작용이 있음을 의미 합니다. 컴퓨터에 오류가 발생 하는 경우 레지스트리 서비스는 서비스를 이동할 위치를 알려 주어 야 합니다.

### <a name="remains-consistent-and-available-in-the-presence-of-failures"></a>일관되며 오류 시 사용 가능한 상태 유지

예기치 않은 오류를 처리하는 것은 특히 분산된 시스템에서는 가장 까다로운 문제 중 하나입니다. 개발자로 작성 하는 대부분의 코드는 예외를 처리 하기 위한 것입니다. 테스트 하는 동안 예외 처리에도 가장 많은 시간이 소요 됩니다. 프로세스는 오류를 처리 하는 코드를 작성 하는 것 보다 더 복잡 합니다. 마이크로 서비스가 실행 중인 컴퓨터가 실패 하는 경우 어떻게 되나요? 오류를 감지 해야 합니다 .이 문제는 자체에서 어려운 문제입니다. 하지만 마이크로 서비스를 다시 시작 해야 합니다.

가용성을 위해 마이크로 서비스는 오류에 대해 복원 력이 있어야 하 고 다른 컴퓨터에서 다시 시작할 수 있어야 합니다. 이러한 복원 력 요구 사항 외에도 데이터가 손실 되지 않으며 데이터가 일관 되 게 유지 되어야 합니다.

애플리케이션 업그레이드 중에 오류가 발생하면 복원력을 얻기가 어렵습니다. 배포 시스템과 작업하는 마이크로 서비스는 복구할 필요가 없습니다. 일관 된 상태를 유지 하기 위해 계속 최신 버전으로 이동 하거나 이전 버전으로 롤백할 수 있는지 여부를 결정 해야 합니다. 계속 진행할 수 있는 충분 한 컴퓨터가 있는지와 이전 버전의 마이크로 서비스를 복구 하는 방법 등 몇 가지 질문을 고려해 야 합니다. 이러한 결정을 내리기 위해 상태 정보를 마이크로 서비스 하는 데 필요 합니다.

### <a name="reports-health-and-diagnostics"></a>보고서 상태 및 진단

분명 한 것 처럼 보일 수 있으며, 마이크로 서비스는 상태와 진단을 보고 해야 합니다. 그렇지 않은 경우에는 운영 관점에서의 상태를 거의 파악 하지 못합니다. 일련의 독립적인 서비스를 통틀어 진단 이벤트 간의 상관 관계를 파악하고 이벤트 순서를 알기 위해 머신의 시간 차이를 이해하는 것은 어려운 작업입니다. 협의된 프로토콜과 데이터 형식을 통해 마이크로 서비스와 상호 작용하는 것과 같은 방식으로, 로그 상태와 진단 이벤트를 로깅하는 방법을 표준화해야 하며 이는 궁극적으로 쿼리 및 보기를 위한 이벤트 저장소로 귀결됩니다. 마이크로 서비스 접근 방식에서는 서로 다른 팀이 단일 로깅 형식에 동의 해야 합니다. 애플리케이션에서 진단 이벤트를 전체적으로 보는 데 일관된 접근 방식이 필요합니다.

상태는 진단과 다릅니다. 상태는 적절한 조치를 취하도록 마이크로 서비스가 현재 상태를 보고하는 것입니다. 좋은 예는 가용성 유지를 위한 업그레이드 및 배포 메커니즘과의 상호 작용입니다. 프로세스 충돌이 나 컴퓨터 재부팅으로 인해 현재 서비스가 비정상 상태가 될 수 있지만 서비스는 여전히 작동 하 고 있을 수 있습니다. 가장 중요 한 점은 업그레이드를 시작 하 여 상황을 악화 시키는 것입니다. 가장 좋은 방법은 먼저 조사 하거나 마이크로 서비스 복구할 시간을 허용 하는 것입니다. 마이크로 서비스의 상태 이벤트를 통해 정보에 입각한 의사 결정을 내리고 효과적인 자체 복구 서비스를 만들 수 있습니다.

## <a name="guidance-for-designing-microservices-on-azure"></a>Azure에서 마이크로 서비스를 설계 하는 방법에 대 한 지침

Azure [에서 마이크로 서비스를 설계 하 고 구축 하](https://docs.microsoft.com/azure/architecture/microservices/)는 방법에 대 한 지침은 azure 아키텍처 센터를 참조 하세요.

## <a name="service-fabric-as-a-microservices-platform"></a>마이크로 서비스 플랫폼으로서의 서비스 패브릭

Microsoft가 일반적으로 모놀리식 된 박스형 제품을 제공 하 여 서비스를 제공 하는 경우 Azure Service Fabric가 제공 됩니다. Azure SQL Database 및 Azure Cosmos DB 처럼 규모가 많은 서비스를 구축 하 고 운영 하는 환경은 Service Fabric. 플랫폼은 시간이 지남에 따라 더 많은 서비스를 채택 하 여 발전 했습니다. Service Fabric이 Azure뿐 아니라 독립 실행형 Windows Server 배포에서 실행되어야 했다는 점입니다.

***Service Fabric은 서비스를 빌드 및 실행 하 고 인프라 리소스를 효율적으로 사용 하기 위한 하드 문제를 해결 하는 것입니다. 따라서 팀은 마이크로 서비스 접근 방식을 사용 하 여 비즈니스 문제를 해결할 수 있습니다.***

Service Fabric은 마이크로 서비스 접근 방식을 사용하는 애플리케이션을 쉽게 빌드할 수 있도록 다음을 제공합니다.

* 실패한 서비스를 배포, 업그레이드, 검색 및 다시 시작하고 서비스를 검색하며 메시지를 라우팅하고 상태를 관리 및 모니터링하는 시스템 서비스를 제공하는 플랫폼입니다.
* 컨테이너 또는 프로세스로 실행 되는 응용 프로그램을 배포할 수 있습니다. Service Fabric은 컨테이너 및 프로세스 조정자입니다.
* 마이크로 서비스로 응용 프로그램을 빌드하는 데 유용한 생산적인 프로그래밍 Api: [ASP.NET Core, Reliable Actors 및 Reliable Services](service-fabric-choose-framework.md). 예를 들어 상태 및 진단 정보를 받거나 기본 제공되는 고가용성을 활용할 수 있습니다.

***Service Fabric은 서비스를 구축 하는 방법에 관계 없이 모든 기술을 사용할 수 있습니다. 하지만 마이크로 서비스를 쉽게 빌드할 수 있도록 하는 기본 제공 프로그래밍 Api를 제공 합니다.***

### <a name="migrating-existing-applications-to-service-fabric"></a>Service Fabric으로 기존 애플리케이션 마이그레이션

Service Fabric를 사용 하 여 기존 코드를 다시 사용 하 고 새 마이크로 서비스로 현대화 수 있습니다. 응용 프로그램 현대화 5 단계가 있으며 어떤 단계에서 든 지 시작 하 고 중지할 수 있습니다. 단계는 다음과 같습니다.

1) 기존의 모놀리식 애플리케이션을 시작합니다.  
2) 이송. 컨테이너 또는 게스트 실행 파일을 사용 하 여 Service Fabric에서 기존 코드를 호스팅합니다.  
3) 현대화. 기존 컨테이너 화 된 코드와 함께 새 마이크로 서비스를 추가 합니다.  
4) 혁신. 필요에 따라 모놀리식 응용 프로그램을 마이크로 서비스로 나눕니다.  
5) 응용 프로그램을 마이크로 서비스로 변환 합니다. 기존 모놀리식 응용 프로그램을 변환 하거나 새로운 최적의 응용 프로그램을 빌드합니다.

![마이크로 서비스로 마이그레이션][Image3]

*이러한 단계를 시작 하 고 중지할*수 있습니다. 다음 단계를 진행 하지 않아도 됩니다. 

이러한 각 단계에 대 한 예를 살펴보겠습니다.

**마이그레이션**  
여러 회사에서 기존 모놀리식 응용 프로그램을 컨테이너로 마이그레이션하는 두 가지 이유는 다음과 같습니다.

* 기존 하드웨어의 통합 및 제거 또는 더 높은 밀도로 응용 프로그램 실행으로 인 한 비용 절감
* 개발 및 운영 간의 일관된 배포 약속.

비용 절감은 간단 합니다. Microsoft에서 많은 기존 응용 프로그램을 컨테이너 화 된 하 고 있습니다. 일관 된 배포는 평가 하기 어렵고 동일 하 게 중요 합니다. 즉, 개발자가 해당 기능에 맞는 기술을 선택할 수 있지만, 작업은 응용 프로그램을 배포 하 고 관리 하는 단일 방법만을 허용 합니다. 개발자가 특정 항목만 선택 하도록 강요 하지 않고도 다양 한 기술을 지원 하기 위한 복잡성을 처리할 필요가 없습니다. 기본적으로 모든 응용 프로그램은 자체 포함 된 배포 이미지로 컨테이너 화 된 됩니다.

대부분의 조직에서는 여기까지만 수행합니다. 이러한 기능에는 이미 컨테이너의 이점이 있으며, Service Fabric는 배포, 업그레이드, 버전 관리, 롤백, 상태 모니터링 등을 비롯 한 완전 한 관리 환경을 제공 합니다.

**현대화**  
현대화는 기존 컨테이너 화 된 코드와 함께 새 서비스를 추가 하는 것입니다. 새 코드를 작성 하려는 경우 마이크로 서비스 경로에서 작은 단계를 수행 하는 것이 가장 좋습니다. 이는 새로운 REST API 끝점 또는 새로운 비즈니스 논리를 추가 하는 것을 의미할 수 있습니다. 이러한 방식으로 새 마이크로 서비스를 구축 하 고 개발 하 고 배포 하는 과정을 시작 합니다.

**혁신**  
마이크로 서비스 접근 방식은 변화하는 비즈니스 요구 사항을 수용합니다. 이 단계에서는 모놀리식 응용 프로그램을 서비스 또는 혁신 분할으로 시작할지 여부를 결정 해야 합니다. 여기에 나와 있는 일반적인 예는 워크플로 큐로 사용 하 고 있는 데이터베이스가 처리 병목 상태가 되는 경우입니다. 워크플로 요청의 수가 증가하므로 작업은 크기에 따라 배포되야 합니다. 크기를 조정 하지 않는 응용 프로그램의 특정 부분을 사용 하거나, 더 자주 업데이트 해야 하는 응용 프로그램의 특정 부분을 마이크로 서비스 및 혁신으로 분할 합니다.

**응용 프로그램을 마이크로 서비스로 변환**  
이 단계에서 응용 프로그램은 마이크로 서비스로 완전히 구성 되거나 분할 됩니다. 이 시점에 도달 하기 위해 마이크로 서비스를 진행 했습니다. 여기서는이 작업을 시작할 수 있지만, 마이크로 서비스 플랫폼 없이도이 작업을 수행 하려면 상당한 투자가 필요 합니다.

### <a name="are-microservices-right-for-my-application"></a>마이크로 서비스가 내 애플리케이션에 적합할까요?

아마도 그렇습니다. Microsoft에서 더 많은 팀이 비즈니스 상의 이유로 클라우드를 빌드하기 위해 빌드를 시작 했으므로 많은 팀이 마이크로 서비스 유사한 접근 방식을 사용 하는 이점을 실현 했습니다. 예를 들어 Bing은 몇 년간 마이크로 서비스를 사용 하 고 있습니다. 다른 팀의 경우 마이크로 서비스 접근 방식은 새로웠습니다. 팀은 핵심 역량이 아니면서 해결이 필요한 까다로운 문제를 찾았습니다. 이러한 이유 때문에 서비스를 빌드하기 위한 기술로 트랙 션을 얻을 Service Fabric 있습니다.

Service Fabric의 목적은 마이크로 서비스 응용 프로그램 빌드에 대 한 복잡성을 줄여 많은 비용이 드는 재설계을 거칠 필요가 없도록 하는 것입니다. 처음에는 소규모로 시작해서 고객의 사용량에 따라 확장하고, 서비스를 중단하고, 새 서비스를 추가하고, 발전해 가는 것이 바로 이 접근 방식입니다. 대부분의 개발자들이 더 쉽게 마이크로 서비스에 접근할 수 있게 하기 위해서는 아직 많은 문제들을 해결해야 한다는 점도 알고 있습니다. 컨테이너와 행위자 프로그래밍 모델은 해당 방향의 작은 단계에 대 한 예입니다. 마이크로 서비스 접근 방식을 더 쉽게 만들기 위해 더 많은 혁신을 제공 하 고 있습니다.

## <a name="next-steps"></a>다음 단계

* [마이크로 서비스: 클라우드가 지원하는 애플리케이션 혁명](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/)
* [Azure 아키텍처 센터: Azure에서 마이크로 서비스 구축](https://docs.microsoft.com/azure/architecture/microservices/)
* [Azure Service Fabric 응용 프로그램 및 클러스터 모범 사례](service-fabric-best-practices-overview.md)
* [서비스 패브릭 용어 개요](service-fabric-technical-overview.md)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png

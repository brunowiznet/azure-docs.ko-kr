---
title: 샘플 - 스토리지 계정에 대한 HTTPS 트래픽 확인
description: 이 샘플 정책 정의에서는 모든 Azure 스토리지 계정이 보안 HTTPS 트래픽만 허용하도록 요구됩니다.
ms.date: 01/23/2019
ms.topic: sample
ms.openlocfilehash: 4d6b6f7e494d2f8c5278c546ead1f9697f245f38
ms.sourcegitcommit: 95931aa19a9a2f208dedc9733b22c4cdff38addc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74463596"
---
# <a name="sample---ensure-https-traffic-only-for-storage-account"></a>샘플 - 스토리지 계정에 대해서만 HTTPS 트래픽 확인

이 정책에서는 스토리지 계정이 HTTPS 트래픽을 사용해야 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>샘플 템플릿

[!code-json[main](../../../../policy-templates/samples/Storage/https-traffic-only/azurepolicy.json "Ensure https traffic only for storage account")]

[PowerShell](#deploy-with-powershell) 또는 [Azure CLI](#deploy-with-azure-cli)와 함께 [Azure Portal](#deploy-with-the-portal)을 사용하여 이 템플릿을 배포할 수 있습니다.

## <a name="deploy-with-the-portal"></a>포털을 사용하여 배포

[![Azure에 Policy 샘플 배포](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FStorage%2Fhttps-traffic-only%2Fazurepolicy.json)

## <a name="deploy-with-powershell"></a>PowerShell을 사용하여 배포

[!INCLUDE [sample-powershell-install](../../../../includes/sample-powershell-install-no-ssh-az.md)]

```azurepowershell-interactive
$definition = New-AzPolicyDefinition -Name "https-traffic-only" -DisplayName "Ensure https traffic only for storage account" -description "Ensure https traffic only for storage account" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Storage/https-traffic-only/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Storage/https-traffic-only/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a>PowerShell 배포 정리

다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurepowershell-interactive
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a>Azure CLI를 사용하여 배포

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'https-traffic-only' --display-name 'Ensure https traffic only for storage account' --description 'Ensure https traffic only for storage account' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Storage/https-traffic-only/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Storage/https-traffic-only/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "https-traffic-only"
```

### <a name="clean-up-azure-cli-deployment"></a>Azure CLI 배포 정리

다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a>다음 단계

- [Azure Policy 샘플](index.md)에서 더 많은 샘플 검토
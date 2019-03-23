---
title: Administrador de conexiones de Azure Resource Manager | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55f7aaaa80992240468f3a94d6fd3b9a0f8807b9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388533"
---
# <a name="azure-resource-manager-connection-manager"></a>Administrador de conexiones de Azure Resource Manager
El **Administrador de conexiones de Azure Resource Manager** permite que un paquete SSIS administre los recursos de Azure con una [entidad de servicio](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

Para crear y configurar un **Administrador de conexiones de Azure Resource Manager**, siga estos pasos:

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureResourceManager** y haga clic en **Agregar**.
2. En el cuadro de diálogo **Azure Resource Manager Connection Manager Editor** (Editor del Administrador de conexiones de Azure Resource Manager), especifique el **id. de aplicación**, la **clave de aplicación** y el **id. de inquilino** de la entidad de servicio. Para obtener más información acerca de estas propiedades, consulte [este](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) artículo.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .

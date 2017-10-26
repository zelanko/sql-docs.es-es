---
title: Administrador de conexiones de administrador de recursos Azure | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Administrador de conexiones de Azure Resource Manager
El **Administrador de conexiones de administrador de recursos de Azure** permite que un paquete SSIS administrar recursos de Azure con un [entidad de servicio](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).

El **Administrador de conexiones de administrador de recursos de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para crear y configurar un **Administrador de conexiones de administrador de recursos de Azure**, siga estos pasos:

1. En el **Agregar administrador de conexiones SSIS** cuadro de diálogo, seleccione **AzureResourceManager**y haga clic en **agregar**.
2. En el **Editor del Administrador de conexiones del Administrador de recursos de Azure** diálogo cuadro, especifique la **Id. de aplicación**, **clave de aplicación**, y **Id. de inquilino** para la entidad de servicio. Para obtener más información acerca de estas propiedades, consulte [esto](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) artículo.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .


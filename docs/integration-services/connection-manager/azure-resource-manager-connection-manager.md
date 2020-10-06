---
description: Administrador de conexiones de Azure Resource Manager
title: Administrador de conexiones de Azure Resource Manager | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 84b9c97935d0bcf89a4741304bb9a1e6b3576605
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726036"
---
# <a name="azure-resource-manager-connection-manager"></a>Administrador de conexiones de Azure Resource Manager

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


El **Administrador de conexiones de Azure Resource Manager** permite que un paquete SSIS administre los recursos de Azure con una [entidad de servicio](/azure/azure-resource-manager/resource-group-create-service-principal-portal).

El **Administrador de conexiones de Azure Resource Manager** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para crear y configurar un **Administrador de conexiones de Azure Resource Manager**, siga estos pasos:

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureResourceManager** y haga clic en **Agregar**.
2. En el cuadro de diálogo **Azure Resource Manager Connection Manager Editor** (Editor del Administrador de conexiones de Azure Resource Manager), especifique el **id. de aplicación**, la **clave de aplicación** y el **id. de inquilino** de la entidad de servicio. Para obtener más información acerca de estas propiedades, consulte [este](/azure/azure-resource-manager/resource-group-create-service-principal-portal) artículo.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .
---
description: Administrador de conexiones de Azure HDInsight
title: Administrador de conexiones de Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 6acb9fec83da610246001df5bc68591ecab1a225
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130146"
---
# <a name="azure-hdinsight-connection-manager"></a>Administrador de conexiones de Azure HDInsight

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


El **Administrador de conexiones de Azure HDInsight** permite que un paquete SSIS se conecte a un clúster de Azure HDInsight.

El **Administrador de conexiones de Azure HDInsight** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para crear y configurar un **Administrador de conexiones de Azure HDInsight**, siga estos pasos:

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureHDInsight** y haga clic en **Agregar**.
2. En el cuadro de diálogo **Azure HDInsight Connection Manager Editor** (Editor del Administrador de conexiones de Azure HDInsight), especifique el **nombre DNS del clúster** (sin el prefijo del protocolo), el **nombre de usuario** y la **contraseña** para conectar el clúster de HDInsight.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .

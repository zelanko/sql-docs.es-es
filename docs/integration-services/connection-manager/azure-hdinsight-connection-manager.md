---
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
ms.openlocfilehash: c57abdf2cd6fbdf5cbb0953f1604440d714e1e7e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67968255"
---
# <a name="azure-hdinsight-connection-manager"></a>Administrador de conexiones de Azure HDInsight

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


El **Administrador de conexiones de Azure HDInsight** permite que un paquete SSIS se conecte a un clúster de Azure HDInsight.

El **Administrador de conexiones de Azure HDInsight** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para crear y configurar un **Administrador de conexiones de Azure HDInsight**, siga estos pasos:

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureHDInsight** y haga clic en **Agregar**.
2. En el cuadro de diálogo **Azure HDInsight Connection Manager Editor** (Editor del Administrador de conexiones de Azure HDInsight), especifique el **nombre DNS del clúster** (sin el prefijo del protocolo), el **nombre de usuario** y la **contraseña** para conectar el clúster de HDInsight.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .

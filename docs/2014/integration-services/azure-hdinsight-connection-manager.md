---
title: Administrador de conexiones de Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPHDICM.F1
- SQL11.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 850a978d-5dba-45b6-a10e-306aafbc353d
caps.latest.revision: 2
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 3d9486108e7f16870d2bf4e22f05b8a0a288b664
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112313"
---
# <a name="azure-hdinsight-connection-manager"></a>Administrador de conexiones de Azure HDInsight
El **Administrador de conexiones de Azure HDInsight** permite que un paquete SSIS se conecte a un clúster de Azure HDInsight.

Para crear y configurar un **Administrador de conexiones de Azure HDInsight**, siga estos pasos:

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureHDInsight** y haga clic en **Agregar**.
2. En el cuadro de diálogo **Azure HDInsight Connection Manager Editor** (Editor del Administrador de conexiones de Azure HDInsight), especifique el **nombre DNS del clúster** (sin el prefijo del protocolo), el **nombre de usuario** y la **contraseña** para conectar el clúster de HDInsight.
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .
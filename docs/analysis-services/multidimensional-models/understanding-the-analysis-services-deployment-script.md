---
title: Descripción de los análisis de servicios de Script de implementación | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6be56539605946468b1c2e2700e2c65841018a4d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Descripción del script de implementación de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El script de implementación XMLA generado por el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está formado por dos secciones:  
  
-   La primera parte del script de implementación contiene los comandos necesarios para crear, modificar o eliminar los objetos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondientes de la base de datos de destino. De forma predeterminada, los archivos de entrada generados por el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se basan en una implementación incremental. En consecuencia, el script de implementación XMLA solamente afectará a los objetos que se cambiaron o se eliminaron.  
  
-   La segunda parte del script de implementación contiene los comandos necesarios para procesar únicamente los objetos creados o modificados en el servidor de destino (opción Procesar predeterminado) o para procesar completamente la base de datos de destino. Además, puede elegir que el script de implementación no contenga comandos de procesamiento.  
  
 El script de implementación completa se puede ejecutar en una única transacción o en varias transacciones. Si el script se ejecuta en varias transacciones, la primera parte del mismo se ejecuta en una única transacción y cada objeto se procesa en su propia transacción.  
  
> [!IMPORTANT]  
>  El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solamente implementa los objetos en una sola base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No implementa ningún objeto o datos en el nivel de servidor.  
  
## <a name="see-also"></a>Vea también  
 [Ejecuta al Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Descripción de los archivos de entrada utilizados para crear el Script de implementación](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  

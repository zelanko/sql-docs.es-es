---
title: "Cambie el valor de tiempo de espera para las consultas de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 51603c1919fae5e164348181412712d4dfc673a0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Cambiar el valor del tiempo de espera para las consultas de minería de datos
  Al generar un gráfico de elevación o ejecutar una consulta de predicción, en ocasiones se necesita mucho tiempo para generar todos los datos requeridos para la predicción. Para evitar que se exceda el tiempo de espera de la consulta, puede cambiar el valor que controla cuánto tiempo debe esperar el servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para completar una consulta.  
  
 El valor predeterminado es 15; sin embargo, si sus modelos son complejos o el origen de datos es grande, puede no ser suficiente. Si es necesario, puede aumentar significativamente el valor para dejar tiempo suficiente para los procesos. Por ejemplo, si establece **Tiempo de espera de la consulta** en 600, la consulta podría seguir ejecutándose hasta un tiempo máximo de 10 minutos.  
  
 Para más información sobre las consultas de predicción, vea [Tareas y procedimientos de Consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Configurar el valor del tiempo de espera para las consultas de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el menú **Herramientas** , seleccione **Opciones**.  
  
2.  En el panel **Opciones** , expanda **Diseñadores de Business Intelligence**.  
  
3.  Haga clic en el cuadro de texto **Tiempo de espera de la consulta** y escriba un valor para el número de segundos.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de Consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
  


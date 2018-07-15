---
title: Los parámetros utilizados para crear un modelo de minería de datos de consulta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: ce7719e0-6127-4d9c-a753-0e0a3db065e1
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee19f34f99c51bd1747718e5d34fd6ab12fe3e49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288351"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>Consultar los parámetros usados para crear un modelo de minería de datos
  La composición de un modelo de minería de datos no solo se ve afectada por los casos de entrenamiento, sino también por los parámetros que se establecieron al crear el modelo. Por lo tanto, es posible que la recuperación de la configuración de parámetros de un modelo existente resulte de utilidad para comprender mejor el comportamiento del modelo. La recuperación de parámetros también resulta útil al documentar una versión determinada del modelo.  
  
 Para buscar los parámetros que se utilizaron al crear el modelo, cree una consulta en uno de los conjuntos de filas de esquema del modelo de minería de datos. En [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], estos conjuntos de filas de esquema se exponen como un conjunto de vistas del sistema que se pueden consultar fácilmente mediante la sintaxis de Transact-SQL. Este procedimiento describe cómo crear una consulta que devuelva los parámetros que se utilizaron para crear el modelo de minería de datos especificado.  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>Para abrir una ventana Consulta para una consulta de conjunto de filas de esquema  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene el modelo que desea consultar.  
  
2.  Haga clic con el botón derecho en el nombre de la instancia, seleccione **Nueva consulta**y, después, seleccione **DMX**.  
  
    > [!NOTE]  
    >  También puede crear una consulta en un modelo de minería de datos usando la plantilla **MDX** .  
  
3.  Si la instancia contiene varias bases de datos, seleccione la base de datos que contiene el modelo que desea consultar en la lista **Bases de datos disponibles** de la barra de herramientas.  
  
### <a name="to-return-model-parameters-for-an-existing-mining-model"></a>Para devolver los parámetros de un modelo de minería de datos existente  
  
1.  En el panel de consulta DMX, escriba o pegue el texto siguiente:  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  En el Explorador de objetos, seleccione el modelo de minería de datos que desee y, a continuación, arrástrelo hasta el panel Consulta DMX y sitúelo entre las comillas simples.  
  
3.  Presione F5 o haga clic en **Ejecutar**.  
  
## <a name="example"></a>Ejemplo  
 El código siguiente devuelve una lista de los parámetros que se utilizaron para crear el modelo de minería de datos generado en el [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md). Estos parámetros incluyen los valores explícitos para cualquier parámetro predeterminado utilizado por los servicios de minería de datos ofrecidos por los proveedores en el servidor.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 En el ejemplo de código se devuelven los parámetros siguientes para el modelo de agrupación en clústeres:  
  
 Resultados del ejemplo:  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## <a name="see-also"></a>Vea también  
 [Tareas de consulta de minería de datos y procedimientos](data-mining-query-tasks-and-how-tos.md)   
 [Consultas de minería de datos](data-mining-queries.md)  
  
  

---
title: "Crear una consulta de contenido en un modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 03b5c96e3a435a757fdb1bc8f83b2d1b093ed224
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-content-query-on-a-mining-model"></a>Crear una consulta de contenido en un modelo de minería de datos
  Puede consultar mediante programación el contenido del modelo de minería de datos utilizando AMO o XML/A, pero crear las consultas mediante DMX resulta más fácil. También puede crear consultas con los conjuntos de filas de esquema de minería de datos estableciendo una conexión a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y crear una consulta mediante la DMV que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los procedimientos siguientes muestran cómo crear consultas con un modelo de minería de datos utilizando DMX y cómo consultar los conjuntos de filas del esquema de minería de datos.  
  
 Para obtener un ejemplo de cómo crear una consulta similar con XML/A, vea [Crear una consulta de minería de datos utilizando XMLA](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>Consultar el contenido del modelo de minería de datos con DMX  
  
#### <a name="to-create-a-dmx-model-content-query"></a>Para crear una consulta de contenido del modelo DMX  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  En el panel **Explorador de plantillas** , haga clic en el icono de cubo para cambiar la lista y mostrar las plantillas de Analysis Services.  
  
3.  En la lista de categorías de plantilla, expanda **DMX**, expanda **Contenido del modelo**y haga doble clic en **Consulta de contenido**.  
  
4.  En el cuadro de diálogo **Conectar a Analysis Services** , seleccione la instancia que contiene el modelo de minería de datos que desea consultar y haga clic en **Conectar**.  
  
     La plantilla **Consulta de contenido** se abre en el editor de código adecuado. El panel de metadatos muestra los modelos que están disponibles en la base de datos actual. Para cambiar la base de datos, seleccione una diferente en la lista **Bases de datos disponibles** .  
  
5.  Escriba el nombre de un modelo de minería de datos en la línea, `FROM` [*\<el modelo de minería de datos, nombre, MiModelo >*]`.CONTENT`. Si el nombre del modelo de minería de datos contiene espacios, debe escribirse entre corchetes.  
  
     Si no desea escribir el nombre, puede seleccionar un modelo de minería de datos en el **Explorador de objetos** y arrastrarlo a la plantilla.  
  
6.  En la línea, `SELECT`  *\<lista de selección, lista de expresión, \* >* , escriba los nombres de columnas en el conjunto de filas de esquema de contenido de modelo de minería de datos.  
  
     Para obtener una lista de las columnas que puede devolver en las consultas de contenido del modelo de minería de datos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
7.  Opcionalmente, escriba una condición en la cláusula WHERE de la plantilla para restringir las filas que se devuelven para nodos o valores concretos.  
  
8.  Haga clic en **Ejecutar**.  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>Consultar los conjuntos de filas de esquema de minería de datos  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>Para crear una consulta con el conjunto de filas de esquema de minería de datos  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en la barra de herramientas **Nueva consulta** , haga clic en **Consulta DMX de Analysis Services**o **Consulta MDX de Analysis Services**.  
  
2.  En el cuadro de diálogo **Conectar a Analysis Services** , seleccione la instancia que contiene los objetos que desea consultar y haga clic en **Conectar**.  
  
     La plantilla **Consulta de contenido** se abre en el editor de código adecuado. El panel de metadatos muestra los objetos que están disponibles en la base de datos actual. Para cambiar la base de datos, seleccione una diferente en la lista **Bases de datos disponibles** .  
  
3.  En el editor de consultas, escriba lo siguiente:  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  Haga clic en **Ejecutar**.  
  
     El panel Resultados muestra el contenido del modelo.  
  
    > [!NOTE]  
    >  Para ver una lista de todos los conjuntos de filas de esquema que puede consultar en la instancia actual, use esta consulta: `SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS. O bien, para obtener una lista de conjuntos de filas de esquema concretos de la minería de datos, vea [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md).  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Conjuntos de filas de esquema de minería de datos](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  


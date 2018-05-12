---
title: Crear una consulta de contenido en un modelo de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a0bc8d9a216f55f04cab4a4012945d2b11cf429
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-content-query-on-a-mining-model"></a>Crear una consulta de contenido en un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
6.  En la línea, `SELECT` *\<lista de selección, lista de expresión, \* >*, escriba los nombres de columnas en el conjunto de filas de esquema de contenido de modelo de minería de datos.  
  
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
 [Contenido del modelo de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Conjuntos de filas de esquema de minería de datos](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

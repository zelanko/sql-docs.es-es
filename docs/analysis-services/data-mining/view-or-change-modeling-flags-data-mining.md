---
title: "Ver o cambiar marcas de modelado (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbffc4a5312dc83976915653141247d27dc8eae4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="view-or-change-modeling-flags-data-mining"></a>Ver o cambiar marcas de modelado (minería de datos)
  Las marcas de modelado son propiedades que se activan en una columna de estructura de minería de datos o columnas de modelo de minería de datos para controlar cómo procesa los datos el algoritmo durante el análisis.  
  
 En el Diseñador de minería de datos, puede ver y modificar las marcas de modelado asociadas a una estructura de minería de datos o a una columna de minería de datos examinando las propiedades de la estructura o del modelo. También puede establecer las marcas de modelado utilizando DMX, AMO o XMLA.  
  
 Este procedimiento describe cómo cambiar las marcas de modelado en el diseñador.  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>Ver o cambiar la marca de modelado de una columna de la estructura o columna del modelo  
  
1.  En SQL Server Design Studio, abra el Explorador de soluciones y, a continuación, haga doble clic en la estructura de minería de datos.  
  
2.  Para establecer la marca de modelado NOT NULL, haga clic en la pestaña **Estructura de minería de datos** . Para establecer las marcas REGRESSOR o MODEL_EXISTENCE_ONLY, haga clic en la pestaña **Modelo de minería de datos** .  
  
3.  Haga clic con el botón derecho en la columna que quiere ver o cambiar y seleccione **Propiedades**.  
  
4.  Para agregar una nueva marca de modelado, haga clic en el cuadro de texto situado junto a la propiedad **ModelingFlags** y active la casilla o casillas de las marcas de modelado que desea utilizar.  
  
     Las marcas de modelado solo se muestran si son adecuadas para el tipo de datos de la columna.  
  
    > [!NOTE]  
    >  Después de cambiar una marca de modelado, debe volver a procesar el modelo.  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>Obtener las marcas de modelado utilizadas en el modelo  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una ventana Consulta DMX y escriba una consulta como la siguiente:  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  

---
title: Crear una estructura de modelos de minería de datos de clústeres de secuencia (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63273478"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>Crear una estructura del modelo de minería de datos de agrupación en clústeres de secuencia (Tutorial intermedio de minería de datos)
  El primer paso para crear un modelo de minería de datos de agrupación en clústeres de secuencia es utilizar el Asistente para minería de datos con el objeto de crear una nueva estructura de minería de datos y un modelo de minería basados en el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Utilizará la misma vista del origen de datos que utilizó para el análisis de la cesta de la compra, pero agregará una columna que contenga el identificador `sequence`. En este escenario, la secuencia significa el orden en el que el cliente agregó los elementos a la cesta de la compra.  
  
 También agregará algunas columnas que se utilizan en uno de los modelos para agrupar los clientes por datos demográficos.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>Para crear un modelo y una estructura de agrupación en clústeres de secuencia  
  
1.  En Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic con el botón secundario en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos**.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **seleccionar el método de definición** , compruebe que la opción **de base de datos relacional o del almacenamiento de datos existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **crear la estructura de minería de datos** , compruebe que está seleccionada la opción **crear estructura de minería de datos con un modelo de minería de** datos. A continuación, haga clic en la lista desplegable de la opción **¿qué técnica de minería de datos desea utilizar?** y seleccione **agrupación en clústeres de secuencia de Microsoft**. Haga clic en **Siguiente**.  
  
     Aparece la página **seleccionar vista del origen de datos** . En **vistas del origen de datos disponibles**, seleccione `Orders`.  
  
     Orders es la misma vista del origen de datos que utilizó para el escenario de la cesta de la compra. Si no ha creado esta vista del origen de datos, vea [Agregar una vista del origen de datos con tablas anidadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md).  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **especificar tipos de tablas** , active la casilla de verificación de **mayúsculas y minúsculas** junto a la tabla **VAssocSeqOrders** y active la casilla **anidada** junto a la tabla **vAssocSeqLineItems** . Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si se produce un error al activar las **casillas de verificación de** **mayúsculas o minúsculas** , es posible que la combinación de la vista del origen de datos no sea correcta. La tabla anidada, **vAssocSeqLineItems**, debe estar conectada a la tabla de casos, **vAssocSeqOrders,** por una combinación de varios a uno. Puede modificar la relación haciendo clic con el botón secundario en la línea de combinación e invirtiendo entonces la dirección de la unión. Para obtener más información, vea [cuadro de diálogo crear o editar relación &#40;Analysis Services-&#41;de datos multidimensionales ](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md).  
  
7.  En la página **especificar los datos de entrenamiento** , elija las columnas que se van a usar en el modelo activando una casilla como se indica a continuación:  
  
    -   **IncomeGroup** Active la casilla **entrada** .  
  
         Esta columna contiene información interesante sobre los clientes que puede utilizar para la agrupación en clústeres. La utilizará en el primer modelo y, a continuación, la omitirá en el segundo.  
  
    -   **OrderNumber** Active la `Key` casilla.  
  
         Este campo se utilizará como identificador para la tabla de casos o `Key`. En general, nunca debería utilizar el campo clave de la tabla de casos como una entrada, porque la clave contiene valores únicos que no son útiles para la agrupación en clústeres.  
  
    -   **Región** de Active la casilla **entrada** .  
  
         Esta columna contiene información interesante sobre los clientes que puede utilizar para la agrupación en clústeres. La utilizará en el primer modelo y, a continuación, la omitirá en el segundo.  
  
    -   **LineNumber** Active las `Key` **casillas de verificación y** .  
  
         El campo **lineNumber** se usará como el identificador de la tabla anidada o `Sequence Key`. La clave para una tabla anidada siempre se debe utilizar para la entrada.  
  
    -   **Modelo** de Active las casillas de verificación de **entrada** y de **predicción** .  
  
     Compruebe que las selecciones sean correctas y, a continuación, haga clic en **siguiente**.  
  
8.  En la página **especificar el contenido y el tipo de datos de las columnas** , compruebe que la cuadrícula contiene las columnas, los tipos de contenido y los tipos de datos que se muestran en la tabla siguiente y, a continuación, haga clic en **siguiente**.  
  
    |Tablas y columnas|Tipo de contenido|Tipo de datos|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |OrderNumber|Key|Text|  
    |Region|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |Line Number|Key Sequence|long|  
    |Modelo|Discrete|Text|  
  
9. En la página **crear conjunto de pruebas** , cambie el **porcentaje de datos de prueba** a 20 y, a continuación, haga clic en **siguiente**.  
  
10. En la página **finalización del asistente** , en **nombre**de la estructura de `Sequence Clustering with Region`minería de datos, escriba.  
  
11. En el **nombre del modelo**de minería `Sequence Clustering with Region`de datos, escriba.  
  
12. Active la casilla **permitir obtención de detalles** y, a continuación, haga clic en **Finalizar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Procesar el modelo de agrupación en clústeres de secuencia](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo de clústeres de secuencia de Microsoft](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  

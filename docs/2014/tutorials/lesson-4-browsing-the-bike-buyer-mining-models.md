---
title: 'Lección 4: Examinar los modelos de minería de Bike Buyer | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63070979"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>Lección 4: Examen de los modelos de minería de datos de Bike Buyer
  En esta lección, usará el [SELECT (DMX)](/sql/dmx/select-dmx) instrucción para explorar el contenido en el árbol de decisión y agrupación en clústeres de minería de datos que haya creado en los modelos [lección 2: Agregar modelos de minería de datos a la estructura de minería de datos predictivos](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Las columnas incluidas en un modelo de minería de datos no son las columnas definidas por la estructura de minería de datos, sino un conjunto específico de columnas que describen las tendencias y los patrones encontrados por el algoritmo. Estas columnas del modelo de minería de datos se describen en la [de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset) de filas de esquema. Por ejemplo, la columna MODEL_NAME del conjunto de filas del esquema de contenido incluye el nombre del modelo de minería de datos. Para un modelo de minería de datos de agrupación en clústeres, la columna NODE_CAPTION contiene el nombre de cada clúster y la columna NODE_DESCRIPTION, una descripción de las características de cada clúster. Puede examinar estas columnas mediante el uso de SELECT FROM \<modelo >. Instrucción contenido en DMX. También puede utilizar esta instrucción para explorar los datos utilizados para crear el modelo de minería de datos. La obtención de detalles debe estar habilitada en la estructura de minería de datos para poder usar esta instrucción. Para obtener más información acerca de la instrucción, consulte [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
 También se pueden devolver todos los estados de una columna discreta mediante la instrucción SELECT DISTINCT. Por ejemplo, si realiza esta operación en una columna que contiene géneros, la consulta devolverá `male` y `female`.  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Explorar el contenido incluido en los modelos de minería de datos  
  
-   Devolver los casos de los datos de origen utilizados para entrenar los modelos de minería de datos  
  
-   Explorar los distintos estados disponibles para una columna discreta específica  
  
## <a name="returning-the-content-of-a-mining-model"></a>Devolver el contenido de un modelo de minería de datos  
 En esta lección, usará el [SELECT FROM &#60;modelo&#62;. CONTENIDO &#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx) instrucción para devolver el contenido del modelo de agrupación en clústeres.  
  
 El siguiente es un ejemplo genérico de SELECT FROM \<modelo >. Instrucción de contenido:  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 En la primera línea del código se definen las columnas que deben devolverse a partir del contenido del modelo de minería de datos y el modelo de minería de datos al que están asociadas:  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 La cláusula .CONTENT junto al nombre del modelo de minería de datos especifica que se devuelve el contenido del modelo de minería de datos. Para obtener más información acerca de las columnas contenidas en el modelo de minería de datos, vea [de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Opcionalmente, puede utilizar la última línea del código para filtrar los resultados devueltos por la instrucción:  
  
```  
WHERE <where clause>  
```  
  
 Por ejemplo, si desea restringir los resultados de la consulta a solo los clústeres que contengan un gran número de casos, puede agregar la siguiente cláusula WHERE a la instrucción SELECT:  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 Para obtener más información sobre el uso de la instrucción WHERE, vea [seleccione &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>Para devolver el contenido del modelo de minería de datos de agrupación en clústeres  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de SELECT FROM \<modelo >. Instrucción de contenido en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    *  
    ```  
  
     También puede reemplazar * con una lista de cualquiera de las columnas contenidas en el [de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Clustering]  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
6.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `SELECT_CONTENT.dmx`.  
  
7.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve el contenido del modelo de minería de datos.  
  
## <a name="use-drillthrough"></a>Usar la obtención de detalles  
 El paso siguiente es usar la instrucción de obtención de detalles para devolver el muestreo de los casos utilizados para entrenar el modelo de minería de datos del árbol de decisión. En esta lección, usará el [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx) instrucción para devolver el contenido del modelo de árbol de decisión.  
  
 El siguiente es un ejemplo genérico de SELECT FROM \<modelo >. Instrucción de casos:  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 En la primera línea del código se definen las columnas que deben devolverse a partir de los datos de origen y el modelo de minería de datos en el que se incluyen:  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 La cláusula .CASES especifica que se está realizando una consulta de obtención de detalles. Para poder utilizar la obtención de detalles, debe habilitarla al crear el modelo de minería de datos.  
  
 La última línea del código es opcional y especifica el nodo del modelo de minería de datos del que se solicitan casos:  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 Para obtener más información sobre el uso de la instrucción WHERE con IsInNode, vea [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>Para devolver los casos utilizados para entrenar el modelo de minería de datos  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de SELECT FROM \<modelo >. Instrucción de los casos en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    *  
    ```  
  
     También puede reemplazar * por una lista de las columnas incluidas dentro de los datos de origen (como [Bike Buyer]).  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
6.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `SELECT_DRILLTHROUGH.dmx`.  
  
7.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve los datos de origen utilizados para entrenar el modelo de minería de datos del árbol de decisión.  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>Devolver los estados de una columna discreta del modelo de minería de datos  
 El paso siguiente es utilizar la instrucción SELECT DISTINCT para devolver los distintos estados posibles en la columna del modelo de minería de datos que se ha especificado.  
  
 A continuación, se incluye un ejemplo genérico de la instrucción SELECT DISTINCT:  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 En la primera línea del código se definen las columnas del modelo de minería de datos para las que se devolverán estados:  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 Debe incluir DISTINCT para devolver todos los estados de la columna. Si no incluye DISTINCT, la instrucción completa se convierte en un acceso directo para una predicción y devuelve el estado más probable de la columna especificada. Para más información, vea [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>Para devolver los estados de una columna discreta  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción SELECT DISTINCT en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    [<column,name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
6.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `SELECT_DISCRETE.dmx`.  
  
7.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve los estados posibles de la columna Bike Buyer.  
  
 En la siguiente lección predecirá si los clientes potenciales serán compradores de bicicletas, utilizando el modelo de minería de datos del árbol de decisión.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 5: Ejecutar consultas de predicción](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  

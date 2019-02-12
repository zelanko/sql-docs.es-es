---
title: 'Lección 3: Procesar la estructura de minería de datos Market Basket | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018267"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>Lección 3: Procesar la estructura de minería de datos Market Basket
  En esta lección, usará el [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrucción y el vAssocSeqLineItems y vAssocSeqOrders de la [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] modelos de datos de ejemplo para procesar las estructuras de minería de datos y la minería de datos creado en [lección 1: Creación de la estructura de minería de datos Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md) y [lección 2: Agregar modelos de minería de datos a la estructura de minería de datos Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md).  
  
 Al procesar una estructura de minería de datos, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lee los datos de origen y genera las estructuras que admiten los modelos de minería de datos. Al procesar un modelo de minería de datos, los datos definidos por la estructura de minería de datos se pasan por el algoritmo de minería de datos que haya elegido. El algoritmo busca tendencias y patrones y, a continuación, almacena esta información en el modelo de minería de datos. Por consiguiente, el modelo de minería de datos no contiene los datos de origen reales, sino la información descubierta por el algoritmo. Para obtener más información acerca de cómo procesar modelos de minería de datos, vea [consideraciones y requisitos de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Solo debe volver a procesar una estructura de minería de datos si cambia una columna de la estructura o los datos de origen. Si agrega un modelo de minería de datos a una estructura de minería de datos que ya se ha procesado, puede usar la instrucción `INSERT INTO MINING MODEL` para entrenar el nuevo modelo de minería de datos en los datos existentes.  
  
 La estructura de minería de datos Market Basket contiene una tabla anidada, por lo que deberá definir las columnas de minería de datos que deben entrenarse usando la estructura de tablas anidadas y usar el comando `SHAPE` para definir las consultas que extraen los datos de aprendizaje de las tablas de origen.  
  
## <a name="insert-into-statement"></a>Instrucción INSERT INTO  
 Con el fin de entrenar la estructura de minería de datos Market Basket y los modelos de minería de datos asociados, use el [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrucción. El código de la instrucción se puede dividir en las partes siguientes.  
  
-   Identificación de la estructura de minería de datos  
  
-   Visualización en una lista de las columnas de la estructura de minería de datos  
  
-   Definición de los datos de aprendizaje con `SHAPE`  
  
 A continuación, se incluye un ejemplo genérico de la instrucción `INSERT INTO`:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 La primera línea del código identifica la estructura de minería de datos que se entrenará:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 Las líneas siguientes del código especifican las columnas definidas por la estructura de minería de datos. Debe incluir en la lista cada una de las columnas de la estructura de minería de datos, y cada columna debe estar asignada a una columna incluida en los datos de la consulta de origen: Puede usar `SKIP` para omitir columnas de los datos de origen que no existen en la estructura de minería de datos. Para obtener más información sobre cómo usar `SKIP`, consulte [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx).  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 Las últimas líneas del código definen los datos que se utilizarán para entrenar la estructura de minería de datos. Los datos de origen se incluyen en dos tablas, por lo que usará `SHAPE` para relacionar estas tablas.  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 En esta lección usará `OPENQUERY` para definir los datos de origen. Para obtener información acerca de otros métodos de definir una consulta en el origen de datos, vea [ &#60;consulta de origen de datos&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará la tarea siguiente:  
  
-   Procesar la estructura de minería de datos Market Basket  
  
## <a name="processing-the-market-basket-mining-structure"></a>Procesar la estructura de minería de datos Market Basket  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Para procesar la estructura de minería de datos con INSERT INTO  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción INSERT INTO en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    [<mining structure>]  
    ```  
  
     por:  
  
    ```  
    Market Basket  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     por:  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     En la instrucción, `Products` hace referencia a la tabla Products definida por la instrucción SHAPE. `SKIP` se usa para omitir la columna Model, que se encuentra en el origen de datos como clave, pero no la usa la estructura de minería de datos.  
  
5.  Reemplace lo siguiente:  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     por:  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     Las referencias de la consulta de origen el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] origen de datos definido en el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] proyecto de ejemplo. Utiliza este origen de datos para obtener acceso a las vistas vAssocSeqLineItems y vAssocSeqOrders. Estas vistas contienen los datos de origen que se utilizarán para entrenar el modelo de minería de datos. Si no ha creado este proyecto o estas vistas, consulte [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
     En el comando `SHAPE`, usará `OPENQUERY` para definir dos consultas. La primera consulta define la tabla primaria y la segunda, la tabla anidada. Las dos tablas se relacionan mediante la columna OrderNumber, que existe en ambas tablas.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
7.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Process Market Basket.dmx`.  
  
8.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
 Después de que la consulta haya terminado de ejecutarse, puede ver los modelos y los conjuntos de elementos encontrados, ver asociaciones o filtrar por conjunto de elementos, probabilidad o importancia. Para ver esta información, en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic en el nombre del modelo de datos y, a continuación, haga clic en **examinar**.  
  
 En la siguiente lección creará varias predicciones basadas en los modelos de minería de datos que ha agregado a la estructura Market Basket.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Predicciones de cesta de la ejecución](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  

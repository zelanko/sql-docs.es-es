---
title: 'Lección 3: Procesar la estructura de minería de datos de Bike Buyer | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ae7d871f4695d4109866a6a25979936116838d17
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312643"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>Lección 3: Procesar la estructura de minería de datos de Bike Buyer
  En esta lección, va a usar la INSERCIÓN en instrucción y la vista vTargetMail de la [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] base de datos de ejemplo para procesar las estructuras de minería de datos y modelos de minería de datos que creó en [lección 1: crear la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md) y [lección 2: agregar modelos de minería de datos a la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Al procesar una estructura de minería de datos, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lee los datos de origen y genera las estructuras que admiten los modelos de minería de datos. Al procesar un modelo de minería de datos, los datos definidos por la estructura de minería de datos se pasan por el algoritmo de minería de datos que elija. El algoritmo busca tendencias y patrones y, a continuación, almacena esta información en el modelo de minería de datos. Por consiguiente, el modelo de minería de datos no contiene los datos de origen reales, sino la información descubierta por el algoritmo. Para obtener más información acerca del procesamiento de modelos de minería de datos, vea [consideraciones y requisitos de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Solamente necesita volver a procesar una estructura de minería de datos si cambia una columna de la estructura o los datos de origen. Si agrega un modelo de minería de datos a una estructura de minería de datos que ya se ha procesado, puede usar la instrucción INSERT INTO MINING MODEL para entrenar el nuevo modelo de minería de datos.  
  
## <a name="train-structure-template"></a>Entrenar la plantilla de la estructura  
 Para entrenar la estructura de minería de datos y los modelos de minería de datos asociados, use la [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrucción. El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Identificación de la estructura de minería de datos  
  
-   Visualización en una lista de las columnas de la estructura de minería de datos  
  
-   Definición de los datos de entrenamiento  
  
 A continuación, se incluye un ejemplo genérico de la instrucción INSERT INTO:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 La primera línea del código identifica la estructura de minería de datos que se entrenará:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 La línea siguiente del código especifica las columnas definidas por la estructura de minería de datos. Debe incluir en la lista cada una de las columnas de la estructura de minería de datos, y cada columna debe estar asignada a una columna incluida en los datos de la consulta de origen:  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 La última línea del código define los datos que se usarán para entrenar la estructura de minería de datos:  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 En esta lección usará `OPENQUERY` para definir los datos de origen. Para obtener información acerca de otros métodos de la definición de la consulta de origen, consulte [ &#60;consulta de origen de datos&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará la tarea siguiente:  
  
-   Procesar la estructura de minería de datos de Bike Buyer  
  
## <a name="processing-the-predictive-mining-structure"></a>Procesar la estructura de minería de datos de predicción  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Para procesar la estructura de minería de datos con INSERT INTO  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], seleccione **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción INSERT INTO en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    [<mining structure name>]   
    ```  
  
     por:  
  
    ```  
    Bike Buyer  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining structure columns>  
    ```  
  
     por:  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
    [Commute Distance],  
    [Education],  
    [Gender],  
    [House Owner Flag],  
    [Marital Status],  
    [Number Cars Owned],  
    [Number Children At Home],  
    [Occupation],  
    [Region],  
    [Total Children],  
    [Yearly Income]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     por:  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     La instrucción OPENQUERY hace referencia al origen de datos de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] para obtener acceso a la vista vTargetMail. La vista contiene los datos de origen que se usarán para entrenar los modelos de minería de datos.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]     
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
7.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y un nombre al archivo `Process Bike Buyer Structure.dmx`.  
  
8.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
 En la siguiente lección explorará el contenido de los modelos de minería de datos que ha agregado a la estructura de minería de datos en esta lección.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Examinar los modelos de minería de datos Bike Buyer](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  

---
title: 'Lección 1: crear la estructura de minería de datos Bike Buyer | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a73ac60b-660f-458a-bd2f-993fbeba7226
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d6384910858d87a80aa3c8f897bc88e45f4504fb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62678498"
---
# <a name="lesson-1-creating-the-bike-buyer-mining-structure"></a>Lección 1: Creación de la estructura de minería de datos de Bike Buyer
  En esta lección creará una estructura de minería de datos que permita predecir si un cliente potencial de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] adquirirá una bicicleta. Si no está familiarizado con las estructuras de minería de datos y su rol en la minería de datos, vea estructuras de minería de datos [&#40;Analysis Services-data mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 La estructura de minería de datos Bike Buyer que creará en esta lección permite agregar modelos de minería de datos basados en el algoritmo de [Microsoft clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)Algorithm[Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md). En lecciones posteriores, utilizará los modelos de minería de datos de agrupación en clústeres para explorar las distintas formas en las que los clientes pueden agruparse, y utilizará los modelos de minería de datos del árbol de decisión para predecir si un cliente potencial adquirirá una bicicleta.  
  
## <a name="create-mining-structure-statement"></a>Instrucción CREATE MINING STRUCTURE  
 Para crear una estructura de minería de datos, use la instrucción [Create Mining structure &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx) . El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Asignación de un nombre a la estructura.  
  
-   Definición de la columna de clave.  
  
-   Definición de las columnas de minería de datos.  
  
-   Definición de un conjunto de datos de pruebas opcional.  
  
 A continuación, se incluye un ejemplo genérico de la instrucción CREATE MINING STRUCTURE:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
(  
    <key column>,  
    <mining structure columns>  
)   
WITH HOLDOUT (<holdout specifier>)  
```  
  
 En la primera línea del código se define el nombre de la estructura:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
```  
  
 Para obtener información acerca de cómo asignar un nombre a un objeto en extensiones de minería de datos (DMX), consulte [identifiers &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 En la siguiente línea del código se define la columna de clave para la estructura de minería de datos, que identifica de forma única una entidad de los datos de origen:  
  
```  
<key column>,  
```  
  
 En la estructura de minería de datos que va a crear, el identificador de cliente, `CustomerKey`, define una entidad en los datos de origen.  
  
 La siguiente línea del código se utiliza para definir las columnas de minería de datos que usarán los modelos de minería de datos asociados a la estructura de minería de datos:  
  
```  
<mining structure columns>  
```  
  
 Puede utilizar la función de discretización dentro de \<las columnas de la estructura de minería de datos> para discretos las columnas continuas mediante la sintaxis siguiente:  
  
 `DISCRETIZE(<method>,<number of buckets>)`  
  
 Para obtener más información sobre la discretización de columnas, vea [métodos de discretización &#40;&#41;de minería de datos ](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md). Para obtener más información acerca de los tipos de columnas de estructura de minería de datos que puede definir, vea [columnas de estructura de minería de datos](../../2014/analysis-services/data-mining/mining-structure-columns.md).  
  
 La línea final del código define una partición opcional en la estructura de minería de datos:  
  
```  
WITH HOLDOUT (<holdout specifier>)  
```  
  
 Se especifica una parte de los datos que se van a utilizar para probar los modelos de minería relacionados con la estructura y los datos restantes se utilizan para el aprendizaje de los modelos. De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] crea un conjunto de datos de pruebas que contiene el 30 por ciento de todos los datos del caso. Debe agregar la especificación donde se indique que el conjunto de datos de pruebas debería contener el 30 por ciento de los casos hasta un máximo de 1000. Si el 30 por ciento de los casos es menor que 1000, el conjunto de datos de pruebas contendrá la cantidad menor.  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Crear una consulta en blanco.  
  
-   Modificar la consulta para crear la estructura de minería de datos.  
  
-   Ejecutar la consulta.  
  
## <a name="creating-the-query"></a>Crear la consulta  
 El primer paso es conectarse a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y crear una consulta DMX en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para crear una consulta DMX mediante SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el cuadro de diálogo **conectar con el servidor** , en **tipo de servidor**, seleccione **Analysis Services**. En **nombre del servidor**, `LocalHost`escriba o escriba el nombre de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a la que desea conectarse para esta lección. Haga clic en **Conectar**.  
  
3.  En **Explorador de objetos**, haga clic con el botón secundario [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en la instancia de, seleccione **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el **Editor de consultas** y una nueva consulta en blanco.  
  
## <a name="altering-the-query"></a>Modificar la consulta  
 El paso siguiente es modificar la instrucción CREATE MINING STRUCTURE descrita anteriormente para crear la estructura de minería de datos de Bike Buyer.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>Para personalizar la instrucción CREATE MINING STRUCTURE  
  
1.  En el Editor de consultas, copie el ejemplo genérico de la instrucción CREATE MINING STRUCTURE en la consulta en blanco.  
  
2.  Reemplace lo siguiente:  
  
    ```  
    [<mining structure>]   
    ```  
  
     Por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <key column>   
    ```  
  
     Por:  
  
    ```  
    CustomerKey LONG KEY  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining structure columns>   
    ```  
  
     Por:  
  
    ```  
    [Age] LONG DISCRETIZED(Automatic,10),  
    [Bike Buyer] LONG DISCRETE,  
    [Commute Distance] TEXT DISCRETE,  
    [Education] TEXT DISCRETE,  
    [Gender] TEXT DISCRETE,  
    [House Owner Flag] TEXT DISCRETE,  
    [Marital Status] TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Number Children At Home] LONG DISCRETE,  
    [Occupation] TEXT DISCRETE,  
    [Region] TEXT DISCRETE,  
    [Total Children]LONG DISCRETE,  
    [Yearly Income] DOUBLE CONTINUOUS  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    WITH HOLDOUT (holdout specifier>)  
    ```  
  
     Por:  
  
    ```  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
    ```  
  
     Ahora, la instrucción completa de la estructura de minería de datos debería ser como sigue:  
  
    ```  
    CREATE MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key] LONG KEY,  
       [Age]LONG DISCRETIZED(Automatic,10),  
       [Bike Buyer] LONG DISCRETE,  
       [Commute Distance] TEXT DISCRETE,  
       [Education] TEXT DISCRETE,  
       [Gender] TEXT DISCRETE,  
       [House Owner Flag] TEXT DISCRETE,  
       [Marital Status] TEXT DISCRETE,  
       [Number Cars Owned]LONG DISCRETE,  
       [Number Children At Home]LONG DISCRETE,  
       [Occupation] TEXT DISCRETE,  
       [Region] TEXT DISCRETE,  
       [Total Children]LONG DISCRETE,  
       [Yearly Income] DOUBLE CONTINUOUS  
    )  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
  
    ```  
  
6.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
7.  En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `Bike Buyer Structure.dmx`al archivo.  
  
## <a name="executing-the-query"></a>Ejecutar la consulta  
 El último paso es ejecutar la consulta. Una vez creada y guardada una consulta, tiene que ejecutarse. Es decir, la instrucción tiene que ejecutarse para crear la estructura de minería de datos en el servidor. Para obtener más información acerca de la ejecución de consultas en el editor de consultas, vea [motor de base de datos editor de consultas &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para ejecutar la consulta  
  
1.  En el editor de consultas, en la barra de herramientas, haga clic en **Ejecutar**.  
  
     El estado de la consulta se muestra en la pestaña **mensajes** , en la parte inferior del editor de consultas, una vez finalizada la ejecución de la instrucción. En Mensajes, debe aparecer lo siguiente:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Ya existe una nueva estructura denominada **Bike Buyer** en el servidor.  
  
 En la siguiente lección agregará modelos de minería de datos a la estructura que acaba de crear.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Adición de modelos de minería de datos a la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
  
  

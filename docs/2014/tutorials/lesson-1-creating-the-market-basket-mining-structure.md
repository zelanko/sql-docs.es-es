---
title: 'Lección 1: Crear la estructura de minería de datos Market Basket | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a817c8d1-aff4-42b4-b194-ad9cc1c60f35
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2201afdb7226267e44686b76edb22e77b11dd199
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312443"
---
# <a name="lesson-1-creating-the-market-basket-mining-structure"></a>Lección 1: Crear la estructura de minería de la cesta de la compra
  En esta lección creará una estructura de minería de datos que permita predecir qué productos de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] tiende a adquirir un cliente simultáneamente. Si no está familiarizado con las estructuras de minería de datos y su rol en la minería de datos, vea [estructuras de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 La estructura de minería de datos de asociación que creará en esta lección admite la adición de modelos de minería de datos en función de la [algoritmo de asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md). En lecciones posteriores utilizará los modelos de minería de datos para predecir el tipo de productos que un cliente tiende a adquirir simultáneamente, lo que se denomina análisis de cesta de mercado (Market Basket). Por ejemplo, es posible que averigüe que los clientes tienden a comprar bicicletas de montaña, ruedas y cascos simultáneamente.  
  
 En esta lección se define la estructura de minería de datos utilizando tablas anidadas. Se utilizan tablas anidadas porque el dominio de datos que definirá la estructura se incluye en dos tablas de origen distintas. Para obtener más información sobre las tablas anidadas, vea [tablas anidadas &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
## <a name="create-mining-structure-statement"></a>Instrucción CREATE MINING STRUCTURE  
 Para crear una estructura de minería de datos que contiene una tabla anidada, se utiliza el [CREATE MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/create-mining-structure-dmx) instrucción. El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Asignación de un nombre a la estructura  
  
-   Definición de la columna de clave  
  
-   Definición de las columnas de minería de datos  
  
-   Definición de las columnas de la tabla anidada  
  
 A continuación, se incluye un ejemplo genérico de la instrucción CREATE MINING STRUCTURE:  
  
```  
CREATE MINING STRUCTURE [<Mining Structure Name>]  
(  
   <key column>,  
   <mining structure columns>,  
   <table columns>  
   (  <nested key column>,  
      <nested mining structure columns> )  
)  
  
```  
  
 En la primera línea del código se define el nombre de la estructura:  
  
```  
CREATE MINING STRUCTURE [Mining Structure Name]  
```  
  
 Para obtener información sobre la nomenclatura de un objeto en DMX, vea [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 En la siguiente línea del código se define la columna de clave para la estructura de minería de datos, que identifica de forma única una entidad de los datos de origen:  
  
```  
<key column>  
```  
  
 La siguiente línea del código se utiliza para definir las columnas de minería de datos que usarán los modelos de minería de datos asociados a la estructura de minería de datos:  
  
```  
<mining structure columns>  
```  
  
 En las siguientes líneas de código se definen las columnas de la tabla anidada:  
  
```  
<table columns>  
(  <nested key column>,  
   <nested mining structure columns> )  
```  
  
 Para obtener información acerca de los tipos de columnas que se pueden definir de la estructura de minería de datos, vea [columnas de estructura de minería de datos](../../2014/analysis-services/data-mining/mining-structure-columns.md).  
  
> [!NOTE]  
>  De forma predeterminada, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea un conjunto de datos de exclusión del 30 por ciento para cada estructura de minería de datos; sin embargo, al utilizar DMX para crear una estructura de minería de datos, debe agregar el conjunto de datos de exclusiones manualmente, si así se desea.  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Crear una consulta en blanco  
  
-   Modificar la consulta para crear la estructura de minería de datos  
  
-   Ejecutar la consulta  
  
## <a name="creating-the-query"></a>Crear la consulta  
 El primer paso es conectarse a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y crear una consulta DMX en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para crear una consulta DMX mediante SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el **conectar al servidor** cuadro de diálogo para **tipo de servidor**, seleccione **Analysis Services**. En **nombre del servidor**, tipo `LocalHost`, o el nombre de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que desea conectarse en esta lección. Haga clic en **Conectar**.  
  
3.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], seleccione **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
## <a name="altering-the-query"></a>Modificar la consulta  
 El paso siguiente es modificar la instrucción CREATE MINING STRUCTURE descrita anteriormente para crear la estructura de minería de datos Market Basket.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>Para personalizar la instrucción CREATE MINING STRUCTURE  
  
1.  En el Editor de consultas, copie el ejemplo genérico de la instrucción CREATE MINING STRUCTURE en la consulta en blanco.  
  
2.  Reemplace lo siguiente:  
  
    ```  
    [mining structure name]   
    ```  
  
     por:  
  
    ```  
    [Market Basket]  
    ```  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <key column>  
    ```  
  
     por:  
  
    ```  
    OrderNumber TEXT KEY  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <table columns>  
    (  <nested key column>,  
       <nested mining structure columns> )  
    ```  
  
     por:  
  
    ```  
    [Products] TABLE (  
        [Model] TEXT KEY  
    )  
    ```  
  
     El lenguaje TEXT KEY especifica que la columna Model es la columna de clave de la tabla anidada.  
  
     Ahora, la instrucción completa de la estructura de minería de datos debería ser como sigue:  
  
    ```  
    CREATE MINING STRUCTURE [Market Basket] (  
        OrderNumber TEXT KEY,  
        [Products] TABLE (  
            [Model] TEXT KEY  
        )  
    )  
    ```  
  
5.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
6.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y un nombre al archivo `Market Basket Structure.dmx`.  
  
## <a name="executing-the-query"></a>Ejecutar la consulta  
 El último paso es ejecutar la consulta. Después de crear y guardar una consulta, debe ejecutarse (es decir, debe ejecutarse la instrucción) para crear la estructura de minería de datos en el servidor. Para obtener más información acerca de cómo ejecutar consultas en el Editor de consultas, vea [Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para ejecutar la consulta  
  
-   En el Editor de consultas, en la barra de herramientas, haga clic en **Execute**.  
  
     El estado de la consulta se muestra en el **mensajes** ficha en la parte inferior del Editor de consultas de después de la instrucción termina de ejecutarse. En Mensajes, debe aparecer lo siguiente:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Una nueva estructura denominada **cesta** ahora existe en el servidor.  
  
 En la siguiente lección agregará modelos de minería de datos a la estructura de minería de datos Market Basket que acaba de crear.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de la cesta](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
  
  

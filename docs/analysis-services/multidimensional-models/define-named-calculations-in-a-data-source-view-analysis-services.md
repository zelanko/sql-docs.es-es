---
title: "Definir cálculos con nombre en una vista del origen de datos (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying named calculations
- data source views [Analysis Services], named calculations
- named calculations [Analysis Services]
ms.assetid: 729e7b12-6185-4b73-8bcb-cfe459b15355
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7459e3a65eb93aba62719d9357daa2d4b1c3ea65
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="define-named-calculations-in-a-data-source-view-analysis-services"></a>Definir cálculos con nombre en una vista del origen de datos (Analysis Services)
  Un cálculo con nombre es una expresión SQL representada como una columna calculada. Esta expresión aparece y se comporta como una columna en la tabla. Un cálculo con nombre permite ampliar el esquema relacional de las tablas o vistas existentes en una vista del origen de datos sin modificar las tablas o vistas en el origen de datos subyacente. Considere los ejemplos siguientes:  
  
-   Cree un cálculo con nombre derivado de varias columnas en una tabla de hechos (por ejemplo, cree Tax Amount multiplicando un tipo impositivo por un precio de venta).  
  
-   Cree un nombre descriptivo para un miembro de dimensión.  
  
-   Para mejorar el rendimiento de las consultas, cree un cálculo con nombre en la DSV en lugar de crear un miembro calculado en un cubo. Los cálculos con nombre se calculan durante el procesamiento, mientras que los miembros calculados se calculan en el tiempo de la consulta.  
  
## <a name="creating-named-calculations"></a>Crear cálculos con nombre  
  
> [!NOTE]  
>  No se puede agregar un cálculo con nombre a una consulta con nombre, ni se puede basar una consulta con nombre en una tabla que contenga un cálculo con nombre.  
  
 Cuando se crea un cálculo con nombre, se especifica un nombre, la expresión SQL y, opcionalmente, una descripción del cálculo. La expresión SQL puede hacer referencia a otras tablas de la vista del origen de datos. Una vez definido el cálculo con nombre, su expresión se envía al proveedor del origen de datos y se valida como la siguiente instrucción SQL en la que `<Expression>` contiene la expresión que define el cálculo con nombre.  
  
```  
SELECT   
   <Table Name in Data Source>.*,   
   <Expression> AS <Column Name>   
FROM   
   <Table Name in Data Source> AS <Table Name in Data Source View>  
```  
  
 El tipo de datos de la columna se determina por el tipo de datos del valor escalar devuelto por la expresión. Si el proveedor no encuentra ningún error en la expresión, la columna se agrega a la tabla.  
  
 Las columnas a las que hace referencia la expresión no deben estar calificadas o deben estar calificadas solo por el nombre de la tabla. Por ejemplo, para hacer referencia a la columna SaleAmount de una tabla, son válidos los valores `SaleAmount` o `Sales.SaleAmount` , pero `dbo.Sales.SaleAmount` genera un error.  
  
 La expresión no se incluye entre paréntesis automáticamente. Por lo tanto, si una expresión, como una instrucción SELECT, requiere paréntesis, debe escribirlos en el cuadro **Expresión** . Por ejemplo, la siguiente expresión solo es válida si escribe los paréntesis.  
  
```  
(SELECT Description FROM Categories WHERE Categories.CategoryID = CategoryID)  
```  
  
## <a name="add-or-edit-a-named-calculation"></a>Agregar o editar un cálculo con nombre  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos que contiene la vista del origen de datos en que desea definir un cálculo con nombre.  
  
2.  En el Explorador de soluciones, expanda la carpeta **Vistas del origen de datos** y luego haga doble clic en la vista del origen de datos.  
  
3.  Haga clic con el botón derecho en la tabla en la que quiere definir el cálculo con nombre en el panel **Tablas** o **Diagrama** y luego haga clic en **Nuevo cálculo con nombre**. Asegúrese de hacer clic con el botón secundario en el nombre de tabla, y no en un atributo. El menú debe ser similar al siguiente:  
  
     ![Captura de pantalla del área de trabajo de diagrama, haga clic en el menú](../../analysis-services/multidimensional-models/media/ssas-olapdsv-diagram.gif "captura de pantalla del área de trabajo de diagrama, el menú contextual")  
  
    > [!NOTE]  
    >  Para buscar una tabla o vista, puede usar la opción **Buscar tabla** si hace clic en el menú **Vista del origen de datos** o si hace clic con el botón derecho en una zona abierta de los paneles **Tablas** o **Diagrama** .  
  
4.  En el cuadro de diálogo **Crear cálculo con nombre** , realice las siguientes operaciones:  
  
    -   En el cuadro de texto **Nombre de columna** , escriba el nombre de la nueva columna.  
  
    -   En el cuadro de texto **Descripción** , escriba una descripción para la nueva columna.  
  
    -   En el cuadro de texto **Expresión** , escriba la expresión que produzca el contenido de la nueva columna en el dialecto SQL adecuado para el proveedor de datos.  
  
5.  Haga clic en **Aceptar**.  
  
     La columna de cálculo con nombre aparecerá como la última columna de la tabla de la vista del origen de datos. El símbolo de una calculadora indica que la columna contiene un cálculo con nombre.  
  
## <a name="delete-a-named-calculation"></a>Eliminar un cálculo con nombre  
 Si trata de eliminar un cálculo con nombre, se le presenta una lista de los objetos definidos en el proyecto o la base de datos que no serán válidos tras la eliminación. Revise la lista cuidadosamente antes de eliminar el cálculo.  
  
## <a name="see-also"></a>Vea también  
 [Definir consultas con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  

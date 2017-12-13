---
title: Usar DRILLTHROUGH para recuperar datos de origen (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 30587e46a4ac54d2ac2825649f25cb321c05eba4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>Manipulación de datos MDX - recuperan los datos de origen mediante la obtención de detalles
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Expresiones multidimensionales (MDX) utilizan la [obtención de detalles](../../../mdx/mdx-data-manipulation-drillthrough.md)instrucción para recuperar un conjunto de filas del origen de datos para una celda del cubo.  
  
 Para ejecutar una instrucción **DRILLTHROUGH** en un cubo, es preciso definir una acción de obtención de detalles para el cubo en cuestión. Para definir una acción de obtención de detalles, en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], en el Diseñador de cubos, en el panel de **Acciones** , en la barra de herramientas, haga clic en **Nueva acción de obtención de detalles**. En la nueva acción de obtención de detalles, especifique el nombre de la acción, el destino, la condición y las columnas que devolverá la instrucción **DRILLTHROUGH** .  
  
## <a name="drillthrough-statement-syntax"></a>Sintaxis de la instrucción DRILLTHROUGH  
 La instrucción **DRILLTHROUGH** utiliza la sintaxis siguiente:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 La cláusula **SELECT** identifica la celda del cubo que contiene el origen de datos que se va a recuperar. Esta cláusula **SELECT** es idéntica a una instrucción MDX **SELECT** normal, con la diferencia de que en la cláusula **SELECT** únicamente se puede especificar un miembro en cada eje. Si se especifica más de un miembro en un eje, se produce un error.  
  
 La sintaxis `<Max_Rows>` especifica el número máximo de filas de cada conjunto de filas devuelto. Si el proveedor OLE DB que se usa para conectarse al origen de datos no es compatible con **DBPROP_MAXROWS**, se omitirá el valor `<Max_Rows>` .  
  
 La sintaxis `<First_Rowset>` identifica la partición cuyo conjunto de filas se devuelve en primer lugar.  
  
 La sintaxis `<Return_Columns>` identifica las columnas de la base de datos subyacente que se devuelven.  
  
## <a name="drillthrough-statement-example"></a>Ejemplo de la instrucción DRILLTHROUGH  
 En el siguiente ejemplo se muestra el uso de la instrucción **DRILLTHROUGH** : En este ejemplo, la instrucción DRILLTHROUGH realiza consultas en las hojas de las dimensiones Store, Product y Time a lo largo de la dimensión Stores (el eje segmentador) y devuelve el grupo de medida de departamento, Id. del departamento y el nombre del empleado.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Vea también  
 [Manipular datos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  

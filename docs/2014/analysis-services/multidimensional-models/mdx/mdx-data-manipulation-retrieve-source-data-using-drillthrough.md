---
title: Usar la obtención de detalles para recuperar datos de origen (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b437016cc29b2e4a85f781e3a422fb40c70f37c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074298"
---
# <a name="using-drillthrough-to-retrieve-source-data-mdx"></a>Usar DRILLTHROUGH para recuperar datos de origen (MDX)
  Las expresiones multidimensionales (MDX) usan la instrucción [DRILLTHROUGH](/sql/mdx/mdx-data-manipulation-drillthrough) para recuperar un conjunto de filas de los datos de origen de una celda de cubo.  
  
 Para ejecutar una instrucción `DRILLTHROUGH` en un cubo, es preciso definir una acción de obtención de detalles para el cubo en cuestión. Para definir una acción de obtención de detalles, en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], en el Diseñador de cubos, en el panel de **Acciones** , en la barra de herramientas, haga clic en **Nueva acción de obtención de detalles**. En la nueva acción de obtención de detalles, especifique el nombre de la acción, el destino, la condición y las columnas que devolverá la instrucción `DRILLTHROUGH`.  
  
## <a name="drillthrough-statement-syntax"></a>Sintaxis de la instrucción DRILLTHROUGH  
 La instrucción `DRILLTHROUGH` utiliza la sintaxis siguiente:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 La cláusula `SELECT` identifica la celda del cubo que contiene el origen de datos que se va a recuperar. Esta cláusula `SELECT` es idéntica a una instrucción MDX `SELECT` normal, con la diferencia de que en la cláusula `SELECT` únicamente se puede especificar un miembro en cada eje. Si se especifica más de un miembro en un eje, se produce un error.  
  
 La sintaxis `<Max_Rows>` especifica el número máximo de filas de cada conjunto de filas devuelto. Si el proveedor OLE DB que se utiliza para conectarse al origen de datos no es compatible con `DBPROP_MAXROWS`, se omite el valor `<Max_Rows>`.  
  
 La sintaxis `<First_Rowset>` identifica la partición cuyo conjunto de filas se devuelve en primer lugar.  
  
 La sintaxis `<Return_Columns>` identifica las columnas de la base de datos subyacente que se devuelven.  
  
## <a name="drillthrough-statement-example"></a>Ejemplo de la instrucción DRILLTHROUGH  
 En el siguiente ejemplo se muestra el uso de la instrucción `DRILLTHROUGH`: En este ejemplo, la instrucción DRILLTHROUGH realiza consultas en las hojas de las dimensiones Store, Product y Time a lo largo de la dimensión Stores (el eje segmentador) y devuelve el grupo de medida de departamento, Id. del departamento y el nombre del empleado.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Manipular datos &#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  

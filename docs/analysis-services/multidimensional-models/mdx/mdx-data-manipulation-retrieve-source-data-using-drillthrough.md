---
title: Usar DRILLTHROUGH para recuperar datos de origen (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81c873d0ea6e5c21d97fc719ce1c72a773df43e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62802840"
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>Manipulación de datos MDX: recuperación de los datos de origen mediante DRILLTHROUGH
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Las expresiones multidimensionales (MDX) usan la instrucción [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md)para recuperar un conjunto de filas de los datos de origen de una celda de cubo.  
  
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
  
  

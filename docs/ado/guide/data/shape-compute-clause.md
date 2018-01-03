---
title: "Dar forma a cláusula COMPUTE | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c20aec7585c33a7165fac4e93b446e4ce3aaf4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="shape-compute-clause"></a>Cláusula COMPUTE de forma
Una cláusula COMPUTE de forma genera un elemento primario **Recordset**, cuyas columnas se componen de una referencia al formulario secundario **Recordset**; opcional columnas cuyo contenido se capítulo, nuevas o las columnas calculadas, o resultado de ejecutar funciones de agregado en el elemento secundario **Recordset** o una forma anteriormente **Recordset**; y las columnas en el elemento secundario **Recordset** enumerados en la cláusula opcional.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 Los elementos de esta cláusula son los siguientes:  
  
 *comando secundario*  
 Consta de uno de los siguientes:  
  
-   Un comando de consulta entre llaves ("{}") que devuelve un elemento secundario **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, si bien ADO no requiere ningún lenguaje de consulta determinado.  
  
-   El nombre de un objeto en forma de **conjunto de registros**.  
  
-   Otro comando shape.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *alias de elemento secundario*  
 Un alias utilizado para hacer referencia a la **Recordset** devuelto por la *comando secundario.* El *alias secundario* se requiere en la lista de columnas en la cláusula COMPUTE y define la relación entre el elemento primario y secundario **Recordset** objetos.  
  
 *lista de columnas anexado*  
 Una lista en la que cada elemento define una columna en el objeto primario generado. Cada elemento contiene una columna de capítulo, una columna nueva, una columna calculada o un valor resultante de una función de agregado en el elemento secundario **conjunto de registros**.  
  
 *lista de campos agrupados*  
 Una lista de columnas en el elemento primario y secundario **Recordset** objetos que especifica cómo se deben agrupar filas en el elemento secundario.  
  
 Para cada columna de la *campo lista agrupados,* hay una columna correspondiente en los primarios y secundarios **Recordset** objetos. Para cada fila en el elemento primario **Recordset**, el *lista de campos agrupados* columnas tienen valores únicos y el elemento secundario **Recordset** al que hace referencia el elemento primario fila se compone únicamente de secundarios las filas cuya *lista de campos agrupados* columnas tienen los mismos valores que la fila primaria.  
  
 Si se incluye, la cláusula BY secundario **Recordset**de filas se agruparán en función de las columnas en la cláusula COMPUTE. El elemento primario **Recordset** contendrá una fila por cada grupo de filas en el elemento secundario **conjunto de registros**.  
  
 Si se omite la cláusula BY, todo el secundario **Recordset** se trata como un solo grupo y el elemento primario **Recordset** contendrá exactamente una fila. Esa fila hará referencia a todo el secundario **conjunto de registros**. Si se omite la cláusula BY, podrá calcular los agregados de "total general" en todo el secundario **conjunto de registros**.  
  
 Por ejemplo:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Independientemente de qué manera el elemento primario **Recordset** está formado (mediante COMPUTE o APPEND), contendrá una columna de capítulo que se utiliza para relacionar con un elemento secundario **conjunto de registros**. Si lo desea, el elemento primario **Recordset** también puede contener columnas que contienen agregados (SUM, MIN, MAX etc.) de las filas secundarias. El elemento primario y el elemento secundario **Recordset** puede contener columnas que contienen una expresión en la fila en la **Recordset**, así como las columnas que son nuevos e inicialmente vacía.  
  
## <a name="operation"></a>Operación  
 El *comando secundario* se emite al proveedor, que devuelve un elemento secundario **conjunto de registros**.  
  
 La cláusula COMPUTE especifica las columnas del elemento primario **Recordset**, lo que puede ser una referencia al formulario secundario **Recordset**, uno o varios agregados, una expresión calculada o columnas nuevas. Si hay una cláusula BY, las columnas que define también se anexan al elemento primario **conjunto de registros**. La cláusula BY especifica cómo las filas del elemento secundario **Recordset** se agrupan.  
  
 Por ejemplo, suponga que tiene una tabla denominada Demographics, que consta de los campos Estado, ciudad y rellenado. (Las cifras de población en la tabla se proporcionan únicamente como ejemplo).  
  
|State|City|Población|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|O BIEN|Medford|200,000|  
|O BIEN|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
|WA|Tacoma|500,000|  
|O BIEN|Corvallis|300,000|  
  
 Ahora, ejecute este comando shape:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Este comando abre una forma **Recordset** con dos niveles. El nivel primario es una generada **Recordset** con una columna agregada (`SUM(rs.population)`), una columna que hace referencia el elemento secundario **Recordset** (`rs`) y una columna para agrupar el secundario **Recordset** (`state`). El nivel secundario es el **Recordset** devuelto por el comando de consulta (`select * from demographics`).  
  
 El elemento secundario **Recordset** serán filas de detalles agrupados por estado, pero por lo demás en ningún orden determinado. Es decir, los grupos no estarán en orden alfabético o numérico. Si desea que el elemento primario **Recordset** para poder ordenarse, puede usar el **Sort del objeto Recordset** método para ordenar el elemento primario **conjunto de registros**.  
  
 Ahora puede navegar el primario abierto **Recordset** y tener acceso a los detalles de secundarios **Recordset** objetos. Para obtener más información, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Primario resultante y conjuntos de registros de detalle de secundarios  
  
### <a name="parent"></a>Parent  
  
|SUM (rs. Llenado)|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|Referencia a child1|CA|  
|1,200,000|Referencia a child2|WA|  
|1,100,000|Referencia a secundario3|O BIEN|  
  
## <a name="child1"></a>Child1  
  
|State|City|Población|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
  
## <a name="child2"></a>Child2  
  
|State|City|Población|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|City|Población|  
|-----------|----------|----------------|  
|O BIEN|Medford|200,000|  
|O BIEN|Portland|400,000|  
|O BIEN|Corvallis|300,000|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a las filas en un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Proveedores deseados para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value (propiedad) (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)

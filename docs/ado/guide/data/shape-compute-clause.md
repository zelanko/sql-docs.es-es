---
title: Cláusula COMPUTE de forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e1e268da5eb4c53b6270e474987c69b88383cd9b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700357"
---
# <a name="shape-compute-clause"></a>Cláusula COMPUTE de forma
Una cláusula COMPUTE de forma genera un elemento primario **Recordset**, cuyas columnas se componen de una referencia al elemento secundario **Recordset**; opcional columnas cuyo contenido se capítulo, nuevas o las columnas calculadas, o resultado de ejecutar las funciones de agregado en el elemento secundario **Recordset** o un previamente formados **Recordset**; y las columnas en el elemento secundario **Recordset** enumerados en la cláusula opcional.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Descripción  
 Las partes de esta cláusula son los siguientes:  
  
 *child-command*  
 Consta de uno de los siguientes:  
  
-   Un comando de consulta entre llaves ("{}") que devuelve un elemento secundario **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, aunque ADO no requiere ningún lenguaje de consulta determinada.  
  
-   El nombre de una existente en forma de **Recordset**.  
  
-   Comando de otra forma.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *child-alias*  
 Un alias que se usa para hacer referencia a la **Recordset** devuelto por la *comando secundario.* El *alias secundario* se requiere en la lista de columnas en la cláusula COMPUTE y define la relación entre los primarios y secundarios **Recordset** objetos.  
  
 *appended-column-list*  
 Una lista en la que cada elemento define una columna en el objeto primario generado. Cada elemento contiene una columna de capítulo, una nueva columna, una columna calculada o un valor resultante de una función de agregado en el elemento secundario **Recordset**.  
  
 *grp-field-list*  
 Una lista de columnas de los primarios y secundarios **Recordset** objetos que especifica cómo se deben agrupar filas en el elemento secundario.  
  
 Para cada columna de la *grp lista de campos,* hay una columna correspondiente en los primarios y secundarios **Recordset** objetos. Para cada fila en el elemento primario **Recordset**, el *lista de campos agrupados* columnas tienen valores únicos y el elemento secundario **Recordset** al que hace referencia el elemento primario fila se compone únicamente de secundarios las filas cuya *lista de campos agrupados* columnas tienen los mismos valores que la fila primaria.  
  
 Si se incluye, la cláusula BY secundario **Recordset**de filas se agruparán en función de las columnas en la cláusula COMPUTE. El elemento primario **Recordset** contendrá una fila por cada grupo de filas en el elemento secundario **Recordset**.  
  
 Si se omite la cláusula BY, todo el secundario **Recordset** se trata como un solo grupo y el elemento primario **Recordset** contendrá exactamente una fila. Esa fila hará referencia a todo el secundario **Recordset**. Si se omite la cláusula BY, podrá calcular agregados de "total general" en todo el secundario **Recordset**.  
  
 Por ejemplo:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Independientemente de qué manera el elemento primario **Recordset** se forma (mediante COMPUTE o APPEND), contendrá una columna de capítulo se usa para relacionarla con un elemento secundario **Recordset**. Si lo desea, el elemento primario **Recordset** también puede contener columnas que contienen agregados (SUM, MIN, MAX etc.) a través de las filas secundarias. El elemento primario y secundario **Recordset** pueden contener columnas que contienen una expresión en la fila de la **Recordset**, así como las columnas que son nuevos e inicialmente vacía.  
  
## <a name="operation"></a>Operación  
 El *comando secundario* se emite al proveedor, que devuelve un elemento secundario **Recordset**.  
  
 La cláusula COMPUTE especifica las columnas del elemento primario **Recordset**, que puede ser una referencia al elemento secundario **Recordset**, uno o varios agregados, una expresión calculada o columnas nuevas. Si hay una cláusula BY, las columnas que define también se anexan con el elemento primario **Recordset**. La cláusula BY especifica cómo las filas del elemento secundario **Recordset** se agrupan.  
  
 Por ejemplo, suponga que tiene una tabla denominada Demographics, que consta de los campos de ciudad, estado y el rellenado. (Los datos de población en la tabla se proporcionan únicamente como ejemplo).  
  
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
  
 Este comando abre una forma **Recordset** con dos niveles. El nivel primario es un generado **Recordset** con una columna agregada (`SUM(rs.population)`), una columna que hace referencia el elemento secundario **Recordset** (`rs`) y una columna para agrupar el elemento secundario **Recordset** (`state`). El nivel secundario es el **Recordset** devuelto por el comando de consulta (`select * from demographics`).  
  
 El elemento secundario **Recordset** filas de detalles será agrupados por estado, pero en caso contrario, sin ningún orden determinado. Es decir, los grupos no estarán en orden alfabético o numérico. Si desea que el elemento primario **Recordset** para poder ordenarse, puede usar el **ordenación del conjunto de registros** para ordenar el elemento primario **Recordset**.  
  
 Ahora puede desplazarse el primario abierto **Recordset** y tener acceso a los detalles del elemento secundario **Recordset** objetos. Para obtener más información, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
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
 [Valor (propiedad, ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)

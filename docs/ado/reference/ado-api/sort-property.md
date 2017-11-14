---
title: Ordenar propiedad | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 16bba12bdcf95e8e71cab6dcb8404b7b3b1916e7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sort-property"></a>Propiedad de ordenación
Indica uno o más nombres de campo en el que el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) está ordenada, y si cada campo se ordena en orden ascendente o descendente.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** los nombres de valor que indica el campo de la **Recordset** en el que se va a ordenar. Cada nombre está separado por una coma y, seguido opcionalmente de un espacio en blanco y la palabra clave, **ASC**, que ordena el campo en orden ascendente, o **DESC**, que ordena el campo en orden descendente. De forma predeterminada, si no se especifica ninguna palabra clave, el campo se ordena en orden ascendente.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad requiere la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establezca en **adUseClient**. Se creará un índice temporal para cada campo especificado en el **ordenación** propiedad si todavía no existe un índice.  
  
 La operación de ordenación es eficaz porque los datos no se reorganizan físicamente, sino que simplemente se obtiene acceso en el orden especificado por el índice.  
  
 Cuando el valor de la **ordenación** propiedad es un valor distinto de una cadena vacía, el **ordenación** orden de las propiedades tiene prioridad sobre el orden especificado en un **ORDER BY** cláusula incluido en la instrucción SQL utilizada para abrir el **conjunto de registros**.  
  
 El **Recordset** no deben estar abiertos antes de acceder a la **ordenación** propiedad; se puede establecer en cualquier momento después de la **conjunto de registros** se crea una instancia de objeto.  
  
 Establecer el **ordenación** propiedad en una cadena vacía se restablecerá todas las filas a su orden original y se eliminarán los índices temporales. No se eliminarán los índices existentes.  
  
 Suponga que un **Recordset** contiene tres campos denominados *firstName*, *middleInitial*, y *lastName*. Establecer el **ordenación** propiedad a la cadena, "`lastName DESC, firstName ASC`", que ordenará el **Recordset** por apellido en orden descendente y luego por nombre en orden ascendente. Se omite la inicial del segundo nombre.  
  
 Ningún campo puede denominarse "ASC" o "DESC" porque esos nombres en conflicto con las palabras clave **ASC** y **DESC**. Puede crear un alias para un campo con un nombre en conflicto mediante la **AS** palabra clave en la consulta que devuelve el **conjunto de registros**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de ordenación (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Ejemplo de la propiedad de ordenación (VC ++)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimizar la propiedad dinámica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


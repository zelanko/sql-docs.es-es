---
title: Propiedad Sort | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3dc6f7799e28fff65a1b6e60329ba9fb94d84824
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759841"
---
# <a name="sort-property"></a>Propiedad de ordenación
Indica uno o más nombres de campo en los que se ordena el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) y si cada campo se ordena en orden ascendente o descendente.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **cadena** que indica los nombres de campo del **conjunto de registros** por los que se va a ordenar. Cada nombre está separado por una coma y, opcionalmente, va seguido de un espacio en blanco y de la palabra clave, **ASC**, que ordena el campo en orden ascendente, o **DESC**, que ordena el campo en orden descendente. De forma predeterminada, si no se especifica ninguna palabra clave, el campo se ordena en orden ascendente.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad requiere que la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) esté establecida en **adUseClient**. Se creará un índice temporal para cada campo especificado en la propiedad **Sort** si aún no existe un índice.  
  
 La operación de ordenación es eficaz porque los datos no se reorganizan físicamente, pero solo se tiene acceso a ellos en el orden especificado por el índice.  
  
 Cuando el valor de la propiedad **Sort** es distinto de una cadena vacía, el orden de las propiedades de **ordenación** tiene prioridad sobre el orden especificado en una cláusula **order by** incluida en la instrucción SQL que se usa para abrir el **conjunto de registros**.  
  
 No es necesario abrir el **conjunto de registros** antes de tener acceso a la propiedad de **ordenación** . se puede establecer en cualquier momento después de crear una instancia del objeto de **conjunto de registros** .  
  
 Si establece la propiedad **Sort** en una cadena vacía, se restablecerán las filas a su orden original y se eliminarán los índices temporales. Los índices existentes no se eliminarán.  
  
 Supongamos que un **conjunto de registros** contiene tres campos denominados *FirstName*, *middleInitial*y *LastName*. Establezca la propiedad **Sort** en la cadena " `lastName DESC, firstName ASC` ", que ordenará el conjunto de **registros** por apellido en orden descendente y luego por nombre en orden ascendente. Se omite la inicial del segundo nombre.  
  
 No se puede llamar a ningún campo "ASC" o "DESC" porque esos nombres entran en conflicto con las palabras clave **ASC** y **DESC**. Puede crear un alias para un campo con un nombre en conflicto mediante la palabra clave **as** en la consulta que devuelve el **conjunto de registros**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad sort (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Ejemplo de propiedad de ordenación (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize (propiedad dinámica) (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)

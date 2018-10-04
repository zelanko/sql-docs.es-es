---
title: Ordenar propiedades | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c579c824d65d50dfd1b222615f247d97209db37
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47675603"
---
# <a name="sort-property"></a>Propiedad de ordenación
Indica uno o más nombres de campo en el que el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) está ordenada, y si cada campo está ordenado en orden ascendente o descendente.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que indica el campo de nombres en el **Recordset** en el que se va a ordenar. Cada nombre está separado por una coma y, seguido opcionalmente de un espacio en blanco y la palabra clave, **ASC**, que ordena el campo en orden ascendente, o **DESC**, que ordena el campo en orden descendente. De forma predeterminada, si no se especifica ninguna palabra clave, el campo se ordena en orden ascendente.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad requiere la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establece en **adUseClient**. Se creará un índice temporal para cada campo especificado en el **ordenación** propiedad si no existe.  
  
 La operación de ordenación es eficaz porque no se reorganizan físicamente datos, sino que simplemente se obtiene acceso en el orden especificado por el índice.  
  
 Cuando el valor de la **ordenación** propiedad es distinto de una cadena vacía, el **ordenación** orden de las propiedades tiene prioridad sobre el orden especificado en un **ORDER BY** cláusula incluido en la instrucción SQL utilizada para abrir el **Recordset**.  
  
 El **Recordset** no deben estar abiertos antes de acceder a la **ordenación** propiedad; se puede establecer en cualquier momento después de la **Recordset** se crea una instancia de objeto.  
  
 Establecer el **ordenación** restablecerá las filas a su orden original y eliminar índices temporales propiedad en una cadena vacía. No se eliminarán los índices existentes.  
  
 Supongamos que un **Recordset** contiene tres campos denominados *firstName*, *middleInitial*, y *lastName*. Establecer el **ordenación** propiedad a la cadena, "`lastName DESC, firstName ASC`", que ordenará los **Recordset** por apellido en orden descendente y luego por nombre en orden ascendente. Se omite la inicial del segundo nombre.  
  
 Ningún campo puede denominarse "ASC" o "DESC" porque esos nombres en conflicto con las palabras clave **ASC** y **DESC**. Puede crear un alias para un campo con un nombre en conflicto mediante la **AS** palabra clave en la consulta que devuelve el **Recordset**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de ordenación (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Ejemplo de la propiedad Sort (VC ++)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimizar la propiedad dinámica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)

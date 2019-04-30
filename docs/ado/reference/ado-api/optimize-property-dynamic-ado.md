---
title: (ADO) de propiedad dinámica Optimize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d461d0fad834dfc3c3c6f22ec64cc4987eca6fa5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240044"
---
# <a name="optimize-property-dynamic-ado"></a>Propiedad dinámica Optimize (ADO)
Especifica si se debe crear un índice en una [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **booleano** valor que indica si se debe crear un índice.  
  
## <a name="remarks"></a>Comentarios  
 Un índice puede mejorar el rendimiento de las operaciones que buscar u ordenar los valores en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). El índice es interno a ADO; no se puede tener acceso a o utilizarlo en su aplicación explícitamente.  
  
 Para crear un índice en un campo, establezca la **optimizar** propiedad **True**. Para eliminar el índice, establezca esta propiedad en **False**.  
  
 **Optimizar** se anexa una propiedad dinámica a la [campo](../../../ado/reference/ado-api/field-object.md) objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Optimizar el ejemplo de la propiedad (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Optimizar el ejemplo de la propiedad (VC ++)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Propiedad de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Buscar (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propiedad de ordenación](../../../ado/reference/ado-api/sort-property.md)

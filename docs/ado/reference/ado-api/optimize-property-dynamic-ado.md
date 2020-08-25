---
description: Propiedad dinámica Optimize (ADO)
title: Optimize (propiedad dinámica) (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 91da30a49a0eff7d8b32274e8486002f78f2a05f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773644"
---
# <a name="optimize-property-dynamic-ado"></a>Propiedad dinámica Optimize (ADO)
Especifica si se debe crear un índice en un [campo](./field-object.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **booleano** que indica si se debe crear un índice.  
  
## <a name="remarks"></a>Observaciones  
 Un índice puede mejorar el rendimiento de las operaciones que buscan u ordenan valores en un [conjunto de registros](./recordset-object-ado.md). El índice es interno de ADO; no se puede obtener acceso a él ni usarlo explícitamente en la aplicación.  
  
 Para crear un índice en un campo, establezca la propiedad **Optimize** en **true**. Para eliminar el índice, establezca esta propiedad en **false**.  
  
 **Optimize** es una propiedad dinámica anexada a la colección de [propiedades](./properties-collection-ado.md) de objeto de [campo](./field-object.md) cuando la propiedad [CursorLocation](./cursorlocation-property-ado.md) está establecida en **adUseClient**.  
  
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
 [Objeto Field](./field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad Optimize (VB)](./optimize-property-example-vb.md)   
 [Ejemplo de la propiedad Optimize (VC + +)](./optimize-property-example-vc.md)   
 [Propiedad Filter](./filter-property.md)   
 [Find (método) (ADO)](./find-method-ado.md)   
 [Propiedad de ordenación](./sort-property.md)
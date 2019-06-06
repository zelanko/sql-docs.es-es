---
title: Método CompareBookmarks (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e0c0e9e2debfc33d8bb51d4797215155247f3a7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698669"
---
# <a name="comparebookmarks-method-ado"></a>Método CompareBookmarks (ADO)
Compara dos marcadores y devuelve una indicación de sus valores relativos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [CompareEnum](../../../ado/reference/ado-api/compareenum.md) valor que indica la posición de fila relativa de dos registros representados por sus marcadores.  
  
#### <a name="parameters"></a>Parámetros  
 *Bookmark1*  
 El marcador de la primera fila.  
  
 *Bookmark2*  
 El marcador de la segunda fila.  
  
## <a name="remarks"></a>Comentarios  
 Los marcadores que deben aplicarse al mismo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o un **Recordset** objeto y su [clon](../../../ado/reference/ado-api/clone-method-ado.md). No se puede comparar de manera confiable los marcadores de diferentes **Recordset** objetos, incluso si se crearon desde el mismo origen o el comando. Tampoco se pueden comparar los marcadores para un **Recordset** cuyo proveedor subyacente no admite comparaciones de objeto.  
  
 Un marcador que identifica una fila en un **Recordset** objeto. Use la [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad de la fila actual para obtener su marcador.  
  
 Dado que el tipo de datos de un marcador es específico para cada proveedor, ADO lo expone como un **Variant**. Por ejemplo, los marcadores de SQL Server son de tipo DBTYPE_R8 (**doble**). ADO expondrá este tipo como un **Variant** con un subtipo de **doble**.  
  
 Cuando se comparan marcadores, ADO no realiza ningún tipo de conversión. Los valores se pasan simplemente al proveedor que se produce la comparación. Si los marcadores que se pasan a la **CompareBookmarks** método se almacenan en variables de diferentes tipos, puede generar el error de coincidencia de tipo siguientes: "Argumentos son del tipo incorrecto, están fuera del intervalo aceptable o que están en conflicto entre sí".  
  
 Marcador que no es válido o con formato incorrecto producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Ejemplo del método CompareBookmarks (VC ++)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark (propiedad) (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)

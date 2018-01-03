---
title: "El método Delete (colección Fields de ADO) | Documentos de Microsoft"
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
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords: Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1cc110ab21ddd81b45b361e5cd38e9d90970a173
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="delete-method-ado-fields-collection"></a>El método Delete (colección Fields de ADO)
Elimina un objeto de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Campo*  
 A **Variant** que designa el [campo](../../../ado/reference/ado-api/field-object.md) objeto que se va a eliminar. Este parámetro puede ser el nombre de la **campo** objeto o la posición ordinal de la **campo** propio objeto.  
  
## <a name="remarks"></a>Comentarios  
 Llamar a la **Fields.Delete** método en un formato de archivo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) provoca un error de tiempo de ejecución.  
  
## <a name="applies-to"></a>Se aplica a  
 [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

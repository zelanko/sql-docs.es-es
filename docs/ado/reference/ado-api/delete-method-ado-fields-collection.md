---
description: El método Delete (colección Fields de ADO)
title: Método Delete (colección Fields de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: rothja
ms.author: jroth
ms.openlocfilehash: fb60cea6ef2e741103e94f38955bb2afc688e228
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444177"
---
# <a name="delete-method-ado-fields-collection"></a>El método Delete (colección Fields de ADO)
Elimina un objeto de la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Campo*  
 **Variante** que designa el objeto de [campo](../../../ado/reference/ado-api/field-object.md) que se va a eliminar. Este parámetro puede ser el nombre del objeto de **campo** o la posición ordinal del propio objeto de **campo** .  
  
## <a name="remarks"></a>Observaciones  
 Si se llama al método **Fields. Delete** en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) abierto, se produce un error en tiempo de ejecución.  
  
## <a name="applies-to"></a>Se aplica a  
 [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

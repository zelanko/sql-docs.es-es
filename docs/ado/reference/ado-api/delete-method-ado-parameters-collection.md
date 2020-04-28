---
title: Método Delete (colección de parámetros de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 965ef1bc84961e3358c530180bfe4e99249b0bc7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933179"
---
# <a name="delete-method-ado-parameters-collection"></a>Método Delete (colección de parámetros de ADO)
Elimina un objeto de la colección de [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Ajustar*  
 Valor de **cadena** que contiene el nombre del objeto que se desea eliminar o la posición ordinal (índice) del objeto en la colección.  
  
## <a name="remarks"></a>Observaciones  
 El uso del método **Delete** en una colección permite quitar uno de los objetos de la colección. Este método solo está disponible en la colección **Parameters** de un objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Debe usar la propiedad [Name](../../../ado/reference/ado-api/name-property-ado.md) del objeto [Parameter](../../../ado/reference/ado-api/parameter-object.md) o su índice de colección al llamar al método **Delete** : una variable de objeto no es un argumento válido.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933179"
---
# <a name="delete-method-ado-parameters-collection"></a>Método Delete (colección de parámetros de ADO)
Elimina un objeto desde el [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Index*  
 Un **cadena** valor que contiene el nombre del objeto que desea eliminar, o la posición del objeto ordinal (índice) en la colección.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **eliminar** método en una colección permite quitar uno de los objetos de la colección. Este método solo está disponible en el **parámetros** colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Debe usar el [parámetro](../../../ado/reference/ado-api/parameter-object.md) del objeto [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad o su índice de colección cuando se llama a la **eliminar** variable de objeto de un método no es un argumento válido.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Eliminar método (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

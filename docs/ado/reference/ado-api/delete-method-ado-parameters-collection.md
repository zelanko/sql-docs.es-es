---
title: Método Delete (colección de parámetros de ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c02a8b95a91c8f62f65db3ae9120f9aee7b31bd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="delete-method-ado-parameters-collection"></a>Método Delete (colección de parámetros de ADO)
Elimina un objeto de la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Index*  
 A **cadena** valor que contiene el nombre del objeto que desea eliminar o la posición ordinal del objeto (índice) de la colección.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **eliminar** método en una colección permite quitar uno de los objetos de la colección. Este método solo está disponible en la **parámetros** colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Debe utilizar el [parámetro](../../../ado/reference/ado-api/parameter-object.md) del objeto [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad o el índice de la colección cuando se llama a la **eliminar** método: una variable de objeto no es un argumento válido.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord (método, ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

---
title: Clear (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920064"
---
# <a name="clear-method-ado"></a>Clear (método) (ADO)
Quita todos los objetos de [error](../../../ado/reference/ado-api/error-object.md) de la colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Observaciones  
 Utilice el método **Clear** en la colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) para quitar todos los objetos de [error](../../../ado/reference/ado-api/error-object.md) existentes de la colección. Cuando se produce un error, ADO borra automáticamente la colección de **errores** y la rellena con objetos de **error** en función del nuevo error.  
  
 Algunas propiedades y métodos devuelven advertencias que aparecen como objetos de **error** en la colección de **errores** , pero no detienen la ejecución de un programa. Antes de llamar a los métodos [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) en un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ; el método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) en un objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) ; o bien, establezca la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) en un objeto de **conjunto de registros** , llame al método **Clear** en la colección de **errores** . De este modo, puede leer la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) de la colección de errores para probar si **hay** advertencias devueltas.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos Execute, Requery y Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Ejemplo de métodos Execute, Requery y Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Ejemplo de los métodos Execute, Requery y Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Propiedad Filter](../../../ado/reference/ado-api/filter-property.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

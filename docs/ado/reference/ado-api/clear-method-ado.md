---
title: "Clear (método) (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b843c14580d792dac671dfa198d23444829db78d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="clear-method-ado"></a>Clear (método) (ADO)
Quita todos los [Error](../../../ado/reference/ado-api/error-object.md) objetos desde la [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Comentarios  
 Use la **desactive** método en el [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección para quitar todas las existentes [Error](../../../ado/reference/ado-api/error-object.md) objetos de la colección. Cuando se produce un error, ADO borra automáticamente la **errores** colección y lo rellena con **Error** objetos basan en el nuevo error.  
  
 Algunos métodos y propiedades devuelven advertencias que aparecen como **Error** objetos en el **errores** colección, pero no detiene la ejecución del programa. Antes de llamar a la [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto; el [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto; o establecer el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad en un **Recordset** objeto, llame a la **borrar**método en el **errores** colección. De este modo, puede leer el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad de la **errores** colección y comprobar si devuelve advertencias.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Execute, Requery y Clear ejemplo de los métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery y Clear métodos ejemplo (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery y Clear ejemplo de los métodos (VC ++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Propiedad de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

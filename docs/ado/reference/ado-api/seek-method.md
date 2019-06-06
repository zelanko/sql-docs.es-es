---
title: Método Seek | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 21cb7f8773c0663d584f62bcaaaeab15c7eac108
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711425"
---
# <a name="seek-method"></a>El método de búsqueda
Busca el índice de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para localizar rápidamente la fila que coincide con los valores especificados y cambia la posición de fila actual para esa fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parámetros  
 *KeyValues*  
 Una matriz de **Variant** valores. Un índice consta de una o varias columnas y la matriz contiene un valor que se compara con cada columna correspondiente.  
  
 *SeekOption*  
 Un [SeekEnum](../../../ado/reference/ado-api/seekenum.md) valor que especifica el tipo de comparación entre las columnas del índice y la correspondiente *KeyValues*.  
  
## <a name="remarks"></a>Comentarios  
 Use la **Seek** método junto con el [índice](../../../ado/reference/ado-api/index-property.md) propiedad si el proveedor subyacente admite índices en el **Recordset** objeto. Use la [admite](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** método para determinar si el proveedor subyacente admite **Seek**y el **Supports** método para determinar si el proveedor admite los índices. (Por ejemplo, el [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) admite **Seek** y **índice**.)  
  
 Si **Seek** hace que no se encontró la fila deseada, ningún error se produce y la fila se coloca al final de la **Recordset**. Establecer el **índice** propiedad en el índice deseado antes de ejecutar este método.  
  
 Este método solo se admite con cursores de servidor. Buscar no se admite cuando la **Recordset** del objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) es el valor de propiedad **adUseClient**.  
  
 Este método solo se pueden usar cuando el **conjunto de registros** objeto se ha abierto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor de **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Seek y ejemplo de la propiedad de índice (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Método Seek y ejemplo de la propiedad Index (VC ++)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Buscar (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propiedad Index](../../../ado/reference/ado-api/index-property.md)

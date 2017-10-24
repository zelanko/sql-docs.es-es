---
title: "Método Seek | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d401bca51d735b2d0d633716cee732ad2ab9a086
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="seek-method"></a>El método de búsqueda
Busca el índice de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a encontrar rápidamente la fila que coincide con los valores especificados y cambia la posición de fila actual a dicha fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parámetros  
 *KeyValue*  
 Una matriz de **Variant** valores. Un índice consta de una o varias columnas y la matriz contiene un valor que se compara con cada columna correspondiente.  
  
 *SeekOption*  
 A [SeekEnum](../../../ado/reference/ado-api/seekenum.md) valor que especifica el tipo de comparación que se va a realizarse entre las columnas del índice y el correspondiente *KeyValue*.  
  
## <a name="remarks"></a>Comentarios  
 Use la **Seek** método junto con el [índice](../../../ado/reference/ado-api/index-property.md) propiedad si el proveedor subyacente admite índices en el **Recordset** objeto. Use la [admite](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** método para determinar si el proveedor subyacente admite **Seek**y el **Supports** método para determinar si el proveedor admite índices. (Por ejemplo, el [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) admite **Seek** y **índice**.)  
  
 Si **Seek** hace que no se encontró la fila deseada, ningún error se produce y la fila se coloca al final de la **conjunto de registros**. Establecer el **índice** propiedad en el índice deseado antes de ejecutar este método.  
  
 Este método es compatible sólo con cursores de servidor. Seek no se admite cuando la **Recordset** del objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) es el valor de la propiedad **adUseClient**.  
  
 Este método solo se pueden utilizar cuando la **conjunto de registros** objeto se ha abierto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor de **adCmdTableDirect**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Seek y ejemplo de la propiedad de índice (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Método Seek y ejemplo de la propiedad de índice (VC ++)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propiedad Index](../../../ado/reference/ado-api/index-property.md)


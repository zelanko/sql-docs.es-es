---
description: El método de búsqueda
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b9eecf5caee690687adaffda7ccd56d869abb9e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442106"
---
# <a name="seek-method"></a>El método de búsqueda
Busca el índice de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) para localizar rápidamente la fila que coincide con los valores especificados y cambia la posición de la fila actual a esa fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parámetros  
 *KeyValues*  
 Matriz de valores **Variant** . Un índice consta de una o más columnas y la matriz contiene un valor que se va a comparar con cada columna correspondiente.  
  
 *SeekOption*  
 Valor [SeekEnum](../../../ado/reference/ado-api/seekenum.md) que especifica el tipo de comparación que se va a realizar entre las columnas del índice y el valor de *keyValues*correspondiente.  
  
## <a name="remarks"></a>Observaciones  
 Use el método **Seek** junto con la propiedad de [Índice](../../../ado/reference/ado-api/index-property.md) si el proveedor subyacente admite índices en el objeto de **conjunto de registros** . Use el método [Supports](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** para determinar si el proveedor subyacente admite **Seek**y el método **Supports (adIndex)** para determinar si el proveedor admite índices. (Por ejemplo, el [proveedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) admite **Seek** e **index**).  
  
 Si **Seek** no encuentra la fila deseada, no se produce ningún error y la fila se coloca al final del conjunto de **registros**. Establezca la propiedad **index** en el índice deseado antes de ejecutar este método.  
  
 Este método solo se admite con los cursores del lado servidor. No se admite Seek cuando el valor de la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) del objeto de **conjunto de registros** es **adUseClient**.  
  
 Este método solo se puede usar cuando se ha abierto el objeto de **conjunto de registros** con el valor **adCmdTableDirect**de [commandtypeenum](../../../ado/reference/ado-api/commandtypeenum.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad index y el método Seek (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Ejemplo de la propiedad index y el método Seek (VC + +)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propiedad Index](../../../ado/reference/ado-api/index-property.md)

---
title: "GetChildren (método) (ADO) | Documentos de Microsoft"
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
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 84f146c110b50cc3c73329dd72feb26f1ebf3858
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getchildren-method-ado"></a>GetChildren (método) (ADO)
Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) cuyas filas representan los elementos secundarios de una colección [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **Recordset** objeto para el que cada fila representa un elemento secundario del elemento actual **registro** objeto. Por ejemplo, los elementos secundarios de un **registro** que representa un directorio serían los archivos y subdirectorios incluidos en el directorio principal.  
  
## <a name="remarks"></a>Comentarios  
 El proveedor determina qué columnas hay en el valor devuelto **conjunto de registros**. Por ejemplo, un proveedor de origen de documentos siempre devuelve un recurso **conjunto de registros**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|


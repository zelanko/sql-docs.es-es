---
title: GetChildren (método) (ADO) | Documentos de Microsoft
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
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 170f17c66ea05a3df7dc6135918d164bd66f993e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|

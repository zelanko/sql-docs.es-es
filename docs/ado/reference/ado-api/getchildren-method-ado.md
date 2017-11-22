---
title: "GetChildren (método) (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords: GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f9af9b4cb1b4648acc75389f7d75cccdc46b96
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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

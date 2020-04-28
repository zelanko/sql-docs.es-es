---
title: GetChildren (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84f1a2f7a80e17571f1b8ad3e63db640fb58dc19
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932503"
---
# <a name="getchildren-method-ado"></a>GetChildren (método) (ADO)
Devuelve un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) cuyas filas representan los elementos secundarios de un [registro](../../../ado/reference/ado-api/record-object-ado.md)de la colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto de **conjunto de registros** para el que cada fila representa un elemento secundario del objeto de **registro** actual. Por ejemplo, los elementos secundarios de un **registro** que representa un directorio serían los archivos y subdirectorios contenidos en el directorio primario.  
  
## <a name="remarks"></a>Observaciones  
 El proveedor determina qué columnas existen en el **conjunto de registros**devuelto. Por ejemplo, un proveedor de origen de documento siempre devuelve un **conjunto de registros**de recursos.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|

---
description: GetChildren (método) (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 906c20d19143f4f1e8fe0b6c1e91585893acfa5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443587"
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

:::row:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

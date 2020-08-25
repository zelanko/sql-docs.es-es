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
ms.openlocfilehash: d5d0ff58401e5294080c762c1e27f018630364f4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775104"
---
# <a name="getchildren-method-ado"></a>GetChildren (método) (ADO)
Devuelve un [conjunto de registros](./recordset-object-ado.md) cuyas filas representan los elementos secundarios de un [registro](./record-object-ado.md)de la colección.  
  
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
        [Objeto Record (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::
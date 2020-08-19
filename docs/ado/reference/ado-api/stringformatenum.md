---
description: StringFormatEnum
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: d7831d7be2df28d31c88216e67e16efbf611b858
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441787"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica el formato al recuperar un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) como una cadena.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita filas por *RowDelimiter*, columnas por *ColumnDelimiter*y valores NULL por *NullExpr*. Estos tres parámetros del método [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) solo son válidos con un *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. StringFormat. CLIPSTRING|  
  
## <a name="applies-to"></a>Se aplica a  
 [GetString (método) (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)

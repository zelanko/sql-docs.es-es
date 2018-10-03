---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2740c7fb25b71e3588bebb924ea9d5f907e3560
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657723"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica el formato al recuperar un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como una cadena.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita filas por *RowDelimiter*, las columnas por *ColumnDelimiter*y los valores por null *NullExpr*. Estos tres parámetros de la [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método solo son válidos con un *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Se aplica a  
 [GetString (método) (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)

---
title: StringFormatEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e6584a40917078c29e8fc619afb6a4f3bddd541
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica el formato al recuperar un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como una cadena.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita filas por *RowDelimiter*, las columnas por *ColumnDelimiter*y valores por null *NullExpr*. Estos tres parámetros de la [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método solo son válidos con un *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Se aplica a  
 [GetString (método) (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)

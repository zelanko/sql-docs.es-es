---
title: StringFormatEnum | Documentos de Microsoft
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
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332a19096035fc271062c8138351197316f46377
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
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

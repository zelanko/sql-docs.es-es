---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05af48f2edcdcf2c6adc6e3617860fdad38bde7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63314748"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica la dirección de una búsqueda de registros dentro de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Busca hacia atrás, deteniendo al principio de la **Recordset**. Si no se encuentra una coincidencia, se coloca el puntero de registro en [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Busca hacia delante, se detiene al final de la **Recordset**. Si no se encuentra una coincidencia, se coloca el puntero de registro en [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Se aplica a  
 [Find (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)

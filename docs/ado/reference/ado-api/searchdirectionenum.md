---
description: SearchDirectionEnum
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dc30978b5ce157aa103e41f2b68dd8b36864f25a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989232"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica la dirección de una búsqueda de registros dentro de un [conjunto de registros](./recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Busca hacia atrás y se detiene al principio del **conjunto de registros**. Si no se encuentra ninguna coincidencia, el puntero de registro se coloca en [BOF](./bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Busca hacia delante y se detiene al final del **conjunto de registros**. Si no se encuentra ninguna coincidencia, el puntero de registro se coloca en [EOF](./bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. SearchDirection. BACKWARD|  
|AdoEnums. SearchDirection. FORWARD|  
  
## <a name="applies-to"></a>Se aplica a  
 [Find (método) (ADO)](./find-method-ado.md)
---
title: MoveRecordOptionsEnum | Documentos de Microsoft
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
f1_keywords: MoveRecordOptionsEnum
helpviewer_keywords: MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d602d52933b6f940131ffbb9cbe9198e6c13699
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica el comportamiento de la [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Predeterminado: Realiza la operación mover predeterminada: la operación se produce un error si el archivo de destino o el directorio ya existe y la operación actualiza los vínculos de hipertexto.|  
|**adMoveOverWrite**|1|Sobrescribe el archivo de destino o el directorio, incluso si ya existe.|  
|**adMoveDontUpdateLinks**|2|Modifica el comportamiento predeterminado de **MoveRecord** método por no actualizar los vínculos de hipertexto del origen de **registro**. El comportamiento predeterminado depende de las capacidades del proveedor. La operación mover actualiza vínculos si el proveedor es compatible con. Si el proveedor no puede reparar vínculos, o si no se especifica este valor, a continuación, el movimiento se realiza correctamente incluso cuando vínculos no se ha corregido.|  
|**adMoveAllowEmulation**|4|Solicitudes que el proveedor intenta simular el movimiento (mediante la descarga y carga, las operaciones de eliminación). Si el intento de mover el **registro** produce un error porque la dirección URL de destino está en un servidor diferente o atendida por un proveedor diferente a la de origen, esto puede provocar una mayor latencia o pérdida de datos debido a las capacidades de un proveedor distinto cuando mover recursos entre proveedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

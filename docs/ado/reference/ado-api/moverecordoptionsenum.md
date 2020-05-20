---
title: MoveRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: rothja
ms.author: jroth
ms.openlocfilehash: 849f3720d831c17b6b9d6d2829ae0b28f19992de
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762446"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica el comportamiento del método [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) del objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Predeterminada. Realiza la operación de movimiento predeterminada: se produce un error en la operación si el archivo o directorio de destino ya existe y la operación actualiza los vínculos de hipertexto.|  
|**adMoveOverWrite**|1|Sobrescribe el archivo o directorio de destino, incluso si ya existe.|  
|**adMoveDontUpdateLinks**|2|Modifica el comportamiento predeterminado del método **MoveRecord** sin actualizar los vínculos de hipertexto del **registro**de origen. El comportamiento predeterminado depende de las capacidades del proveedor. La operación de movimiento actualiza los vínculos si el proveedor es compatible. Si el proveedor no puede corregir los vínculos o si no se especifica este valor, el movimiento se realizará correctamente aunque no se hayan corregido los vínculos.|  
|**adMoveAllowEmulation**|4|Solicita que el proveedor intente simular el movimiento (mediante operaciones de descarga, carga y eliminación). Si se produce un error al intentar mover el **registro** debido a que la dirección URL de destino está en un servidor diferente o se presta servicio a través de un proveedor diferente del de origen, esto puede provocar una mayor latencia o pérdida de datos, debido a diferentes capacidades de proveedor al trasladar recursos entre proveedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

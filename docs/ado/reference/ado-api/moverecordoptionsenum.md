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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcdb825073b267c3e3351001ecc7b11c969582e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932045"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica el comportamiento del método [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) del objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Default. Realiza la operación de movimiento predeterminada: se produce un error en la operación si el archivo o directorio de destino ya existe y la operación actualiza los vínculos de hipertexto.|  
|**adMoveOverWrite**|1|Sobrescribe el archivo o directorio de destino, incluso si ya existe.|  
|**adMoveDontUpdateLinks**|2|Modifica el comportamiento predeterminado del método **MoveRecord** sin actualizar los vínculos de hipertexto del **registro**de origen. El comportamiento predeterminado depende de las capacidades del proveedor. La operación de movimiento actualiza los vínculos si el proveedor es compatible. Si el proveedor no puede corregir los vínculos o si no se especifica este valor, el movimiento se realizará correctamente aunque no se hayan corregido los vínculos.|  
|**adMoveAllowEmulation**|4|Solicita que el proveedor intente simular el movimiento (mediante operaciones de descarga, carga y eliminación). Si se produce un error al intentar mover el **registro** debido a que la dirección URL de destino está en un servidor diferente o se presta servicio a través de un proveedor diferente del de origen, esto puede provocar una mayor latencia o pérdida de datos, debido a diferentes capacidades de proveedor al trasladar recursos entre proveedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

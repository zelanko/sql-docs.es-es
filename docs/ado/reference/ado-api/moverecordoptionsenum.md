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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932045"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica el comportamiento de la [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Predeterminado: Realiza la operación de movimiento predeterminado: La operación produce un error si el archivo de destino o directorio ya existe, y la operación actualiza los vínculos de hipertexto.|  
|**adMoveOverWrite**|1|Sobrescribe el archivo de destino o el directorio, incluso si ya existe.|  
|**adMoveDontUpdateLinks**|2|Modifica el comportamiento predeterminado de **MoveRecord** método si no actualiza los vínculos de hipertexto del origen de **registro**. El comportamiento predeterminado depende de las capacidades del proveedor. Mover la operación actualiza los vínculos si es compatible con el proveedor. Si el proveedor no puede reparar los vínculos, o si no se especifica este valor, el cambio tiene éxito incluso cuando vínculos no se han corregido.|  
|**adMoveAllowEmulation**|4|Solicitudes que el proveedor intenta simular el movimiento (mediante operaciones de eliminación, carga y descarga). Si el intento de mover el **registro** produce un error porque la dirección URL de destino está en un servidor diferente o atendida por un proveedor diferente de origen, esto provocaría un mayor latencia o pérdida de datos debido a las capacidades del proveedor diferente cuando mover recursos entre los proveedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

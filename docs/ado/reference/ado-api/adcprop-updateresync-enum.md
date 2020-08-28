---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2fcf60974612325e8af7501eaa6066d96d9f2985
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976826"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
Especifica si el método [UpdateBatch](./updatebatch-method.md) va seguido de una operación de método [Resync](./resync-method.md) implícita y, en caso afirmativo, el ámbito de esa operación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Invoca **Resync** con el valor combinado de todos los demás miembros de ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|Predeterminada. Intenta recuperar el nuevo valor de identidad para las columnas que se incrementan o generan automáticamente en el origen de datos, como los campos Autonuméricos de Microsoft Jet o las columnas de identidad de Microsoft SQL Server.|  
|**adResyncConflicts**|2|Invoca la **resincronización** de todas las filas en las que se produjo un error en la operación de actualización o eliminación debido a un conflicto de simultaneidad.|  
|**adResyncInserts**|8|Invoca **Resync** para todas las filas insertadas correctamente. Sin embargo, los valores de columna de incremento automático no se vuelven a sincronizar. En su lugar, el contenido de las filas recién insertadas se vuelve a sincronizar según el valor de clave principal existente. Si la clave principal es un valor de incremento automático, **Resync** no recuperará el contenido de la fila deseada. Para incrementar automáticamente los valores de clave principal de incremento automático, llame a **UpdateBatch** con el valor combinado **adResyncAutoIncrement**  +  **adResyncInserts**.|  
|**adResyncNone**|0|No invoca la **resincronización**.|  
|**adResyncUpdates**|4|Invoca **Resync** para todas las filas actualizadas correctamente.|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad dinámica Update Resync (ADO)](./update-resync-property-dynamic-ado.md)
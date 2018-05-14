---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 000c1bc15a0cbdba2c1614d085c9b083b872e917
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|511|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ROW_TOOBIG|  
|Texto del mensaje|No se puede crear una fila de tamaño %d que sea mayor que el máximo permitido de %d.|  
  
## <a name="explanation"></a>Explicación  
La operación que se ha intentado ha superado el tamaño máximo de una fila. Normalmente, el tamaño máximo de una fila es 8.060 bytes. Algunos formatos de almacenamiento contienen una sobrecarga que puede reducir el tamaño de fila disponible para datos. Por ejemplo, cuando se utilizan columnas dispersas, el tamaño máximo de una fila es 8.018 bytes. Algunas operaciones que agregan o quitan filas y algunas operaciones que cambian el tipo de datos de una columna requieren que se vuelva a escribir la fila en la página de datos y, a continuación, se quita la fila original. En estas operaciones, el límite real para el tamaño de la fila es la mitad del límite máximo. Esto se debe a que la fila original y la fila modificada deben estar en la página de datos durante un breve período de tiempo.  
  
## <a name="user-action"></a>Acción del usuario  
Si es posible, reduzca el tamaño de la fila.  
  
Si cree que el problema se debe a una actualización en contexto de la fila, debe cambiar la tabla en varios pasos. Cree una tabla nueva y transfiera los datos a dicha tabla. A continuación, elimine la tabla original y cambie el nombre de la nueva tabla; o bien, trunque la tabla original, modifique las filas en ella y, a continuación, vuelva a mover los datos a la citada tabla.  
  

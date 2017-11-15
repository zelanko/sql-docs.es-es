---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 4022d3e6a23d067d6b4f5ec91805d2d6ba37866b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
  
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
  

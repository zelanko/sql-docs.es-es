---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee53135fb492185d91287f553b7b1f0ddf3cc8ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867800"
---
# <a name="mssqlserver_511"></a>MSSQLSERVER_511
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|511|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ROW_TOOBIG|  
|Texto del mensaje|No se puede crear una fila de tamaño %d que sea mayor que el máximo permitido de %d.|  
  
## <a name="explanation"></a>Explicación  
 La operación que se ha intentado ha superado el tamaño máximo de una fila. Normalmente, el tamaño máximo de una fila es 8.060 bytes. Algunos formatos de almacenamiento contienen una sobrecarga que puede reducir el tamaño de fila disponible para datos. Por ejemplo, cuando se utilizan columnas dispersas, el tamaño máximo de una fila es 8.018 bytes. Algunas operaciones que agregan o quitan filas y algunas operaciones que cambian el tipo de datos de una columna requieren que se vuelva a escribir la fila en la página de datos y, a continuación, se quita la fila original. En estas operaciones, el límite real para el tamaño de la fila es la mitad del límite máximo. Esto se debe a que la fila original y la fila modificada deben estar en la página de datos durante un breve período de tiempo.  
  
> [!WARNING]  
>  Cada columna **VARCHAR (Max)** o **nvarchar (Max)** que no sea NULL requiere 24 bytes de asignación fija adicional que se recuenton con respecto al límite de filas de 8.060 bytes durante una operación de ordenación. Esto puede crear un límite implícito del número de columnas **VARCHAR (Max)** o **nvarchar (Max** ) no NULL que se pueden crear en una tabla. No se produce ningún error especial cuando se crea la tabla (más allá de la advertencia habitual de que el tamaño máximo de la fila supera el máximo permitido de 8060 bytes) ni en el momento de la inserción de los datos. Este tamaño de fila grande puede provocar errores (como el error 512) durante algunas operaciones normales, como una actualización de claves de índices agrupados u ordenaciones del conjunto completo de columnas, que los usuarios no pueden prever hasta que lleven a cabo alguna operación.  
  
## <a name="user-action"></a>Acción del usuario  
 Si es posible, reduzca el tamaño de la fila.  
  
 Si cree que el problema se debe a una actualización en contexto de la fila, debe cambiar la tabla en varios pasos. Cree una tabla nueva y transfiera los datos a dicha tabla. A continuación, elimine la tabla original y cambie el nombre de la nueva tabla; o bien, trunque la tabla original, modifique las filas en ella y, a continuación, vuelva a mover los datos a la citada tabla.  
  
  

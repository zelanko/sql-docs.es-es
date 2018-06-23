---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 76b05ac7adb3577d45657ad2bc772507f79e7dde
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111793"
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9003|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_INVALID_LSN|  
|Texto del mensaje|El número de examen del registro %S_LSN pasado al examen del registro de la base de datos '%.*ls' no es válido. This error may indicate data corruption or that the log file (.ldf) does not match the data file (.mdf). If this error occurred during replication, re-create the publication. De lo contrario, restaure la base de datos a partir de una copia de seguridad si el problema da lugar a un error durante el inicio.|  
  
## <a name="explanation"></a>Explicación  
 Un componente pasó un número de flujo de registro no válido al administrador de registros para la base de datos. Podría corresponder a la replicación, a daños o a una incoherencia entre el archivo de datos principal y el registro.  
  
## <a name="user-action"></a>Acción del usuario  
 Si esto ocurrió durante la replicación, vuelva a crear la publicación. De lo contrario, restaure una copia de seguridad.  
  
  
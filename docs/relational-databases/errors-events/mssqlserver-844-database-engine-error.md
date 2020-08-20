---
description: MSSQLSERVER_844
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6b92d297b2e948baadf30947ba51cee48822120
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499466"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|844|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|BUFLATCH_TIMEOUT_CONTINUE|  
|Texto del mensaje|Tiempo de espera agotado mientras se esperaba el bloqueo temporal del búfer -- tipo %d, bp %p, página %d:%d, stat %#x, id. de base de datos: %d, id. de unidad de asignación: %I64d%ls, tarea 0x%p : %d, tiempo de espera %d, marcas 0x%I64x, tarea propietaria 0x%p.  Esperando.|  
  
## <a name="explanation"></a>Explicación  
Un proceso está esperando para adquirir un bloqueo temporal. Este problema puede estar causado por una operación de E/S que está tardando mucho en llevarse a cabo. Normalmente, este tipo de error es el resultado de que otras tareas estén bloqueando los procesos del sistema. En algunos casos, este error puede ser el resultado de un error de hardware.  
  
## <a name="user-action"></a>Acción del usuario  
Para evitar que ocurra este error, intente lo siguiente:  
  
-   Reduzca la carga de trabajo.  
  
-   Busque errores de E/S asociados en el registro de errores o el registro de eventos. Normalmente, los errores de E/S indican un funcionamiento incorrecto del disco.  
  
-   Compruebe el registro de errores para ver si hay tareas que no rinden y otros errores críticos.  
  
-   Si se producen frecuentemente errores críticos, como aserciones, solucione estos problemas.  
  
Si el error persiste, póngase en contacto con el servicio de Soporte técnico y Atención al cliente de Microsoft.  
  

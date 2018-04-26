---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0b42ca15cda763ed914bf895d575dad039bf2cf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|825|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|B_RETRYWORKED|  
|Texto del mensaje|Se realizó correctamente una operación de lectura del archivo '%ls' en el desplazamiento %#016I64x después de %d intentos sin éxito: %ls. Encontrará más detalles en los mensajes adicionales del registro de errores de SQL Server y el registro de eventos del sistema. Este estado de error amenaza la integridad de la base de datos y debe ser rectificado. Ejecute una comprobación de coherencia completa de la base de datos (DBCC CHECKDB). Este error puede deberse a muchos factores. Para obtener más información vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que la operación de lectura tenía que volver a emitirse al menos una vez e indica un problema más importante con el hardware del disco. Este mensaje no indica actualmente un problema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sino que el problema del disco podría provocar la pérdida de datos o daños en la base de datos si no se resuelve. El registro de eventos del sistema puede contener eventos relacionados que ayuden a diagnosticar el problema. Para obtener más información sobre los errores de E/S, vea el [capítulo 2 del documento sobre conceptos básicos de E/S de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Acción del usuario  
Las siguientes acciones pueden ayudarle a identificar y resolver el problema subyacente:  
  
-   Revise el registro de errores y el texto variable de este mensaje para obtener pistas que expliquen el problema.  
  
-   Compruebe su sistema de disco. El problema podría estar relacionado con discos, controladores de discos, tarjetas de matriz o unidades de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las utilidades más recientes a fin de comprobar el estado del sistema de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las últimas actualizaciones del controlador.  
  

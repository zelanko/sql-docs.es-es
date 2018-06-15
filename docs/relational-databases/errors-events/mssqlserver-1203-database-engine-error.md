---
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c283411d8b2508a931a8fb66873e37985ae86cd
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323796"
---
# <a name="mssqlserver1203"></a>MSSQLSERVER_1203
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1203|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LK_NOT|  
|Texto del mensaje|El Id. de proceso %d intentó desbloquear un recurso que no es de su propiedad: %.*ls. Vuelva a intentar repetir la transacción porque este error puede producirse por una condición de sincronización. Si el problema persiste, póngase en contacto con el administrador de la base de datos.|  
  
## <a name="explanation"></a>Explicación  
Este error se genera cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ocupado en alguna actividad diferente a la limpieza de estado posterior al procesamiento y descubre que la página que está intentando desbloquear está ya desbloqueada.  
  
### <a name="possible-causes"></a>Posibles causas  
Es posible que la causa subyacente de este error esté relacionada con problemas estructurales dentro de la base de datos afectada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra la adquisición y liberación de las páginas para mantener el control de simultaneidad en el entorno multiusuario. Este mecanismo se mantiene usando varias estructuras de bloqueo internas que identifican la página y el tipo de bloqueo existente. Los bloqueos se adquieren para el procesamiento de páginas afectadas y liberadas cuando el procesamiento finaliza.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute DBCC CHECKDB en la base de datos a la que pertenece el objeto. Si DBCC CHECKDB no notifica errores, intente restablecer la conexión y ejecutar el comando.  
  
> [!IMPORTANT]  
> Si está ejecutando DBCC CHECKDB con una de las cláusulas REPAIR y no se corrige el problema de índice, o si no está seguro del efecto que DBCC CHECKDB con una cláusula REPAIR produce en los datos, póngase en contacto con el proveedor principal de soporte.  
  

---
title: MSSQLSERVER_3314 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3314 (Database Engine error)
ms.assetid: f3a5ca6a-b502-4cab-b3b1-4bc753763fa9
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69f5b0467ef44a60102d36dd49fb1090d20cc8a8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407664"
---
# <a name="mssqlserver3314"></a>MSSQLSERVER_3314
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3314|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ERR_LOG_RID2|  
|Texto del mensaje|Durante la puesta al día de una operación registrada en la base de datos '%.*ls', se produjo un error en la entrada de registro con id. %S_LSN. Normalmente, el error específico se registra antes como un error en el servicio Registro de eventos de Windows. Restaure la base de datos o el archivo a partir de una copia de seguridad completa o repare la base de datos.|  
  
## <a name="explanation"></a>Explicación  
 Este es un error de acumulación de la recuperación de una operación de deshacer. Este error ha colocado la base de datos en el estado SUSPECT. El grupo de archivos principal, y posiblemente otros grupos de archivos, es sospechoso y puede estar dañado. La base de datos no se puede recuperar durante el inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, por consiguiente, no está disponible. Se requiere una acción por parte del usuario para resolver el problema.  
  
 Tenga en cuenta que si este error se produce para **tempdb**, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cierra.  
  
## <a name="user-action"></a>Acción del usuario  
 Una condición transitoria que se dio en el sistema durante un intento determinado de iniciar la instancia del servidor o recuperar una base de datos puede producir este error. También puede deberse a un error permanente que se produce cada vez que se intenta iniciar la base de datos. Para obtener información acerca de la causa, examine el registro de eventos de Windows para ver si contiene un error anterior que indique el error concreto.  
  
 Para obtener información sobre la causa de esta repetición del error 3314, busque en el registro de eventos de Windows un error anterior que indique el error específico. La acción del usuario adecuada depende de si la información del registro de eventos de Windows indica que el error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo causó una condición transitoria o un error permanente. Para obtener información sobre las acciones del usuario para solucionar el error 3314, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  

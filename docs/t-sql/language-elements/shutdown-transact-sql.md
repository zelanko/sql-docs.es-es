---
title: SHUTDOWN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4cf8ea2b61d4f1acb69ea489a5116a701264469
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server se detiene inmediatamente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NOWAIT  
 Opcional. Cierra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin ejecutar puntos de comprobación en cada base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cierra tras intentar finalizar todos los procesos de usuario. Cuando el servidor se reinicia, se produce una operación de reversión para las transacciones incompletas.  
  
## <a name="remarks"></a>Comentarios  
 A menos que se utiliza la opción WITHNOWAIT, SHUTDOWN cierra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por:  
  
1.  Deshabilitar los inicios de sesión (excepto para los miembros de la **sysadmin** y **serveradmin** roles fijos de servidor).  
  
    > [!NOTE]  
    >  Para mostrar una lista de todos los usuarios actuales, ejecute **sp_who**.  
  
2.  Esperar a que terminen las instrucciones Transact-SQL o los procedimientos almacenados que se están ejecutando. Para mostrar una lista de todos los procesos y bloqueos activos, ejecute **sp_who** y **sp_lock**, respectivamente.  
  
3.  Insertar un punto de comprobación en cada base de datos.  
  
 Usar la instrucción SHUTDOWN minimiza la cantidad trabajo de recuperación automática necesario cuando los miembros de la **sysadmin** fijo reinicio del rol de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 También se pueden utilizar otros métodos y herramientas para detener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada uno de ellos emite un punto de comprobación en todas las bases de datos. Puede vaciar los datos confirmados de la caché de datos y detener el servidor.  
  
-   Con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Mediante la ejecución de **net stop mssqlserver** desde un símbolo del sistema para una instancia predeterminada, o bien ejecutando **net stop mssql$ *** nombreDeInstancia* desde un símbolo del sistema para una instancia con nombre.  
  
-   Con Servicios del Panel de control.  
  
 Si **sqlservr.exe** se inició desde el símbolo del sistema, al presionar CTRL+C se cierra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, al presionar CTRL+C no se inserta ningún punto de comprobación.  
  
> [!NOTE]  
>  Al usar cualquiera de estos métodos para detener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se envía el mensaje `SERVICE_CONTROL_STOP` a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Permisos de SHUTDOWN se asignan a los miembros de la **sysadmin** y **serveradmin** roles fijos de servidor y no son transferibles.  
  
## <a name="see-also"></a>Vea también  
 [Punto de comprobación &#40; Transact-SQL &#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr (aplicación)](../../tools/sqlservr-application.md)   
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  

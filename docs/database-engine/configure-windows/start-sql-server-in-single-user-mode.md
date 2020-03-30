---
title: Iniciar SQL Server en modo de usuario único | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1cb488b6ce3dc21567b4f64738f9c26910c61f17
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68037163"
---
# <a name="start-sql-server-in-single-user-mode"></a>Iniciar SQL Server en modo de usuario único
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En determinadas circunstancias, puede que sea necesario iniciar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único mediante la **opción de inicio -m.** Por ejemplo, es posible que desee cambiar las opciones de configuración del servidor o recuperar una base de datos maestra dañada u otra base de datos del sistema. Ambas acciones requieren que se inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único.  
  
 Al iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único se permite que cualquier miembro del grupo local de administradores del equipo se conecte a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como miembro del rol fijo de servidor sysadmin. Para obtener más información, vea [Conectarse a SQL Server cuando los administradores del sistema no tienen acceso](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Tenga en cuenta los siguientes aspectos cuando inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único:  
  
-   Solo se podrá conectar al servidor un único usuario.  
  
-   No se ejecuta el proceso CHECKPOINT. De manera predeterminada, se ejecuta automáticamente en el inicio.  
  
> [!NOTE]  
>  Detenga el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único; de lo contrario, el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizará la conexión y, por tanto, la bloqueará.  
  
Al iniciar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se podría producir un error en el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] porque requiere más de una conexión para algunas operaciones. Para administrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único, ejecute las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] conectándose solo a través del Editor de consultas de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]o use la [utilidad sqlcmd](../../tools/sqlcmd-utility.md).  
  
Cuando use la opción **-m** con **SQLCMD** o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], puede limitar las conexiones a una aplicación cliente especificada. 

> [!NOTE]
> En Linux, **SQLCMD** debe escribirse en mayúsculas como se muestra.

Por ejemplo, **-m"SQLCMD"** limita las conexiones a una conexión única y esa conexión se debe identificar como el programa cliente **SQLCMD**. Use esta opción cuando esté iniciando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único y una aplicación cliente desconocida esté usando la única conexión disponible. Para conectarse a través del Editor de consultas en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use **-m"Microsoft SQL Server Management Studio - Query"** .  
  
> [!IMPORTANT]  
>  No use esta opción como una característica de seguridad. La aplicación cliente proporciona el nombre de la misma y puede proporcionar un nombre falso como parte de la cadena de conexión.  
  
## <a name="note-for-clustered-installations"></a>Nota para instalaciones en clúster  
 Para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno en clúster, cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia en modo de usuario único, la DLL de recursos de clúster utiliza la conexión disponible, con lo que impide cualquier otra conexión con el servidor. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en este estado, si se intenta poner en línea el recurso del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede producir la conmutación por error del recurso de SQL a otro nodo si el recurso está configurado para afectar al grupo.  
  
 Para solucionar el problema, utilice el procedimiento siguiente:  
  
1.  Quite el parámetro de inicio -m de las propiedades avanzadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Ponga sin conexión el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Desde el nodo de propietario actual de este grupo, ejecute el comando siguiente en el símbolo del sistema:  
    net start MSSQLSERVER /m.  
  
4.  Compruebe en el administrador de clústeres o en la consola de administración de clústeres de conmutación por error que el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sigue estando sin conexión.  
  
5.  Conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando ahora el siguiente comando y realice la operación necesaria: SQLCMD -E -S\<nombreDeServidor>.  
  
6.  Una vez completada la operación, cierre el símbolo del sistema y vuelva a poner en línea SQL y otros recursos mediante el administrador de clústeres.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar, detener o pausar el servicio del Agente SQL Server](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)   
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  

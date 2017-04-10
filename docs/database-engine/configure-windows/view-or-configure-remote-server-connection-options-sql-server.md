---
title: "Ver o configurar las opciones de conexi&#243;n de servidor remoto (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servidores remotos [SQL Server], opciones de conexión"
  - "servidores [SQL Server], remotos"
  - "conexiones [SQL Server], servidores remotos"
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Ver o configurar las opciones de conexi&#243;n de servidor remoto (SQL Server)
  En este tema se describe cómo ver o configurar las opciones de conexión de servidor remoto en el nivel de servidor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver o configurar las opciones de conexión de servidor remoto, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar las opciones de conexión de servidor remoto](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 La ejecución de **sp_serveroption** requiere el permiso ALTER ANY LINKED SERVER en el servidor.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para ver o configurar las opciones de conexión de servidor remoto  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y, luego, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades de SQL Server - \<***nombre_servidor***>**, haga clic en **Conexiones**.  
  
3.  En la página **Conexiones** , revise las opciones de configuración de **Conexiones a servidores remotos** y modifíquelas si es necesario.  
  
4.  Repita los pasos 1 a 3 en el otro servidor de la pareja de servidores remotos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para ver las opciones de conexión de servidor remoto  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usa [sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md) para devolver información sobre todos los servidores remotos.  
  
```tsql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### Para configurar las opciones de conexión de servidor remoto  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_serveroption](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md) para configurar un servidor remoto. En el ejemplo siguiente se configura un servidor remoto que corresponde a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SEATTLE3`, para que sea compatible con la intercalación de la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```tsql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> Seguimiento: después de configurar las opciones de conexión de servidor remoto  
 El servidor remoto debe detenerse e reiniciarse para que la opción de configuración valor surta efecto.  
  
## Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)   
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
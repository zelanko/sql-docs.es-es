---
title: Ver o cambiar las propiedades del servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c5ff985b62e39287b696e96f10142daf90ae0a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783124"
---
# <a name="view-or-change-server-properties-sql-server"></a>Ver o cambiar las propiedades del servidor (SQL Server)
  En este tema se describe cómo ver o cambiar las propiedades de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o el Administrador de configuración de SQL Server.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para ver o cambiar las propiedades del servidor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Administrador de configuración de SQL Server](#PowerShellProcedure)  
  
-   **Seguimiento:**  [después de cambiar propiedades del servidor](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando utilice sp_configure, deberá ejecutar RECONFIGURE o RECONFIGURE WITH OVERRIDE después de establecer una opción de configuración. La instrucción RECONFIGURE WITH OVERRIDE se suele reservar para opciones de configuración que deberían utilizarse con extrema precaución. No obstante, RECONFIGURE WITH OVERRIDE funciona con todas las opciones de configuración y puede utilizarlo en lugar de RECONFIGURE.  
  
    > [!NOTE]  
    >  RECONFIGURE se ejecuta en una transacción. Si una de las operaciones de reconfiguración genera un error, ninguna de estas operaciones surtirá efecto.  
  
-   Algunas páginas de propiedades presentan información obtenida mediante Instrumental de administración de Windows (WMI). Para mostrar dichas páginas, WMI debe estar instalado en el equipo en el que se ejecuta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para obtener más información, vea [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md).  
  
 De forma predeterminada `sp_configure` , los permisos de ejecución en sin parámetros o con solo el primer parámetro se conceden a todos los usuarios. Para ejecutar `sp_configure` con ambos parámetros para cambiar una opción de configuración o ejecutar la instrucción RECONFIGURE, se debe conceder al usuario el permiso de nivel de servidor Alter Settings. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>Para ver o cambiar las propiedades del servidor  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y luego haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades del servidor** , haga clic en una página para ver o cambiar la información de servidor acerca de dicha página. Algunas propiedades son de solo lectura.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>Para ver las propiedades del servidor mediante la función integrada SERVERPROPERTY  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se emplea la función integrada [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) en una instrucción `SELECT` para devolver información sobre el servidor actual. Este escenario es útil cuando hay varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en un servidor basado en Windows y el cliente debe abrir otra conexión a la misma instancia usada por la conexión actual.  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>Para ver las propiedades del servidor mediante la vista de catálogo sys.servers  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se consulta la vista de catálogo [sys.servers](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql) para devolver el nombre (`name`) y el identificador (`server_id`) del servidor actual, además del nombre del proveedor OLE DB (`provider`) para conectarse a un servidor vinculado.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysconfigurations-catalog-view"></a>Para ver las propiedades del servidor mediante la vista de catálogo sys.configurations  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se consulta la vista de catálogo [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) para devolver información sobre cada opción de configuración del servidor actual. El ejemplo devuelve el nombre (`name`) y la descripción (`description`) de la opción y si se trata de una opción avanzada (`is_advanced`).  
  
    ```sql
    USE AdventureWorks2012;
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;
    GO
    ```  
  
#### <a name="to-change-a-server-property-by-using-sp_configure"></a>Para cambiar una propiedad del servidor mediante sp_configure  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para cambiar una propiedad del servidor. El ejemplo cambia el valor de la opción `fill factor` a `100`. El servidor debe reiniciarse para que el cambio surta efecto.  
  
```sql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="PowerShellProcedure"></a> Usar el Administrador de configuración de SQL Server  
 Algunas propiedades del servidor se pueden ver o cambiar mediante el Administrador de configuración de SQL Server. Por ejemplo, puede ver la versión y la edición de la instancia de SQL Server, o cambiar la ubicación donde se almacenan los archivos de registro de errores. Estas propiedades también se pueden ver si se consultan las [Funciones y vistas de administración dinámica relacionadas con servidores](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql).  
  
#### <a name="to-view-or-change-server-properties"></a>Para ver o cambiar las propiedades del servidor  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
2.  En **Administrador de configuración de SQL Server**, haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón secundario en **SQL Server (\<***nombreDeInstancia***>)** y, a continuación, haga clic en **propiedades**.  
  
4.  En el cuadro de diálogo **propiedades de SQL Server (\<***nombreDeInstancia***>)** , cambie las propiedades del servidor en las pestañas **servicio** o **avanzadas** y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="follow-up-after-you-change-server-properties"></a><a name="FollowUp"></a> Seguimiento: después de cambiar propiedades del servidor  
 Para algunas propiedades, puede que sea necesario reiniciar el servidor para que el cambio surta efecto.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Funciones de configuración &#40;Transact-SQL&#41;](/sql/t-sql/functions/configuration-functions-transact-sql)   
 [Funciones y vistas de administración dinámica relacionadas con servidores &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql)  

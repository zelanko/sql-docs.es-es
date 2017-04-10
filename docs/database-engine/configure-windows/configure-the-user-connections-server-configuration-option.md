---
title: "Establecer la opci&#243;n de configuraci&#243;n del servidor Conexiones de usuario | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "simultáneas, conexiones [SQL Server]"
  - "opción de conexiones de usuario [SQL Server]"
  - "usuarios [SQL Server], conexiones simultáneas"
  - "número máximo de conexiones de usuario simultáneas"
  - "conexiones [SQL Server], simultáneas"
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Establecer la opci&#243;n de configuraci&#243;n del servidor Conexiones de usuario
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo establecer la opción de configuración del servidor **conexiones de usuario** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **conexiones de usuario** especifica el número máximo de conexiones de usuario simultáneas que se permiten en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número real de conexiones de usuario permitidas depende también de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se use y de los límites de las aplicaciones y del hardware. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite un máximo de 32.767 conexiones de usuario. Como la opción **user connections** es una opción dinámica (autoconfiguración), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta automáticamente el número máximo de conexiones de usuario a medida que se necesitan, hasta el valor máximo permitido. Por ejemplo, si solo 10 usuarios han iniciado una sesión, se asignan 10 objetos de conexión de usuario. En la mayoría de los casos, no es necesario cambiar el valor de esta opción. El valor predeterminado es 0, lo que significa que se permite un máximo de 32 767 conexiones de usuario.  
  
 Para determinar el número máximo de conexiones de usuario que el sistema permite, puede ejecutar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) o consultar la vista de catálogo [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de conexiones de usuario, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de conexiones de usuario](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   Usar la opción de **conexiones de usuario** ayuda a evitar que el servidor se sobrecargue con demasiadas conexiones simultáneas. Puede calcular el número de conexiones basándose en los requisitos del sistema y de los usuarios. Por ejemplo, en un sistema con muchos usuarios, cada usuario no necesitará normalmente una conexión exclusiva. Los usuarios pueden compartir las conexiones. Los usuarios que ejecutan aplicaciones de OLE DB necesitan una conexión para cada objeto de conexión abierta, los que ejecutan aplicaciones de Conectividad abierta de bases de datos (ODBC) necesitan una conexión para cada controlador de conexión activo de la aplicación y los que ejecutan aplicaciones de DB-Library necesitan una conexión para cada proceso iniciado que llame a la función **dbopen** de DB-Library.  
  
    > [!IMPORTANT]  
    >  Si tiene que utilizar esta opción, no establezca un valor demasiado alto, ya que cada conexión tiene sobrecarga, independientemente de si la conexión se está utilizando. Si se supera el número máximo de conexiones de usuario, recibirá un mensaje de error y no podrá conectarse hasta que esté disponible otra conexión.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el nivel de servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para configurar la opción de conexiones de usuario  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y haga clic en **Propiedades**.  
  
2.  Haga clic en el nodo **Conexiones** .  
  
3.  En **Conexiones**, en el cuadro **Número máximo de conexiones simultáneas** , escriba o seleccione un valor entre 0 y 32767 para establecer el número máximo de usuarios que se pueden conectar simultáneamente a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para configurar la opción de conexiones de usuario  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar el valor de la opción de `user connections` en `325` usuarios.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de conexiones de usuario  
 El servidor debe reiniciarse para que el valor surta efecto.  
  
## Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
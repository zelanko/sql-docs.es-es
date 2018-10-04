---
title: Establecer la opción de configuración del servidor Conexiones de usuario | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- simultaneous connections [SQL Server]
- user connections option [SQL Server]
- users [SQL Server], simultaneous connections
- maximum number of simultaneous user connections
- connections [SQL Server], simultaneous
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1d1d29ee5c4fcfc7b13267e6ea4e6b0e96d1269
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122315"
---
# <a name="configure-the-user-connections-server-configuration-option"></a>Establecer la opción de configuración del servidor Conexiones de usuario
  En este tema se describe cómo establecer la opción de configuración del servidor **conexiones de usuario** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **conexiones de usuario** especifica el número máximo de conexiones de usuario simultáneas que se permiten en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número real de conexiones de usuario permitidas depende también de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se use y de los límites de las aplicaciones y del hardware. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite un máximo de 32.767 conexiones de usuario. Como la opción **user connections** es una opción dinámica (autoconfiguración), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta automáticamente el número máximo de conexiones de usuario a medida que se necesitan, hasta el valor máximo permitido. Por ejemplo, si solo 10 usuarios han iniciado una sesión, se asignan 10 objetos de conexión de usuario. En la mayoría de los casos, no es necesario cambiar el valor de esta opción. El valor predeterminado es 0, lo que significa que se permite un máximo de 32 767 conexiones de usuario.  
  
 Para determinar el número máximo de conexiones de usuario que el sistema permite, puede ejecutar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) o consultar la vista de catálogo [sys.configuration](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) .  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de conexiones de usuario, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de conexiones de usuario](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   Usar la opción de **conexiones de usuario** ayuda a evitar que el servidor se sobrecargue con demasiadas conexiones simultáneas. Puede calcular el número de conexiones basándose en los requisitos del sistema y de los usuarios. Por ejemplo, en un sistema con muchos usuarios, cada usuario no necesitará normalmente una conexión exclusiva. Los usuarios pueden compartir las conexiones. Los usuarios que ejecutan aplicaciones de OLE DB necesitan una conexión para cada objeto de conexión abierta, los que ejecutan aplicaciones de Conectividad abierta de bases de datos (ODBC) necesitan una conexión para cada controlador de conexión activo de la aplicación y los que ejecutan aplicaciones de DB-Library necesitan una conexión para cada proceso iniciado que llame a la función **dbopen** de DB-Library.  
  
    > [!IMPORTANT]  
    >  Si tiene que utilizar esta opción, no establezca un valor demasiado alto, ya que cada conexión tiene sobrecarga, independientemente de si la conexión se está utilizando. Si se supera el número máximo de conexiones de usuario, recibirá un mensaje de error y no podrá conectarse hasta que esté disponible otra conexión.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-the-user-connections-option"></a>Para configurar la opción de conexiones de usuario  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y haga clic en **Propiedades**.  
  
2.  Haga clic en el nodo **Conexiones** .  
  
3.  En **Conexiones**, en el cuadro **Número máximo de conexiones simultáneas** , escriba o seleccione un valor entre 0 y 32767 para establecer el número máximo de usuarios que se pueden conectar simultáneamente a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-user-connections-option"></a>Para configurar la opción de conexiones de usuario  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para configurar el valor de la opción de `user connections` en `325` usuarios.  
  
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
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de conexiones de usuario  
 El servidor debe reiniciarse para que el valor surta efecto.  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  

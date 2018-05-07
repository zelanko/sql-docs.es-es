---
title: 'Tutorial: Preparar SQL Server para la replicación: publicador, distribuidor, suscriptor | Microsoft Docs'
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1468095ba959f7baf383b68cfaab65dab2591af6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriber"></a>Tutorial: Preparar SQL Server para la replicación: publicador, distribuidor, suscriptor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Es importante planificar la seguridad antes de configurar la topología de replicación. En este tutorial se muestra cómo proteger una topología de replicación y cómo configurar la distribución, que es el primer paso en la replicación de datos. Debe finalizar este tutorial antes que cualquiera de los otros tutoriales.  
  
> [!NOTE]  
> Para replicar datos de forma segura entre servidores, debe implementar todas las recomendaciones de [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
Este tutorial le enseñará a preparar un servidor de manera que la replicación se ejecute de forma segura con los privilegios mínimos.  

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Crear cuentas de Windows para replicación
> * Preparar la carpeta de instantáneas
> * Configurar la distribución

## <a name="prerequisites"></a>Prerequisites
Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación. 

Para completar este tutorial, el sistema debe tener SQL Server Management Studio (SSMS) y los siguientes componentes:  
  
-   En el publicador (servidor de origen):  
  
    -   Cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto SQL Server Express o SQL Compact. Estas ediciones no pueden ser publicadores de replicación.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] Base de datos de ejemplo. Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada.  
  
-   En el suscriptor (servidor de destino):  
  
    -   Cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] no puede ser un suscriptor de replicación transaccional.  
  
- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obtener instrucciones sobre cómo restaurar una base de datos en SSMS, vea [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
    
>[!NOTE]
> - La replicación no se admite entre SQL Server que estén separados por más de dos versiones entre sí. Para obtener más información, vea [Versiones de SQL admitidas en la topología de replicación](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], debe conectarse al publicador y al suscriptor con un inicio de sesión que sea miembro del rol fijo de servidor **sysadmin** . Para obtener más información sobre el rol sysadmin, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  


**Tiempo estimado para completar este tutorial: 30 minutos**
  
## <a name="create-windows-accounts-for-replication"></a>Crear cuentas de Windows para replicación
En esta sección creará cuentas de Windows para ejecutar agentes de replicación. Creará distintas cuentas de Windows en el servidor local para los siguientes agentes:  
  
|Agente|Ubicación|Nombre de cuenta|  
|---------|------------|----------------|  
|Agente de instantáneas|publicador|<*nombreDeEquipo*>\repl_snapshot|  
|Agente de registro del LOG|publicador|<*nombreDeEquipo*>\repl_logreader|  
|Agente de distribución|Publicador y suscriptor|<*nombreDeEquipo*>\repl_distribution|  
|Agente de mezcla|Publicador y suscriptor|<*nombreDeEquipo*>\repl_merge|  
  
> [!NOTE]  
> En los tutoriales de replicación, el publicador y el distribuidor comparten la misma instancia (NODE1\SQL2016) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mientras que la instancia del suscriptor (NODE2\SQL2016) es remota. El publicador y el suscriptor pueden compartir la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque no es necesario. Si el publicador y el suscriptor comparten la misma instancia, no se requieren los pasos que se utilizan para crear las cuentas en el suscriptor.  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Crear cuentas locales de Windows para agentes de replicación en el publicador
  
1.  En el publicador, vaya al Panel de control y abra **Administración de equipos** en **Herramientas administrativas** .  
  
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**.  
  
3.  Haga clic con el botón derecho en **Usuarios** y, después, seleccione **Usuario nuevo**.  
     
4.  Escriba **repl_snapshot** en el cuadro **Nombre de usuario**, proporcione la contraseña y demás información relevante y, después, seleccione **Crear** para crear la cuenta repl_snapshot: 

       ![Nuevo usuario](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5.  Repita el paso anterior para crear las cuentas repl_logreader, repl_distribution y repl_merge:  
 
    ![Usuarios de replicación](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6.  Seleccione **Cerrar**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Para crear cuentas locales de Windows para agentes de replicación en el suscriptor  
  
1.  En el suscriptor, vaya al Panel de control y abra **Administración de equipos** en **Herramientas administrativas** .  
  
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**.  
  
3.  Haga clic con el botón derecho en **Usuarios** y, después, seleccione **Usuario nuevo**.  
  
4.  Escriba **repl_distribution** en el cuadro **Nombre de usuario**, proporcione la contraseña y demás información relevante y, después, seleccione **Crear** para crear la cuenta repl_distribution.  
  
5.  Repita el paso anterior para crear la cuenta repl_merge.  
  
6.  Seleccione **Cerrar**.  

**Vea también**: [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  

## <a name="prepare-the-snapshot-folder"></a>Preparar la carpeta de instantáneas
En esta sección aprenderá a configurar la carpeta de instantáneas que se utiliza para crear y almacenar la instantánea de publicación. 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Crear un recurso compartido para la carpeta de instantáneas y asignar permisos  
  
1.  En el Explorador de Windows, navegue a la carpeta de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La ubicación predeterminada es C:\Archivos de programa\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Cree una carpeta con el nombre **repldata**.  
  
3.  Haga clic con el botón derecho en esta carpeta y seleccione **Propiedades**.  
  
    A. En la pestaña **Compartir** del cuadro de diálogo **Propiedades de repldata**, seleccione **Uso compartido avanzado**.  
  
    B. En el cuadro de diálogo **Uso compartido avanzado**, seleccione **Compartir esta carpeta**y, después, seleccione **Permisos**:  

       ![Compartir datos de replicación](media/tutorial-preparing-the-server-for-replication/repldata.png)

6.  En el cuadro de diálogo **Permisos de repldata**, seleccione **Agregar**. En el cuadro de texto **Seleccionar usuarios, equipos, cuentas de servicio o grupos**, escriba el nombre de la cuenta del Agente de instantáneas creado anteriormente, como <*Nombre_De_Equipo_Publicador>***\repl_snapshot**. Seleccione **Comprobar nombres**y, después, seleccione **Aceptar**:  

    ![Agregar permisos de uso compartido](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. Repita el paso 6 para agregar las otras dos cuentas que se crearon previamente: <*Nombre_De_Equipo_Publicador>***\repl_merge** y <*Nombre_De_Equipo_Publicador>***\repl_distribution**

8. Una vez que se hayan agregado estas tres cuentas, asigne los permisos siguientes:      
    - repl_distribution - Lectura  
    - repl_merge - Lectura  
    - repl_snapshot - Control total    

  ![Permisos de los recursos compartidos](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. Después de configurar correctamente los permisos de los recursos compartidos, seleccione **Aceptar** para cerrar el cuadro de diálogo **Permisos de repldata**. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Uso compartido avanzado**. 

10.  En las **Propiedades de repldata**, seleccione la pestaña **Seguridad** y seleccione **Editar**:  

       ![Modificar seguridad](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. En el cuadro de diálogo **Permisos de repldata**, seleccione **Agregar...**. En el cuadro de texto **Seleccionar usuarios, equipos, cuentas de servicio o grupos**, escriba el nombre de la cuenta del Agente de instantáneas creado anteriormente, como <*Nombre_De_Equipo_Publicador>***\repl_snapshot**. Seleccione **Comprobar nombres**y, después, seleccione **Aceptar**:  

    ![Agregar permisos de seguridad](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12.  Repita el paso anterior para agregar permisos para el Agente de distribución, por ejemplo <*Nombre_De_Equipo_Publicador>***\repl_distribution** y, para el Agente de mezcla, <* Nombre_De_Equipo_Publicador>***\repl_merge**.  
    
  
13. Compruebe que se admiten los siguientes permisos:  
  
    - repl_distribution - Lectura
    - repl_merge - Lectura
    - repl_snapshot - Control total   
 
    ![Permisos de usuario de datos de replicación](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. Vuelva a seleccionar la pestaña **Compartir** y anote la **Ruta de acceso a la red** para el recurso compartido. Necesitará esta ruta de acceso más adelante cuando configure la **Carpeta de instantáneas**:  

    ![Ruta de acceso a la red](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades de repldata**. 
 
**Vea también**:  
[Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  

## <a name="configure-distribution"></a>Configurar la distribución
En esta sección configurará la distribución en el publicador y establecerá los permisos requeridos en las bases de datos de publicación y distribución. Si ya ha configurado el distribuidor, debe deshabilitar la publicación y distribución antes de iniciar esta sección. No lo haga si debe mantener una topología de replicación existente, especialmente en Producción.   
  
En este tutorial no se contempla la configuración de un publicador con un distribuidor remoto.  

### <a name="configure-distribution-at-the-publisher"></a>Configurar la distribución en el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Haga clic con el botón derecho en la carpeta **Replicación** y luego seleccione **Configurar distribución**:  

    ![Configurar la distribución](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
    > [!NOTE]  
    > Si se ha conectado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando **localhost** en lugar del nombre real del servidor, aparecerá una advertencia indicando que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar con el servidor **'localhost'**. En el cuadro de diálogo de advertencia, seleccione **Aceptar**. En el cuadro de diálogo **Conectar al servidor** , cambie el **Nombre del servidor** de **localhost** al nombre del servidor. Seleccione **Conectar**.  
  
    Se iniciará el Asistente para configurar la distribución.  
  
3.  En la página **Distribuidor**, seleccione **"NombreServidor" actuará como su propio distribuidor; SQL Server creará una base de datos y un registro de distribución** y luego seleccione **Siguiente**:  

    ![El servidor actúa como su propio distribuidor](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4.  Si el agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Inicio del Agente**, seleccione **Sí**, configurar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del Agente para que se inicie automáticamente. Seleccione **Siguiente**.  

     
5.  Escriba la ruta de acceso \\\\<*Nombre_De_Equipo_Publicador>***\repldata** en el cuadro de texto **Carpeta de instantáneas** y, después, seleccione **Siguiente**. Esta ruta de acceso debe coincidir con lo que vimos anteriormente en **Ruta de acceso a la red** de la carpeta de propiedades de repldata después de configurar las propiedades del recurso compartido: 

    ![Carpeta de instantáneas de datos de replicación](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6.  Acepte los valores predeterminados en las páginas restantes del asistente:  
    
    ![Valores predeterminados del Asistente para la distribución](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7.  Seleccione **Finalizar** para habilitar la distribución. 

    Este error puede aparecer al configurar el distribuidor. Es una indicación de que la cuenta utilizada para iniciar la cuenta del Agente SQL Server no es un administrador del sistema. Necesitará iniciar manualmente el Agente SQL Server, conceder dichos permisos a la cuenta existente o modificar la cuenta que utiliza el Agente SQL Server: 

     ![Error iniciando el agente](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

    Si su SQL Server Management Studio se ejecuta con derechos administrativos, puede iniciar el agente de SQL manualmente desde dentro de SSMS:  
        ![Iniciar el Agente desde SSMS](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

    >[!NOTE]
    > Si no se inicia el Agente SQL de forma visible, haga clic en el Agente SQL Server en SSMS y en **Actualizar**.  Si está todavía en estado detenido, deberá iniciarlo manualmente desde el **Administrador de configuración de SQL Server**.    
  
### <a name="setting-database-permissions-at-the-publisher"></a>Establecer permisos de base de datos en el publicador  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y, después, seleccione **Nuevo inicio de sesión**:  

    ![Nuevo inicio de sesión](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2.  En la página **General**, seleccione **Buscar**, escriba <*Nombre_De_Equipo_Publicador>***\repl_snapshot** en el cuadro **Escriba el nombre de objeto a seleccionar**, seleccione **Comprobar nombres** y, después, seleccione **Aceptar**:  

    ![Agregar el inicio de sesión de instantáneas de replicación](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3.  En la página **Asignación de usuarios** , en la lista **Usuarios asignados a este inicio de sesión** , seleccione las bases de datos de **distribución** y de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    En la lista Pertenencia al rol de la base de datos, seleccione el rol **db_owner** para el inicio de sesión en ambas bases de datos:  

    ![Propietario de la base de datos de instantáneas de replicación](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4.  Seleccione **Aceptar** para crear el inicio de sesión.  
  
5.  Repita los pasos del 1 al 4 para crear un inicio de sesión para el resto de cuentas locales (repl_distribution, repl_logreader y repl_merge). Estos inicios de sesión también se deben asignar a usuarios que son miembros del rol fijo de base de datos **db_owner** en las bases de datos **distribution** y **AdventureWorks**:  

    ![Usuarios de replicación en SSMS](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
**Vea también**:  
[Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
[Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>Pasos siguientes
Ya ha preparado correctamente el servidor para la replicación. El artículo siguiente le enseñará a configurar la replicación transaccional. 

Vaya al siguiente artículo para obtener más información
> [!div class="nextstepaction"]
> [Pasos siguientes](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  

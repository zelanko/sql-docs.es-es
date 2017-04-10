---
title: "Lecci&#243;n 3: Configurar la distribuci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicación [SQL Server], tutoriales"
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Lecci&#243;n 3: Configurar la distribuci&#243;n
En esta lección configurará la distribución en el publicador y establecerá los permisos requeridos en las bases de datos de publicación y distribución. Si ya ha configurado el distribuidor, debe deshabilitar la publicación y distribución antes de iniciar esta lección. No lo haga si debe mantener una topología de replicación existente.  
  
En este tutorial no se contempla la configuración de un publicador con un distribuidor remoto.  
  
### Configurar la distribución en el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Haga clic con el botón derecho en la carpeta **Replicación** y luego haga clic en **Configurar distribución**.  
  
    > [!NOTE]  
    > Si se ha conectado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando **localhost** en lugar del nombre real del servidor, aparecerá una advertencia indicando que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar con el servidor **'localhost'**. En el cuadro de diálogo de advertencia, haga clic en **Aceptar** . En el cuadro de diálogo **Conectar al servidor** , cambie el **Nombre del servidor** de **localhost** al nombre del servidor. Haga clic en **Conectar**.  
  
    Se iniciará el Asistente para configurar la distribución.  
  
3.  En la página **Distribuidor**, seleccione 'NombreServidor' actuará como su propio distribuidor; SQL Server creará una base de datos y un registro de distribución** y luego haga clic en **Siguiente**.  
  
4.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Inicio del Agente** , seleccione **Sí**, configurar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del Agente para que se inicie automáticamente. Haga clic en **Siguiente**.  
  
5.  Escriba **\\\\**\<*nombre_equipo>***\repldata** en el cuadro de texto **Carpeta de instantáneas**, donde \<*nombre_equipo>* es el nombre del publicador y luego haga clic en **Siguiente**.  
  
6.  Acepte los valores predeterminados en las páginas restantes del asistente.  
  
7.  Haga clic en **Finalizar** para habilitar la distribución.  
  
### Establecer permisos de base de datos en el publicador  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión** y, después, seleccione **Nuevo inicio de sesión**.  
  
2.  En la página **General**, haga clic en **Buscar**, escriba \<*nombre_equipo>***\repl_snapshot** en el cuadro **Escriba el nombre del objeto que desea seleccionar**, donde \<*nombre_equipo>* es el nombre del servidor local del publicador, haga clic en **Comprobar nombres** y, después, haga clic en **Aceptar**.  
  
3.  En la página **Asignación de usuarios** , en la lista **Usuarios asignados a este inicio de sesión** , seleccione las bases de datos de **distribución** y de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    En la lista **Pertenencia al rol de la base de datos**, seleccione el rol **db_owner** para el inicio de sesión en ambas bases de datos.  
  
4.  Haga clic en **Aceptar** para crear el inicio de sesión.  
  
5.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_logreader. El inicio de sesión también se debe asignar a usuarios que son miembros del rol fijo de base de datos **db_owner** en las bases de datos **distribution** y **AdventureWorks**.  
  
6.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_distribution. El inicio de sesión se debe asignar a los usuarios que son miembros del rol fijo de base de datos **db_owner** en la base de datos **distribution**.  
  
7.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_merge. Este inicio de sesión debe contar con asignaciones de usuario en las bases de datos **distribution** y **AdventureWorks** .  
  
## Vea también  
[Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
[Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)  
  
  
  

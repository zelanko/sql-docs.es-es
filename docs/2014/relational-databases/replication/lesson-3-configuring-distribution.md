---
title: 'Lección 3: Configuración de la distribución | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7fbfb6d659aa8bc96ebc13ad0a3b89df750c5f95
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167475"
---
# <a name="lesson-3-configuring-distribution"></a>Lección 3: Configurar la distribución
  En esta lección configurará la distribución en el publicador y establecerá los permisos requeridos en las bases de datos de publicación y distribución. Si ya ha configurado el distribuidor, debe deshabilitar la publicación y distribución antes de iniciar esta lección. No lo haga si debe mantener una topología de replicación existente.  
  
 En este tutorial no se contempla la configuración de un publicador con un distribuidor remoto.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configurar la distribución en el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Haga clic con el botón derecho en la carpeta **Replicación** y luego haga clic en **Configurar distribución**.  
  
    > [!NOTE]  
    >  Si se ha conectado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando **localhost** en lugar del nombre real del servidor, aparecerá una advertencia indicando que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar con el servidor **'localhost'**. En el cuadro de diálogo de advertencia, haga clic en **Aceptar** . En el cuadro de diálogo **Conectar al servidor** , cambie el **Nombre del servidor** de **localhost** al nombre del servidor. Haga clic en **Conectar**.  
  
     Se iniciará el Asistente para configurar la distribución.  
  
3.  En el **distribuidor** página, seleccione **'***\<ServerName >***' actuará como su propio distribuidor; SQL Server creará una base de datos de distribución y un registro**y, a continuación, haga clic en **siguiente**.  
  
4.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Inicio del Agente** , seleccione **Sí**, configurar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del Agente para que se inicie automáticamente. Haga clic en **Siguiente**.  
  
5.  Introduzca **\\\\**\<*Nombre_De_Equipo>***\repldata** en el cuadro de texto **Carpeta de instantáneas**, donde \<*Nombre_De_Equipo>* es el nombre del publicador y luego haga clic en **Siguiente**.  
  
6.  Acepte los valores predeterminados en las páginas restantes del asistente.  
  
7.  Haga clic en **Finalizar** para habilitar la distribución.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Establecer permisos de base de datos en el publicador  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y, después, seleccione **Nuevo inicio de sesión**.  
  
2.  En la página **General**, haga clic en **Buscar**, escriba \<*Nombre_De_Equipo>***\repl_snapshot* en el cuadro **Escriba el nombre del objeto que desea seleccionar**, donde \<*Nombre_De_Equipo>* es el nombre del servidor local del publicador, haga clic en **Comprobar nombres** y, después, haga clic en **Aceptar**.  
  
3.  En la página **Asignación de usuarios** , en la lista **Usuarios asignados a este inicio de sesión** , seleccione las bases de datos de **distribución** y de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
     En el **pertenencia al rol de base de datos** lista select el `db_owner` rol para el inicio de sesión para ambas bases de datos.  
  
4.  Haga clic en **Aceptar** para crear el inicio de sesión.  
  
5.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_logreader. También se debe asignar este inicio de sesión a los usuarios que son miembros de la `db_owner` rol fijo de base de datos en el **distribución** y **AdventureWorks** bases de datos.  
  
6.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_distribution. Este inicio de sesión debe asignarse a un usuario que sea miembro de la `db_owner` rol fijo de base de datos en el **distribución** base de datos.  
  
7.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_merge. Este inicio de sesión debe contar con asignaciones de usuario en las bases de datos **distribution** y **AdventureWorks** .  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Replication Agent Security Model](security/replication-agent-security-model.md)  
  
  

---
title: 'Lección 3: Configuración de la distribución | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: rothja
ms.author: jroth
ms.openlocfilehash: 28df67dad52bcd11a18fc5deb42a6725700dde5a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065951"
---
# <a name="lesson-3-configuring-distribution"></a>Lección 3: Configurar la distribución
  En esta lección configurará la distribución en el publicador y establecerá los permisos requeridos en las bases de datos de publicación y distribución. Si ya ha configurado el distribuidor, debe deshabilitar la publicación y distribución antes de iniciar esta lección. No lo haga si debe mantener una topología de replicación existente.  
  
 En este tutorial no se contempla la configuración de un publicador con un distribuidor remoto.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configurar la distribución en el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Haga clic con el botón derecho en la carpeta **Replicación** y luego haga clic en **Configurar distribución**.  
  
    > [!NOTE]  
    >  Si se ha conectado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando **localhost** en lugar del nombre real del servidor, aparecerá una advertencia indicando que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar con el servidor **'localhost'**. Haga clic en **Aceptar** en el cuadro de diálogo de advertencia. En el cuadro de diálogo **Conectar al servidor** , cambie el **Nombre del servidor** de **localhost** al nombre del servidor. Haga clic en **Conectar**.  
  
     Se iniciará el Asistente para configurar la distribución.  
  
3.  En la página **distribuidor** , seleccione **'** _\<ServerName>_ **' actuará como su propio distribuidor; SQL Server creará una base de datos y un registro de distribución**y, a continuación, haga clic en **siguiente**.  
  
4.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Inicio del Agente** , seleccione **Sí**, configurar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del Agente para que se inicie automáticamente. Haga clic en **Siguiente**.  
  
5.  Escriba **\\\\** \<_Machine_Name> _**\repldata** en el cuadro de texto **carpeta de instantáneas** , donde \<*Machine_Name> * es el nombre del publicador y, a continuación, haga clic en **siguiente**.  
  
6.  Acepte los valores predeterminados en las páginas restantes del asistente.  
  
7.  Haga clic en **Finalizar** para habilitar la distribución.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Establecer permisos de base de datos en el publicador  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , expanda **seguridad**, haga clic con el botón secundario en **inicios de sesión**y seleccione **nuevo inicio de sesión**.  
  
2.  En la página **General** , haga clic en **Buscar**, escriba \<_Machine_Name> _**\ repl_snapshot** en el cuadro **Escriba el nombre del objeto que desea seleccionar** , donde \<*Machine_Name> * es el nombre del servidor del publicador local, haga clic en **Comprobar nombres**y, a continuación, haga clic en **Aceptar**.  
  
3.  En la página **asignación de usuarios** , en la lista **usuarios asignados a este inicio de sesión** , seleccione las bases de datos de **distribución** y de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
     En la lista **pertenencia al rol** de la base de datos, seleccione el `db_owner` rol para el inicio de sesión de las dos bases de datos.  
  
4.  Haga clic en **Aceptar** para crear el inicio de sesión.  
  
5.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_logreader. Este inicio de sesión también se debe asignar a usuarios que son miembros del `db_owner` rol fijo de base de datos en las bases de datos de **distribución** y **AdventureWorks** .  
  
6.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_distribution. Este inicio de sesión debe estar asignado a un usuario que sea miembro del `db_owner` rol fijo de base de datos en la base de datos de **distribución** .  
  
7.  Repita los pasos 1 a 4 para crear un inicio de sesión para la cuenta local de repl_merge. Este inicio de sesión debe contar con asignaciones de usuario en las bases de datos **distribution** y **AdventureWorks** .  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la distribución](configure-distribution.md)   
 [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md)  
  
  

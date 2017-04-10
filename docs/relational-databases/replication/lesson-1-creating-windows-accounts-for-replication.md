---
title: "Lecci&#243;n 1: Crear cuentas de Windows para replicaci&#243;n | Microsoft Docs"
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
  - "replicación [SQL Server], administrar"
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Lecci&#243;n 1: Crear cuentas de Windows para replicaci&#243;n
En esta lección creará cuentas de Windows para ejecutar agentes de replicación. Creará distintas cuentas de Windows en el servidor local para los siguientes agentes:  
  
|Agente|Ubicación|Nombre de cuenta|  
|---------|------------|----------------|  
|Agente de instantáneas|publicador|\<*nombre_equipo*> \repl_snapshot|  
|Agente de registro del LOG|publicador|\<*nombre_equipo*> \repl_logreader|  
|Agente de distribución|Publicador y suscriptor|\<*nombre_equipo*> \repl_distribution|  
|Agente de mezcla|Publicador y suscriptor|\<*nombre_equipo*> \repl_merge|  
  
> [!NOTE]  
> En los tutoriales de replicación, el publicador y el distribuidor comparten la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El publicador y el suscriptor pueden compartir la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque no es necesario. Si el publicador y el suscriptor comparten la misma instancia, no se requieren los pasos que se utilizan para crear las cuentas en el suscriptor.  
  
### Para crear cuentas locales de Windows para agentes de replicación en el publicador  
  
1.  En el publicador, vaya al Panel de control y abra **Administración de equipos** en **Herramientas administrativas**.  
  
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**.  
  
3.  Haga clic con el botón derecho en **Usuarios** y después haga clic en **Usuario nuevo**.  
  
4.  Escriba **repl_snapshot** en el cuadro **Nombre de usuario**, proporcione la contraseña y demás información relevante y, después, haga clic en **Crear** para crear la cuenta repl_snapshot.  
  
5.  Repita el paso anterior para crear las cuentas repl_logreader, repl_distribution y repl_merge.  
  
6.  Haga clic en **Cerrar**.  
  
### Para crear cuentas locales de Windows para agentes de replicación en el suscriptor  
  
1.  En el suscriptor, vaya al Panel de control y abra **Administración de equipos** en **Herramientas administrativas**.  
  
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**.  
  
3.  Haga clic con el botón derecho en **Usuarios** y después haga clic en **Usuario nuevo**.  
  
4.  Escriba **repl_distribution** en el cuadro **Nombre de usuario**, proporcione la contraseña y demás información relevante y, después, haga clic en **Crear** para crear la cuenta repl_distribution.  
  
5.  Repita el paso anterior para crear la cuenta repl_merge.  
  
6.  Haga clic en **Cerrar**.  
  
## Pasos siguientes  
Ha creado correctamente cuentas de Windows para agentes de replicación. A continuación, configurará la carpeta de instantáneas. Consulte [Lección 2: Preparar la carpeta de instantáneas](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md).  
  
## Vea también  
[Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
  

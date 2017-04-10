---
title: "Ver el registro de aplicaci&#243;n Windows (Windows) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ver registros"
  - "registros de aplicación [SQL Server]"
  - "registros [SQL Server], aplicación"
  - "supervisar el registro de aplicación Windows NT [SQL Server]"
  - "registros de aplicación Windows NT [SQL Server]"
  - "mostrar registros"
  - "supervisar [SQL Server], eventos"
  - "registros [SQL Server], ver"
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Ver el registro de aplicaci&#243;n Windows (Windows)
  Si se configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para utilizar el registro de aplicación de Windows, todas las sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribirán los nuevos eventos en el registro. A diferencia del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se crea un nuevo registro de aplicación cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### Para ver el registro de aplicación Windows  
  
1.  En el menú **Inicio** , seleccione **Todos los programas**, **Herramientas administrativas**y, a continuación, haga clic en **Visor de eventos**.  
  
2.  En el Visor de eventos, haga clic en **Aplicación**.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Los eventos se identifican con la entrada **MSSQLSERVER** (las instancias con nombre se identifican con **MSSQL$***<nombre_de_instancia>*) en la columna **Origen**. Los eventos del Agente SQL Server se identifican con la entrada SQLSERVERAGENT (para las instancias con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se identifican con **SQLAgent$**\<*nombre_de_instancia*>). Los eventos del servicio Microsoft Search se identifican con la entrada **Microsoft Search**.  
  
4.  Para ver el registro de otro equipo, haga clic con el botón derecho en **Visor de eventos**, haga clic en **Conectar con otro equipo** y complete el cuadro de diálogo **Seleccionar equipo**.  
  
5.  Opcionalmente, para que solo se muestren los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el menú **Ver** , haga clic en **Filtro**y, en la lista **Origen del evento** , seleccione **MSSQLSERVER**. Para ver solo los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **SQLSERVERAGENT** en la lista **Origen del evento** .  
  
6.  Para ver más información acerca de un evento, haga doble clic en el suceso.  
  
## Vea también  
 [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
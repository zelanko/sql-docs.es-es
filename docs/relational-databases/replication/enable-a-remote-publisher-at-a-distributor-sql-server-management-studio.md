---
title: "Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "distribuidores remotos [replicación de SQL Server]"
  - "publicadores [replicación de SQL Server]"
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio)
  Habilite un publicador para utilizar un distribuidor remoto en la página **Publicadores** . Esta página está disponible en el Asistente para configurar la distribución y el **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [Configurar publicación y distribución](../../relational-databases/replication/configure-publishing-and-distribution.md) y [Propiedades de publicador y distribuidor modificar y vista](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Para habilitar un publicador en el Asistente para configurar la distribución  
  
1.  En la página **Publicadores** del Asistente para configurar la distribución, haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En el **contraseña del distribuidor** página, en el **contraseña** y **Confirmar contraseña** cuadros de texto, especifique una contraseña segura para la **distributor_admin** cuenta de que la replicación se utiliza para conectarse desde el publicador al distribuidor para realizar tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para habilitar un publicador en el cuadro de diálogo Propiedades del distribuidor  
  
1.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo, haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En el **publicadores** página, en el **contraseña** y **Confirmar contraseña** cuadros de texto, especifique una contraseña segura para la **distributor_admin** cuenta de que la replicación se utiliza para conectarse desde el publicador al distribuidor para realizar tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)   
 [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
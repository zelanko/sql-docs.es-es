---
title: "Tarea Copia de seguridad de la base de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.backupdatabasetask.f1"
helpviewer_keywords: 
  - "base de datos, copia de seguridad [Integration Services]"
  - "Copia de seguridad de la base de datos, tarea [Integration Services]"
  - "copia de seguridad de las bases de datos [Integration Services]"
  - "registro de transacciones, copia de seguridad [Integration Services]"
  - "copia de seguridad de los registros de transacciones [Integration Services]"
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Tarea Copia de seguridad de la base de datos
  La tarea Copia de seguridad de la base de datos realiza distintos tipos de copias de seguridad de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Un paquete puede utilizar la tarea Copia de seguridad de la base de datos para realizar una copia de seguridad de una o varias bases de datos. Si la tarea solo realiza una copia de seguridad de una única base de datos, puede elegir el componente de copia de seguridad: la base de datos o sus archivos y grupos de archivos.  
  
## Tipos de copia de seguridad y modelos de recuperación admitidos  
 En la tabla siguiente se muestran los modelos de recuperación y los tipos de copia de seguridad compatibles con la tarea Copia de seguridad de la base de datos.  
  
|Modelo de recuperación|Base de datos|Diferencial de base de datos|Registro de transacciones|Archivos o diferencial de archivos|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Necesario|Opcional|No compatible|No compatible|  
|Completa|Necesario|Opcional|Necesario|Opcional|  
|Registro masivo|Necesario|Opcional|Necesario|Opcional|  
  
 La tarea Copia de seguridad de la base de datos encapsula una instrucción BACKUP de Transact-SQL. Para obtener más información, vea [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
## Configuración de la tarea Copia de seguridad de la base de datos  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Copia de seguridad de base de datos &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/back-up-database-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  
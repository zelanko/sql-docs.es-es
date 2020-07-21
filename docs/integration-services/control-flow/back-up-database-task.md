---
title: Tarea Copia de seguridad de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e45060a494fad2fbd0310a31bdf433e624becdc2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294302"
---
# <a name="back-up-database-task"></a>Tarea Copia de seguridad de la base de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Copia de seguridad de la base de datos realiza distintos tipos de copias de seguridad de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Un paquete puede utilizar la tarea Copia de seguridad de la base de datos para realizar una copia de seguridad de una o varias bases de datos. Si la tarea solo realiza una copia de seguridad de una única base de datos, puede elegir el componente de copia de seguridad: la base de datos o sus archivos y grupos de archivos.  
  
## <a name="supported-recover-models-and-backup-types"></a>Tipos de copia de seguridad y modelos de recuperación admitidos  
 En la tabla siguiente se muestran los modelos de recuperación y los tipos de copia de seguridad compatibles con la tarea Copia de seguridad de la base de datos.  
  
|modelo de recuperación|Base de datos|Diferencial de base de datos|Registro de transacciones|Archivos o diferencial de archivos|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Obligatorio|Opcional|No compatible|No compatible|  
|Completo|Obligatorio|Opcional|Obligatorio|Opcional|  
|Registro masivo|Obligatorio|Opcional|Obligatorio|Opcional|  
  
 La tarea Copia de seguridad de la base de datos encapsula una instrucción BACKUP de Transact-SQL. Para obtener más información, vea [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Configuración de la tarea Copia de seguridad de la base de datos  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Copia de seguridad de base de datos &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

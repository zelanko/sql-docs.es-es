---
title: Bases de datos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05f9976284e6207a1057f1b7308e7276d833daae
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="databases"></a>Bases de datos
  Una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consta de una colección de tablas en las que se almacena un conjunto específico de datos estructurados. Una tabla contiene una colección de filas, también denominadas tuplas o registros, y columnas, también denominadas atributos. Cada columna de la tabla se ha diseñado para almacenar un determinado tipo de información; por ejemplo, fechas, nombres, importes en moneda o números.  
  
## <a name="basic-information-about-databases"></a>Información básica sobre las bases de datos  
 Un equipo puede tener una o varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas. Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede contener una o varias bases de datos.  En una base de datos, hay uno o varios grupos de propiedad de objetos denominados esquemas. Dentro de cada esquema hay objetos de base de datos como tablas, vistas y procedimientos almacenados. Algunos objetos, como certificados y claves asimétricas, se encuentran en la base de datos, pero no dentro de un esquema. Para obtener más información acerca de cómo crear tablas, vea [Tables](../../relational-databases/tables/tables.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se almacenan en archivos del sistema de archivos. Los archivos se pueden agrupar en grupos de archivos. Para obtener más información acerca de los grupos de archivos, vea [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Cuando los usuarios obtienen acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se identifican como un inicio de sesión. Cuando los usuarios obtienen acceso a una base de datos, se identifican como un usuario de base de datos. Un usuario de base de datos puede estar basado en un inicio de sesión. Si están habilitadas las bases de datos independientes, se puede crear un usuario de base de datos que no esté basado en un inicio de sesión. Para obtener más información sobre usuarios, vea [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
 A un usuario que tiene acceso a una base de datos se le puede conceder permiso para acceder a los objetos de la base de datos. Aunque los permisos se pueden conceder a usuarios individuales, se recomienda crear roles de base de datos, agregar usuarios de base de datos a los roles y, a continuación, conceder permiso de acceso a los roles. La concesión de permisos a roles en vez de a usuarios facilita la coherencia y la comprensión de los permisos a medida que el número de usuarios aumenta y cambia continuamente. Para obtener más información sobre permisos de roles, vea [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) y [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Trabajar con bases de datos  
 La mayoría de los usuarios que trabajan con bases de datos usan la herramienta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . La herramienta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] tiene una interfaz de usuario gráfica para crear bases de datos y los objetos de las bases de datos. [!INCLUDE[tsql](../../includes/tsql-md.md)] también dispone de un editor de consultas para interactuar con bases de datos mediante la escritura de instrucciones [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] se puede instalar desde el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o se puede descargar de MSDN.  
  
## <a name="in-this-section"></a>En esta sección  
  
|||  
|-|-|  
|[Bases de datos del sistema](../../relational-databases/databases/system-databases.md)|[Eliminar archivos de datos o de registro de una base de datos](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[Bases de datos independientes](../../relational-databases/databases/contained-databases.md)|[Mostrar la información del espacio ocupado por los datos y el registro de una base de datos](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[Archivos de datos de SQL Server en Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[Aumentar el tamaño de una base de datos](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md)|[Cambiar el nombre de una base de datos](../../relational-databases/databases/rename-a-database.md)|  
|[Estados de base de datos](../../relational-databases/databases/database-states.md)|[Establecer una base de datos en modo de usuario único](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[Estados de los archivos](../../relational-databases/databases/file-states.md)|[Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)|  
|[Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[Reducir un archivo](../../relational-databases/databases/shrink-a-file.md)|  
|[Copiar bases de datos en otros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)|[Ver o cambiar las propiedades de una base de datos](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[Ver una lista de bases de datos en una instancia de SQL Server](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Agregar archivos de datos o de registro a una base de datos](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[Cambiar los valores de configuración de una base de datos](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[Usar el Asistente para planes de mantenimiento](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Crear una base de datos](../../relational-databases/databases/create-a-database.md)|[Crear un alias de tipo de datos definido por el usuario](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[Eliminar una base de datos](../../relational-databases/databases/delete-a-database.md)|[Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Índices](../../relational-databases/indexes/indexes.md)  
  
 [Vistas](../../relational-databases/views/views.md)  
  
 [Procedimientos almacenados &#40;Database Engine&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  

---
title: Base de datos modelo | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
caps.latest.revision: 47
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3f8fd67f968701440b06274bbd40600be94c00b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111799"
---
# <a name="model-database"></a>Base de datos model
  La base de datos **modelo** se utiliza como plantilla para todas las bases de datos creadas en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como **tempdb** se crea de nuevo cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la base de datos **modelo** siempre tiene que existir en un sistema con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Todo el contenido de la base de datos **modelo** , incluidas las opciones de base de datos, se copia en la base de datos nueva. Algunos de los valores de configuración de la base de datos **model** también se usan para crear una base de datos **tempdb** nueva durante el inicio, de modo que la base de datos **model** siempre debe existir en un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Las bases de datos de usuario recién creadas usan el mismo [modelo de recuperación](../backup-restore/recovery-models-sql-server.md) que la en. La opción predeterminada la puede configurar el usuario. Para obtener más información sobre el modelo de recuperación actual del modelo, consulte [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Si modifica la base de datos **model** con información de la plantilla específica del usuario, se recomienda realizar una copia de seguridad de **model**. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="model-usage"></a>Uso de modelo  
 Cuando se emite una instrucción CREATE DATABASE, la primera parte de la base de datos se crea mediante la copia del contenido de la base de datos **modelo** . El resto de la nueva base de datos se llena a continuación con páginas vacías.  
  
 Si modifica la base de datos **model** , todas las bases de datos creadas posteriormente heredan los cambios. Por ejemplo, se podrían establecer permisos u opciones de base de datos o agregar objetos, como tablas, funciones o procedimientos almacenados. Las propiedades del archivo de la base de datos del **modelo** son una excepción y se ignoran, excepto el tamaño inicial del archivo de datos.  
  
## <a name="physical-properties-of-model"></a>Propiedades físicas de model  
 Las siguientes tablas muestran los valores de configuración iniciales de los archivos de datos y registro de **model** . El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Crecimiento del archivo|  
|----------|------------------|-------------------|-----------------|  
|Datos principales|modeldev|model.mdf|Crecimiento automático del 10 por ciento hasta llenar el disco.|  
|Log|modellog|modellog.ldf|Crecimiento automático del 10 por ciento hasta un máximo de 2 terabytes.|  
  
 Para mover la base de datos **model** o los archivos de registro, consulte [Mover bases de datos del sistema](system-databases.md).  
  
### <a name="database-options"></a>Opciones de base de datos  
 La siguiente tabla muestra el valor predeterminado de cada opción de la base de datos **modelo** e indica si la opción puede modificarse. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sí|  
|ANSI_NULL_DEFAULT|OFF|Sí|  
|ANSI_NULLS|OFF|Sí|  
|ANSI_PADDING|OFF|Sí|  
|ANSI_WARNINGS|OFF|Sí|  
|ARITHABORT|OFF|Sí|  
|AUTO_CLOSE|OFF|Sí|  
|AUTO_CREATE_STATISTICS|ON|Sí|  
|AUTO_SHRINK|OFF|Sí|  
|AUTO_UPDATE_STATISTICS|ON|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sí|  
|CHANGE_TRACKING|OFF|no|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sí|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|no<br /><br /> Sí<br /><br /> Sí|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sí|  
|DB_CHAINING|OFF|no|  
|ENCRYPTION|OFF|no|  
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|Sí|  
|RECOVERY|Depende de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edición<sup>1</sup>|Sí|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|DISABLE_BROKER|no|  
|TRUSTWORTHY|OFF|no|  
  
 <sup>1</sup> para comprobar que el modelo de recuperación actual de la base de datos, consulte [ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41; ](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) o [sys.databases &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrictions  
 Las siguientes operaciones no se pueden realizar en la base de datos **modelo** :  
  
-   Agregar archivos o grupos de archivos.  
  
-   Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
  
-   Cambiar el propietario de la base de datos. **model** es propiedad de **sa**.  
  
-   Eliminar la base de datos.  
  
-   Eliminar el usuario **guest** de la base de datos.  
  
-   Habilitar el mecanismo de captura de cambios en los datos.  
  
-   Participar en el reflejo de la base de datos.  
  
-   Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
  
-   Cambiar el nombre de la base de datos o del grupo de archivos principal.  
  
-   Establecer la base de datos en OFFLINE.  
  
-   Establecer el grupo de archivos principal en READ_ONLY.  
  
-   Crear procedimientos, vistas, o desencadenadores utilizando la opción WITH ENCRYPTION. La clave de cifrado está asociada a la base de datos en la que se crea el objeto. Los objetos cifrados creados en la base de datos **modelo** solo se pueden usar en **modelo**.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Bases de datos del sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover archivos de base de datos](move-database-files.md)  
  
  

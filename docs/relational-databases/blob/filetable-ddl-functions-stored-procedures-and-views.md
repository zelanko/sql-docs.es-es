---
title: Funciones FileTable, procedimientos almacenados, vistas | Microsoft Docs
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6f429d40b3bc93a4897cf23c5f9985fbf71c9016
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75252716"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>DDL de FileTable, funciones, procedimientos almacenados y vistas

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Enumera las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y los objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se han agregado o cambiado para admitir la característica FileTable en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La columna Estado de las tablas siguientes indica si el elemento es nuevo en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o estaba en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero se ha cambiado en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para admitir la búsqueda semántica.  
  
 Para obtener la lista de instrucciones y objetos de base de datos que admiten FILESTREAM, vea [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Instrucciones del lenguaje de definición de datos (DDL) de Transact-SQL  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)|Cambiado|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Cambiado|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|Cambiado|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Cambiado|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [RESTORE &#40;argumentos, Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|Cambiado||  
  
##  <a name="func"></a> Funciones  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> Procedimientos almacenados  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> Vistas de catálogo  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**Agregado**|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**Agregado**|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|Cambiado|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> Vistas de administración dinámica  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  

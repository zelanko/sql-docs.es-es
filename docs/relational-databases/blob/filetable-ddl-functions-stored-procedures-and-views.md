---
title: "DDL de FileTable, funciones, procedimientos almacenados y vistas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FileTables [SQL Server], objetos de base de datos"
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# DDL de FileTable, funciones, procedimientos almacenados y vistas
  Enumera las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y los objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se han agregado o cambiado para admitir la característica FileTable en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La columna Estado de las tablas siguientes indica si el elemento es nuevo en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o estaba en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero se ha cambiado en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para admitir la búsqueda semántica.  
  
 Para obtener la lista de instrucciones y objetos de base de datos que admiten FILESTREAM, vea [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Instrucciones del lenguaje de definición de datos (DDL) de Transact-SQL  
  
|Object|Estado|Más información|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)|Cambiado|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Cambiado|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|Cambiado|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Cambiado|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)<br /><br /> [RESTORE &#40;argumentos, Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)|Cambiado||  
  
##  <a name="func"></a> Funciones  
  
|Object|Estado|Más información|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> Procedimientos almacenados  
  
|Object|Estado|Más información|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../Topic/sp_kill_filestream_non_transacted_handles%20\(Transact-SQL\).md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> Vistas de catálogo  
  
|Object|Estado|Más información|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**Agregado**|[Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**Agregado**|[Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|Cambiado|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> Vistas de administración dinámica  
  
|Object|Estado|Más información|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**Agregado**|[Administrar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
## Vea también  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
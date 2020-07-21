---
title: DDL de FileTable, funciones, procedimientos almacenados y vistas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3fca483581a47720cf0d923506f4439e3e614520
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955315"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>DDL de FileTable, funciones, procedimientos almacenados y vistas
  Enumera las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y los objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se han agregado o cambiado para admitir la característica FileTable en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La columna Estado de las tablas siguientes indica si el elemento es nuevo en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o estaba en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero se ha cambiado en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para admitir la búsqueda semántica.  
  
 Para obtener la lista de instrucciones y objetos de base de datos que admiten FILESTREAM, vea [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md).  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Instrucciones del lenguaje de definición de datos (DDL) de Transact-SQL  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|Cambiado|[Habilitar los requisitos previos de FileTables](enable-the-prerequisites-for-filetable.md)<br /><br /> [Administrar FileTables](manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|Cambiado|[Crear, modificar y quitar FileTables](create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](manage-filetables.md)|  
|[CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|Cambiado|[Habilitar los requisitos previos de FileTables](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|Cambiado|[Crear, modificar y quitar FileTables](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [RESTORE &#40;argumentos, Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|Cambiado||  
  
##  <a name="functions"></a><a name="func"></a> Funciones  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**Agregado**|[Trabajar con directorios y rutas de acceso de FileTables](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> Procedimientos almacenados  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**Agregado**|[Administrar FileTables](manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> Vistas de catálogo  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**Agregado**|[Habilitar los requisitos previos de FileTables](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**Agregado**|[Crear, modificar y quitar FileTables](create-alter-and-drop-filetables.md)<br /><br /> [Administrar FileTables](manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**Agregado**|[Administrar FileTables](manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Cambiado|[Administrar FileTables](manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> Vistas de administración dinámica  
  
|Object|Status|Más información|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**Agregado**|[Administrar FileTables](manage-filetables.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Administrar FileTables](manage-filetables.md)  
  
  

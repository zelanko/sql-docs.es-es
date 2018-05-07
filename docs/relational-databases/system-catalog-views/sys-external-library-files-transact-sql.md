---
title: Sys.external_library_files (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: febfe235bd7f4711e8192ab7625491b72ac050ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysexternallibraryfiles-transact-sql"></a>Sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Muestra una fila por cada archivo que constituye una biblioteca externa.

|Nombre de columna |Tipo de datos |Description|
|------|------|-----|
|external_library_id | int |Identificador del objeto de biblioteca externa. |
|content |varbinary(max) |Contenido del artefacto de archivo de biblioteca externa. |
|Plataforma |tinyint |Id. de la plataforma de host en el que está instalado SQL Server. |
|platform_desc | nvarchar(60) |Nombre de la plataforma de host. Los valores válidos son 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>Vea también  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Administración de paquetes de servicio de aprendizaje de máquina de SQL Server](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

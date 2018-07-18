---
title: Sys.external_library_files (Transact-SQL) | Microsoft Docs
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001177"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>Sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Muestra una fila por cada archivo que constituye una biblioteca externa.

|Nombre de columna |Tipo de datos |Descripción|
|------|------|-----|
|external_library_id | INT |Identificador del objeto de biblioteca externa. |
|content |varbinary(max) |Contenido del artefacto de archivo de biblioteca externa. |
|Plataforma |TINYINT |Id. de la plataforma de host donde está instalado SQL Server. |
|platform_desc | nvarchar(60) |Nombre de la plataforma de host. Los valores válidos son 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>Vea también  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREAR UNA BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Administración de paquetes para el servicio de SQL Server Machine Learning](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

---
title: Sys. external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 69c1b1c0f1ec2c7ab1c6cd17fbf949f0aaf166f2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754482"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Muestra una fila para cada archivo que constituye una biblioteca externa.

|Nombre de la columna |Tipo de datos |Descripción|
|------|------|-----|
|external_library_id | int |IDENTIFICADOR del objeto de biblioteca externa. |
|contenido |varbinary(max) |Contenido del artefacto de archivo de biblioteca externa. |
|platform |TINYINT |IDENTIFICADOR de la plataforma de host en la que está instalado SQL Server. |
|platform_desc | nvarchar(60) |Nombre de la plataforma de host. Los valores válidos son ' WINDOWS ', ' LINUX '. |

### <a name="see-also"></a>Vea también  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  

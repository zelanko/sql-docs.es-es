---
title: Sys. external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7af0a7fcb639ae3beab6216e77f9b7b95a398da
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471097"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>Sys. external_library_files (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Muestra una fila para cada archivo que constituye una biblioteca externa.

|Nombre de columna |Tipo de datos |Descripción|
|------|------|-----|
|external_library_id | int |IDENTIFICADOR del objeto de biblioteca externa. |
|contenido |varbinary(max) |Contenido del artefacto de archivo de biblioteca externa. |
|plataforma |tinyint |IDENTIFICADOR de la plataforma de host en la que está instalado SQL Server. |
|platform_desc | nvarchar(60) |Nombre de la plataforma de host. Los valores válidos son ' WINDOWS ', ' LINUX '. |

### <a name="see-also"></a>Vea también  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Administración de paquetes para SQL Server servicio Machine Learning](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

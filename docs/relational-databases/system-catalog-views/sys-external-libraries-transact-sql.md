---
title: Sys. external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac6ad0872e813d36d9884a00f979b2a5284cd4a3
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536160"
---
# <a name="sysexternal_libraries-transact-sql"></a>Sys. external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Admite la administración de bibliotecas de paquetes relacionadas con los tiempos de ejecución externos como R, Python y Java.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. R, Python y Java en las plataformas Windows y Linux se admiten en SQL Server 2019 y versiones posteriores.

## <a name="sysexternal_libraries"></a>sys.external_libraries

La vista de catálogo sys. external_libraries muestra una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |int | IDENTIFICADOR del objeto de biblioteca externa. |
|name |sysname |Nombre de la biblioteca externa. Es único en la base de datos por propietario.|
|principal_id |int |IDENTIFICADOR de la entidad de seguridad que posee esta biblioteca externa. |
|language | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son ' R ', ' Python ' y ' Java '. Los tiempos de ejecución adicionales pueden agregarse en el futuro.|
|ámbito |int |0 para el ámbito público; 1 para ámbito privado |  
|scope_desc |VARCHAR (7) |Indica si el paquete es público o privado.|

## <a name="see-also"></a>Vea también  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Instalación de paquetes de Python adicionales en SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  
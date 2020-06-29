---
title: Sys. external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 7303649ec6d7a849979871de3f4f91b978adc23a
ms.sourcegitcommit: a0ebbcb717f09d3614de5ce9eb9f3c00f0a45f81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85409374"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Admite la administración de bibliotecas de paquetes relacionadas con los tiempos de ejecución externos como R, Python y Java.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 y versiones posteriores se admiten R, Python y Java en las plataformas Windows y Linux. En Azure SQL Instancia administrada, se admiten R y Python.

## <a name="sysexternal_libraries"></a>sys.external_libraries

La vista de catálogo sys. external_libraries muestra una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de la columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |int | IDENTIFICADOR del objeto de biblioteca externa. |
|name |sysname |Nombre de la biblioteca externa. Es único en la base de datos por propietario.|
|principal_id |int |IDENTIFICADOR de la entidad de seguridad que posee esta biblioteca externa. |
|lenguaje | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son ' R ', ' Python ' y ' Java '. Los tiempos de ejecución adicionales pueden agregarse en el futuro.|
|scope |int |0 para el ámbito público; 1 para ámbito privado |  
|scope_desc |VARCHAR (7) |Indica si el paquete es público o privado.|

## <a name="see-also"></a>Consulte también  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalación de paquetes de R adicionales](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Instalación de paquetes de Python adicionales](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
ms.openlocfilehash: 78923a0eb1404c1437c6e1144888261e542ebc5a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471099"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Admite la administración de bibliotecas de paquetes relacionadas con los tiempos de ejecución externos como R, Python y Java.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 CTP 2.4 se admiten R, Python, Java y Linux en la plataforma Windows.

## <a name="sysexternallibraries"></a>sys.external_libraries

La vista de catálogo sys. external_libraries muestra una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |int | IDENTIFICADOR del objeto de biblioteca externa. |
|name |sysname |Nombre de la biblioteca externa. Es único en la base de datos por propietario.|
|principal_id |int |IDENTIFICADOR de la entidad de seguridad que posee esta biblioteca externa. |
|language | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son ' R ', ' Python ' y ' Java '. Los tiempos de ejecución adicionales pueden agregarse en el futuro.|
|scope |int |0 para el ámbito público; 1 para ámbito privado |  
|scope_desc |VARCHAR (7) |Indica si el paquete es público o privado.|

## <a name="see-also"></a>Vea también  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Instalación de paquetes de Python adicionales en SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  
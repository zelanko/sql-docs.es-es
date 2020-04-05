---
title: sys.external_libraries (Transact-SQL) Microsoft Docs
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
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664432"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Admite la administración de bibliotecas de paquetes relacionadas con tiempos de ejecución externos como R, Python y Java.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 y versiones posteriores se admiten R, Python y Java en las plataformas Windows y Linux.

## <a name="sysexternal_libraries"></a>sys.external_libraries

La vista de catálogo sys.external_libraries enumera una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de la columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |int | ID del objeto de biblioteca externa. |
|name |sysname |Nombre de la biblioteca externa. Es único dentro de la base de datos por propietario.|
|principal_id |int |ID de la entidad de seguridad propietaria de esta biblioteca externa. |
|language | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son 'R', 'Python' y 'Java'. Es posible que se agreguen tiempos de ejecución adicionales en el futuro.|
|scope |int |0 para el ámbito público; 1 para el ámbito privado |  
|scope_desc |varchar(7) |Indica si el paquete es público o privado|

## <a name="see-also"></a>Vea también  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalación de paquetes de R adicionales en SQL Server](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Instalación de paquetes de Python adicionales en SQL Server](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
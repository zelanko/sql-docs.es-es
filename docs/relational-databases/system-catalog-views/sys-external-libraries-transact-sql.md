---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
ms.openlocfilehash: d56d0c69b9e3bae87dda9b55d241a1c040210ca9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637474"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Admite la administración de bibliotecas de paquetes relacionados con tiempos de ejecución externos como R, Python y Java.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 CTP 2.4 se admiten R, Python, Java y Linux en la plataforma Windows.

## <a name="sysexternallibraries"></a>sys.external_libraries

El sys.external_libraries de vista de catálogo contiene una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |INT | Identificador del objeto de biblioteca externa. |
|NAME |sysname |Nombre de la biblioteca externa. Es único dentro de la base de datos por propietario.|
|principal_id |INT |Id. de la entidad que posee esta biblioteca externa. |
|language | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son 'R', "Python" y "Java". Los tiempos de ejecución adicionales podrían agregarse en el futuro.|
|ámbito |INT |0 para un ámbito público; 1 para el ámbito privado |  
|scope_desc |varchar(7) |Indica si el paquete es público o privado|

## <a name="see-also"></a>Vea también  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREAR UNA BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Instalación de paquetes de Python adicionales en SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  
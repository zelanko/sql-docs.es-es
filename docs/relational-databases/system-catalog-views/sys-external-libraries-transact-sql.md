---
title: Sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1373849201dccbb36f7096549d63864a23330f14
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075878"
---
# <a name="sysexternallibraries-transact-sql"></a>Sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Admite la administración de bibliotecas de paquetes relacionados con tiempos de ejecución externos como R o Python.

## <a name="sysexternallibraries"></a>sys.external_libraries

El sys.external_libraries de vista de catálogo contiene una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_library_id |INT | Identificador del objeto de biblioteca externa. |
|NAME |sysname |Nombre de la biblioteca externa. Es único dentro de la base de datos por propietario.|
|principal_id |INT |Id. de la entidad que posee esta biblioteca externa. |
|language | sysname | Nombre del lenguaje o tiempo de ejecución que admite la biblioteca externa. Los valores válidos son 'R'. Los tiempos de ejecución adicionales podrían agregarse en el futuro.|
|ámbito |INT |0 para un ámbito público; 1 para el ámbito privado |  
|scope_desc |varchar(7) |Indica si el paquete es público o privado|


## <a name="see-also"></a>Vea también  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[CREAR UNA BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Administración de paquetes de SQL Server R Services](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

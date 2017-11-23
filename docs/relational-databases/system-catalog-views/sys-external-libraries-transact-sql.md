---
title: Sys.external_libraries (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_libraries catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: bb229022bcccfb9cdc8c419844d30335337575d4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraries-transact-sql"></a>Sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Admite la administración de bibliotecas de paquete relacionados con tiempos de ejecución externos, como R o Python.

## <a name="sysexternallibraries"></a>Sys.external_libraries

El sys.external_libraries de la vista de catálogo muestra una fila para cada biblioteca externa que se ha cargado en la base de datos.

|Nombre de columna |Tipo de datos | Description|
|------|------|------|
|external_library_id |int | Identificador del objeto de biblioteca externa. |
|name |sysname |Nombre de la biblioteca externa. Es único dentro de la base de datos por propietario.|
|principal_id |int |Id. de la entidad que posee esta biblioteca externa. |
|language | sysname | Nombre del idioma o en tiempo de ejecución que admite la biblioteca externa. Los valores válidos son 'R'. Tiempos de ejecución adicionales podrían agregarse en el futuro.|
|ámbito |int |0 para el ámbito público; 1 para el ámbito privado |  
|scope_desc |varchar(7) |Indica si el paquete es público o privado|


## <a name="see-also"></a>Vea también  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[CREAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Administración de paquetes de SQL Server R Services](../../advanced-analytics/r/installing-and-managing-r-packages.md)  

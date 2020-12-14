---
description: sys.database_scoped_configurations (Transact-SQL)
title: sys.database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
dev_langs:
- TSQL
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: beb536c39db6dbee3bc2e0855de20282bc994fe4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404731"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Contiene una fila por cada configuración. 

|Nombre de la columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|IDENTIFICADOR de la opción de configuración.|
|**name**|**nvarchar(60)**|Nombre de la opción de configuración. Para obtener información sobre las posibles configuraciones, vea [ALTER DATABASE scoped CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**value**|**SQLVARIANT**|Valor establecido para esta opción de configuración para la réplica principal.|
|**value_for_secondary**|**SQLVARIANT**|Valor establecido para esta opción de configuración para las réplicas secundarias.|
|**is_value_default**|**bit** |Especifica si el conjunto de valores es el valor predeterminado.|

## <a name="permissions"></a><a name="Permissions"></a> Permisos

Debe pertenecer al rol **public** .

## <a name="remarks"></a>Comentarios

Cuando se devuelve NULL como valor de **value_for_secondary**, esto significa que el secundario se establece en Primary.
 
Las opciones de configuración con ámbito de base de datos se transfieren con la base de datos. Esto significa que cuando se restaura o adjunta una base de datos, se conservan las opciones de configuración existentes.

## <a name="see-also"></a>Consulte también

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)

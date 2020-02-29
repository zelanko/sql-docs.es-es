---
title: Sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
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
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: 372d3a1b5722b1a19e9560fe92f61e45b6744ace
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78180114"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>Sys. database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Contiene una fila por cada configuración. 

|Nombre de la columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|IDENTIFICADOR de la opción de configuración.|
|**Name**|**nvarchar (60)**|Nombre de la opción de configuración. Para obtener información sobre las posibles configuraciones, vea [ALTER DATABASE scoped CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**value**|**SQLVARIANT**|Valor establecido para esta opción de configuración para la réplica principal.|
|**value_for_secondary**|**SQLVARIANT**|Valor establecido para esta opción de configuración para las réplicas secundarias.|
|**is_value_default**|**bit** |Especifica si el conjunto de valores es el valor predeterminado.|
|**dw_compatibility_level**|**int**|Nivel de compatibilidad de la base de datos.  Valor predeterminado = 0 (automático)|

## <a name="Permissions"></a> Permisos

Debe pertenecer al rol **public** .

## <a name="remarks"></a>Observaciones

Cuando se devuelve NULL como valor de **value_for_secondary**, esto significa que el secundario se establece en Primary.
 
Las opciones de configuración con ámbito de base de datos se transfieren con la base de datos. Esto significa que cuando se restaura o adjunta una base de datos, se conservan las opciones de configuración existentes.

## <a name="see-also"></a>Consulte también

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)

---
description: CURRENT_TIMEZONE (Transact-SQL)
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 60eb4edd5f52bb160b3be2fad2757b649a59d474
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115245"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Esta función devuelve el nombre de la zona horaria observada por un servidor o una instancia. Para SQL Managed Instance, el valor devuelto se basa en la zona horaria de la propia instancia asignada durante la creación de la instancia, no en la zona horaria del sistema operativo subyacente.
  
> [!NOTE]  
> Para SQL Database, la zona horaria siempre se establece en UTC y `CURRENT_TIMEZONE` devuelve el nombre de la zona horaria UTC.
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>Argumentos

Esta función no toma ningún argumento.
  
## <a name="return-type"></a>Tipo de valor devuelto  

**varchar**
  
## <a name="remarks"></a>Observaciones  

`CURRENT_TIMEZONE` es una función no determinista. Las vistas y las expresiones que hacen referencia a esta columna no se pueden indizar.
  
## <a name="example"></a>Ejemplo

Tenga en cuenta que el valor devuelto reflejará la configuración real de la zona horaria y el idioma del servidor o de la instancia.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>Consulte también

[Zonas horarias de SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)

[CURRENT_TIMEZONE_ID()](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-id-transact-sql)

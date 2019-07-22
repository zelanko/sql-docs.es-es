---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
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
ms.openlocfilehash: 6c29cfba3f47506cb88860763d6650cfb3ecab7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026388"
---
# <a name="currenttimezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Esta función devuelve el nombre de la zona horaria observada por un servidor o una instancia. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`CURRENT_TIMEZONE` deriva el valor devuelto del sistema operativo del equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para Instancia administrada de SQL Database el valor devuelto se basa en la zona horaria de la propia instancia asignada durante la creación de la instancia, no en la zona horaria del sistema operativo subyacente.
  
> [!NOTE]  
> Para instancias de SQL Database individuales y agrupadas, la zona horaria siempre se establece en UTC y `CURRENT_TIMEZONE` devuelve el nombre de la zona horaria UTC.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>Argumentos

Esta función no toma ningún argumento.
  
## <a name="return-type"></a>Tipo devuelto  

**varchar**
  
## <a name="remarks"></a>Notas  

`CURRENT_TIMEZONE` es una función no determinista. Las vistas y las expresiones que hacen referencia a esta columna no se pueden indizar.
  
## <a name="example"></a>Ejemplo

Tenga en cuenta que el valor devuelto reflejará la configuración real de la zona horaria y el idioma del servidor o de la instancia.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>Vea también

[Zona horaria de Instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)

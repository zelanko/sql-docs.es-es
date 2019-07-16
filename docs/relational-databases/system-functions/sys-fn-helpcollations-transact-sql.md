---
title: sys.fn_helpcollations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016|| = azure-sqldw-latest ||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee626b9eef8cf2f2e80217b2a3709271a227f293
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906122"
---
# <a name="sysfnhelpcollations-transact-sql"></a>sys.fn_helpcollations (Transact-SQL)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Devuelve una lista de todas las intercalaciones admitidas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>Tablas devueltas

 **fn_helpcollations** devuelve la siguiente información.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|NOMBRE|**sysname**|Nombre de intercalación estándar|  
|Descripción|**nvarchar(1000)**|Descripción de la intercalación|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite intercalaciones de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admite un número limitado (< 80) de las intercalaciones denominadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intercalaciones, que se desarrollaron antes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite las intercalaciones de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las intercalaciones se siguen admitiendo por compatibilidad con versiones anteriores, pero no puede utilizarse para nuevos trabajos de desarrollo. Para obtener más información sobre la intercalación de Windows, consulte [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md). Para obtener más información sobre las intercalaciones, vea [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos

 En el ejemplo siguiente se devuelven todos los nombres de intercalación que comienzan por la letra `L` y que son intercalaciones de orden binario.

> [!Note]
> En la base de datos maestra, se deben ejecutar consultas de Azure SQL Data Warehouse en fn_helpcollations.  
  
```sql  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```
  
## <a name="see-also"></a>Vea también

[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Compatibilidad con la intercalación de base de datos de Azure SQL Data Warehouse](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  
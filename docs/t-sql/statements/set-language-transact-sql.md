---
title: SET LANGUAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET_LANGUAGE_TSQL
- SET LANGUAGE
dev_langs:
- TSQL
helpviewer_keywords:
- LANGUAGE option
- languages [SQL Server], setting language
- SET LANGUAGE statement
- options [SQL Server], date
- default languages
ms.assetid: 0ec0e5cf-e115-4be9-a0db-e65837d6fa45
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ca1afbc76d7ee7562eee7d0f1b3e81963ae19014
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="set-language-transact-sql"></a>SET LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Especifica el entorno de idioma de la sesión. El idioma de la sesión determina los formatos de **datetime** y los mensajes del sistema.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET LANGUAGE { [ N ] 'language' | @language_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 [**N**]**'***language***'** | **@***language_var*  
 Es el nombre del idioma tal como está almacenado en [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Este argumento puede ser Unicode o DBCS convertido a Unicode. Para especificar un idioma en Unicode, use **N'***language***'**. Si se especifica como variable, esta debe ser **sysname**.  
  
## <a name="remarks"></a>Notas  
 La opción SET LANGUAGE se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 SET LANGUAGE establece la opción [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) de forma implícita.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establece el idioma predeterminado en `Italian`, se muestra el nombre del mes y, después, se cambia de nuevo a `us_english` y se vuelve a mostrar el nombre del mes.  
  
```  
DECLARE @Today DATETIME;  
SET @Today = '12/5/2007';  
  
SET LANGUAGE Italian;  
SELECT DATENAME(month, @Today) AS 'Month Name';  
  
SET LANGUAGE us_english;  
SELECT DATENAME(month, @Today) AS 'Month Name' ;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

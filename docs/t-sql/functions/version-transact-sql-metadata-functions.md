---
description: Versión - Funciones de metadatos de Transact SQL
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 82ae0f0b2ef46cf1082d5d0fe7fc064e3c538ee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88361591"
---
# <a name="version---transact-sql-metadata-functions"></a>Versión - Funciones de metadatos de Transact SQL
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 Devuelve la versión de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] en ejecución en el dispositivo.  
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="general-remarks"></a>Notas generales  
Debe especificarse un nombre de tabla en una cláusula [FROM](../../t-sql/queries/from-transact-sql.md) para esta función para que devuelva resultados. Se devolverá una fila de resultados para cada fila del conjunto de resultados de la consulta; use [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) para limitar el número de filas devueltas.  
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente se devuelve el número de la versión.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>Vea también 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  

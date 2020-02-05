---
title: Funciones JSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5b83e6f6eefce1cf56b71e7d433dca19cb4575d1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68109418"
---
# <a name="json-functions-transact-sql"></a>Funciones JSON (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Use las funciones descritas en las páginas de esta sección para validar o cambiar el texto JSON o para extraer valores simples o complejos.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[ISJSON](../../t-sql/functions/isjson-transact-sql.md)|Prueba si una cadena contiene un valor JSON válido.|  
|[JSON_VALUE](../../t-sql/functions/json-value-transact-sql.md)|Extrae un valor escalar de una cadena JSON.|  
|[JSON_QUERY](../../t-sql/functions/json-query-transact-sql.md)|Extrae un objeto o una matriz desde una cadena JSON.|  
|[JSON_MODIFY](../../t-sql/functions/json-modify-transact-sql.md)|Actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.|

 Para obtener más información sobre la compatibilidad integrada con JSON en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Datos JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md).  

## <a name="see-also"></a>Consulte también

 - [Validar, consultar y cambiar datos JSON con funciones integradas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)
 - [Expresiones de ruta de acceso JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)
 - [Datos JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  

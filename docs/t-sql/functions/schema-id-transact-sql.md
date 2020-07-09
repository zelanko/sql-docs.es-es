---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00a3667c5e058bcc25faa4195af3d676ae9cdf08
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003671"
---
# <a name="schema_id-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Devuelve el identificador de esquema asociado a un nombre de esquema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|----------|----------------|  
|*schema_name*|Es el nombre del esquema. *schema_name* es **sysname**. Si *schema_name* no se especifica, SCHEMA_ID devolverá el identificador del esquema predeterminado del autor de la llamada.|  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **int**  
  
 Se devolverá NULL si *schema_name* no es un esquema válido.  
  
## <a name="remarks"></a>Observaciones  
 SCHEMA_ID devolverá los Id. de los esquemas del sistema y de los esquemas definidos por el usuario. Se puede llamar a SCHEMA_ID en una lista de selección, en una cláusula WHERE y en cualquier lugar en el que se permita una expresión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. Devolver el identificador del esquema predeterminado del llamador  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Devolver el identificador de un esquema con nombre  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


---
title: Quitar tabla externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 7cf14c5782a5cdc876b04600447892932f9e9921
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-table-transact-sql"></a>Quitar tabla externa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Quita una tabla externa de PolyBase de. Esto no elimina los datos externos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>Argumentos  
 [ *database_name* . [*schema_name*]. | *schema_name* . ] *table_name*  
 El nombre de una a tres partes de la tabla externa para quitar. El nombre de tabla puede incluir opcionalmente el esquema, o la base de datos y el esquema.  
  
## <a name="permissions"></a>Permissions  
  
-   Requiere **ALTER** permiso en el esquema al que pertenece la tabla.  
  
## <a name="general-remarks"></a>Notas generales  
 Al quitar una tabla externa, quitan todos los metadatos relacionados con la tabla. No elimina los datos externos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-basic-syntax"></a>A. Con la sintaxis básica  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. Quitar una tabla externa de la base de datos actual  
 En el ejemplo siguiente se quita el `ProductVendor1` tabla, sus datos, índices y las vistas dependientes de la base de datos actual.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. Quitar una tabla de otra base de datos  
 En el siguiente ejemplo se quita la tabla `SalesPerson` de la base de datos `EasternDivision`.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  



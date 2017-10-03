---
title: OPENQUERY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2a3ad57f9cd898d4c059df725b380be28622035e
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ejecuta la consulta de paso a través especificada en el servidor vinculado especificado. Este servidor es un origen de datos OLE DB. Se puede hacer referencia a OPENQUERY en la cláusula FROM de una consulta como si fuera un nombre de tabla. También se puede hacer referencia a OPENQUERY como la tabla de destino de una instrucción INSERT, UPDATE, DELETE o TRUNCATE. Esto está sujeto a las capacidades del proveedor OLE DB. Aunque la consulta puede devolver varios conjuntos de resultados, OPENQUERY solo devuelve el primero.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *linked_server*  
 Es un identificador que representa el nombre del servidor vinculado.  
  
 **'** *consulta* **'**  
 Es la cadena de consulta que se ejecuta en el servidor vinculado. La longitud máxima de la cadena es de 8 KB.  
  
## <a name="remarks"></a>Comentarios  
 OPENQUERY no acepta variables para sus argumentos.  
  
 No se puede utilizar OPENQUERY para ejecutar procedimientos almacenados extendidos en un servidor vinculado. Sin embargo, se puede ejecutar un procedimiento almacenado extendido en un servidor vinculado mediante un nombre de cuatro partes. Por ejemplo:  
  
```t-sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 Las llamadas a OPENDATASOURCE, OPENQUERY u OPENROWSET en la cláusula FROM se evalúan por separado y de forma independiente de otras llamadas a estas funciones utilizadas como destino de la actualización, incluso si se han suministrado argumentos idénticos a las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
## <a name="permissions"></a>Permissions  
 Cualquier usuario puede ejecutar OPENQUERY. Los permisos utilizados para conectarse al servidor remoto se obtienen de la configuración definida para el servidor vinculado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. Ejecutar una consulta UPDATE de paso a través  
 En el ejemplo siguiente se usa una consulta `UPDATE` de paso a través en el servidor vinculado creado en el ejemplo A.  
  
```t-sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. Ejecutar una consulta INSERT de paso a través  
 En el ejemplo siguiente se usa una consulta `INSERT` de paso a través en el servidor vinculado creado en el ejemplo A.  
  
```t-sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. Ejecutar una consulta DELETE de paso a través  
 En el ejemplo siguiente se usa una consulta `DELETE` de paso a través para eliminar la columna insertada en el ejemplo C.  
  
```t-sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. Ejecutar una consulta SELECT de paso a través  
 En el ejemplo siguiente se utiliza un acceso directo `SELECT` consulta para seleccionar la fila insertada en el ejemplo C.  
  
```t-sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>Vea también  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Funciones de conjunto de filas &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


---
title: SESSION_USER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_USER_TSQL
- SESSION_USER
dev_langs: TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- sessions [SQL Server], user names
- displaying user names
- viewing user names
- SESSION_USER function
ms.assetid: 3dbe8532-31b6-4862-8b2a-e58b00b964de
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 96d5050eedfa87599b2b06a1e22b88bda45860e0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sessionuser-transact-sql"></a>SESSION_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SESSION_USER devuelve el nombre de usuario del contexto actual en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SESSION_USER  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentarios  
 Utilice SESSION_USER con restricciones DEFAULT en las instrucciones CREATE TABLE o ALTER TABLE, o utilícela como cualquier función estándar. SESSION_USER se puede insertar en una tabla cuando no se especifica un valor predeterminado. Esta función no toma ningún argumento. SESSION_USER se puede utilizar en consultas.  
  
 Si se llama a SESSION_USER después de un cambio de contexto, SESSION_USER devolverá el nombre de usuario del contexto representado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-sessionuser-to-return-the-user-name-of-the-current-session"></a>A. Utilizar SESSION_USER para devolver el nombre de usuario de la sesión actual  
 En el siguiente ejemplo se declara una variable como `nchar`, se le asigna el valor actual de `SESSION_USER` y, a continuación, se imprime la variable con una descripción de texto.  
  
```  
DECLARE @session_usr nchar(30);  
SET @session_usr = SESSION_USER;  
SELECT 'This session''s current user is: '+ @session_usr;  
GO  
```  
  
 Éste es el conjunto de resultados cuando el usuario de la sesión es `Surya`:  
  
 ```
--------------------------------------------------------------
This session's current user is: Surya

(1 row(s) affected)
```  
  
### <a name="b-using-sessionuser-with-default-constraints"></a>B. Utilizar SESSION_USER con restricciones DEFAULT  
 En el siguiente ejemplo se crea una tabla que utiliza `SESSION_USER` como una restricción `DEFAULT` para el nombre de la persona que registra la recepción de un envío.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE deliveries3  
(  
 order_id int IDENTITY(5000, 1) NOT NULL,  
 cust_id  int NOT NULL,  
 order_date smalldatetime NOT NULL DEFAULT GETDATE(),  
 delivery_date smalldatetime NOT NULL DEFAULT   
    DATEADD(dd, 10, GETDATE()),  
 received_shipment nchar(30) NOT NULL DEFAULT SESSION_USER  
);  
GO  
```  
  
 Los registros agregados a la tabla se mostrarán con el nombre de usuario del usuario actual. En este ejemplo, `Wanida`, `Sylvester` y `Alejandro` comprueban la recepción de los envíos. Se puede simular si se cambia el contexto del usuario con `EXECUTE AS`.  
  
```  
EXECUTE AS USER = 'Wanida'  
INSERT deliveries3 (cust_id)  
VALUES (7510);  
INSERT deliveries3 (cust_id)  
VALUES (7231);  
REVERT;  
EXECUTE AS USER = 'Sylvester'  
INSERT deliveries3 (cust_id)  
VALUES (7028);  
REVERT;  
EXECUTE AS USER = 'Alejandro'  
INSERT deliveries3 (cust_id)  
VALUES (7392);  
INSERT deliveries3 (cust_id)  
VALUES (7452);  
REVERT;  
GO  
```  
  
 La siguiente consulta selecciona toda la información de la tabla `deliveries3`.  
  
```  
SELECT order_id AS 'Order #', cust_id AS 'Customer #',   
   delivery_date AS 'When Delivered', received_shipment   
   AS 'Received By'  
FROM deliveries3  
ORDER BY order_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Order #   Customer #  When Delivered       Received By
--------  ----------  -------------------  -----------
5000      7510        2005-03-16 12:02:14  Wanida
5001      7231        2005-03-16 12:02:14  Wanida
5002      7028        2005-03-16 12:02:14  Sylvester
5003      7392        2005-03-16 12:02:14  Alejandro
5004      7452        2005-03-16 12:02:14  Alejandro

(5 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-sessionuser-to-return-the-user-name-of-the-current-session"></a>C: Utilizar SESSION_USER para devolver el nombre de usuario de la sesión actual  
 En el ejemplo siguiente se devuelve el usuario de la sesión para la sesión actual.  
  
```  
SELECT SESSION_USER;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40; Transact-SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40; Transact-SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SYSTEM_USER &#40; Transact-SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [USUARIO &#40; Transact-SQL &#41;](../../t-sql/functions/user-transact-sql.md)   
 [User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
  
  


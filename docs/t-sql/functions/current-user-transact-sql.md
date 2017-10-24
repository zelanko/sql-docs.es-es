---
title: CURRENT_USER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_USER
- CURRENT_USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- niladic functions
- CURRENT_USER
- users [SQL Server], names
ms.assetid: 29248949-325b-4063-9f55-5a445fb35c6e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7fbb100c34c2a8b1b33a585cb5ead6aaca56f0d8
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="currentuser-transact-sql"></a>CURRENT_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el nombre de usuario actual. Esta función es equivalente a USER_NAME().
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CURRENT_USER  
```  

## <a name="return-types"></a>Tipos de valor devuelto
**sysname**
  
## <a name="remarks"></a>Comentarios  
CURRENT_USER devuelve el nombre del contexto de seguridad actual. Si CURRENT_USER se ejecuta después de una llamada a EXECUTE AS, cambia el contexto; CURRENT_USER devolverá el nombre del contexto suplantado. Si una entidad de seguridad de Windows ha tenido acceso a la base de datos en concepto de pertenencia a un grupo, se devolverá el nombre de la entidad de seguridad de Windows en vez del nombre del grupo.
  
Para devolver el inicio de sesión del usuario actual, vea [SUSER_NAME &#40; Transact-SQL &#41; ](../../t-sql/functions/suser-name-transact-sql.md) y [SYSTEM_USER &#40; Transact-SQL &#41; ](../../t-sql/functions/system-user-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-currentuser-to-return-the-current-user-name"></a>A. Usar CURRENT_USER para devolver el nombre del usuario actual  
En el ejemplo siguiente se devuelve el nombre del usuario actual.
  
```sql
SELECT CURRENT_USER;  
GO  
```  
  
### <a name="b-using-currentuser-as-a-default-constraint"></a>B. Usar CURRENT_USER como restricción DEFAULT  
En el siguiente ejemplo se crea una tabla que usa `CURRENT_USER` como restricción `DEFAULT` para la columna `order_person` en una fila de ventas.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'orders22')  
   DROP TABLE orders22;  
GO  
SET NOCOUNT ON;  
CREATE TABLE orders22  
(  
order_id int IDENTITY(1000, 1) NOT NULL,
cust_id  int NOT NULL,
order_date smalldatetime NOT NULL DEFAULT GETDATE(),
order_amt money NOT NULL,
order_person char(30) NOT NULL DEFAULT CURRENT_USER
);  
GO  
```  
  
El siguiente código inserta un registro en la tabla. El usuario que ejecuta estas instrucciones se denomina `Wanida`.
  
```sql
INSERT orders22 (cust_id, order_amt)  
VALUES (5105, 577.95);  
GO  
SET NOCOUNT OFF;  
GO  
```  
  
La siguiente consulta selecciona toda la información de la tabla `orders22`.
  
```sql
SELECT * FROM orders22;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
order_id    cust_id     order_date           order_amt    order_person
----------- ----------- -------------------- ------------ ------------
1000        5105        2005-04-03 23:34:00  577.95       Wanida
  
(1 row(s) affected)
```
  
### <a name="c-using-currentuser-from-an-impersonated-context"></a>C. Usar CURRENT_USER desde un contexto suplantado  
En el siguiente ejemplo, el usuario `Wanida` ejecuta el siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
```sql
SELECT CURRENT_USER;  
GO  
EXECUTE AS USER = 'Arnalfo';  
GO  
SELECT CURRENT_USER;  
GO  
REVERT;  
GO  
SELECT CURRENT_USER;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Wanida
Arnalfo
Wanida
```
  
## <a name="see-also"></a>Vea también
[User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
[SYSTEM_USER &#40; Transact-SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  



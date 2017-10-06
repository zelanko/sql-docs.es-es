---
title: SYSTEM_USER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSTEM_USER_TSQL
- SYSTEM_USER
dev_langs:
- TSQL
helpviewer_keywords:
- current user names
- system-supplied user names [SQL Server]
- users [SQL Server], logins
- logins [SQL Server], identification name
- current system user names
- SYSTEM_USER function
- inserting system user name into table
- system usernames [SQL Server]
- users [SQL Server], names
ms.assetid: 565984cd-60c6-4df7-83ea-2349b838ccb2
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3f13d5db5d7787a60c455edc64644f4c23779fc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="systemuser-transact-sql"></a>SYSTEM_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Permite insertar en una tabla un valor proporcionado por el sistema para el inicio de sesión actual cuando no se especifica ningún valor predeterminado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SYSTEM_USER  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nchar**  
  
## <a name="remarks"></a>Comentarios  
 En las instrucciones CREATE TABLE y ALTER TABLE puede utilizar la función SYSTEM_USER con restricciones DEFAULT. También puede utilizarla como cualquier función estándar.  
  
 Si el nombre de usuario y el nombre de inicio de sesión con diferentes, SYSTEM_USER devuelve el nombre de inicio de sesión.  
  
 Si el usuario actual ha iniciado sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación de Windows, SYSTEM_USER devuelve el nombre de identificación de inicio de sesión de Windows con el formato: *dominio*\\*user_login_name*. Sin embargo, si el usuario actual ha iniciado la sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la autenticación de SQL Server, SYSTEM_USER devuelve el nombre de identificación de inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por ejemplo `WillisJo` para un usuario que ha iniciado la sesión como `WillisJo`.  
  
 SYSTEM_USER devuelve el nombre del contexto de ejecución actual. Si se ha usado la instrucción EXECUTE AS para cambiar el contexto, SYSTEM_USER devuelve el nombre del contexto suplantado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-systemuser-to-return-the-current-system-user-name"></a>A. Usar SYSTEM_USER para devolver el nombre de usuario actual del sistema  
 En el siguiente ejemplo se declara una variable `char`, se almacena en ella el valor actual de `SYSTEM_USER` y, a continuación, se imprime el valor almacenado en la variable.  
  
```  
DECLARE @sys_usr char(30);  
SET @sys_usr = SYSTEM_USER;  
SELECT 'The current system user is: '+ @sys_usr;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------------------------------------------------------
The current system user is: WillisJo

(1 row(s) affected)
 ```  
  
### <a name="b-using-systemuser-with-default-constraints"></a>B. Usar SYSTEM_USER con restricciones DEFAULT  
 En el siguiente ejemplo se crea una tabla con `SYSTEM_USER` como una restricción `DEFAULT` para la columna `SRep_tracking_user`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.Sales_Tracking  
(  
    Territory_id int IDENTITY(2000, 1) NOT NULL,  
    Rep_id  int NOT NULL,  
    Last_sale datetime NOT NULL DEFAULT GETDATE(),  
    SRep_tracking_user varchar(30) NOT NULL DEFAULT SYSTEM_USER  
);  
GO  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (151);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (293, '19980515');  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (27882, '19980620');  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (21392);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (24283, '19981130');  
GO  
```  
  
 En la siguiente consulta se selecciona toda la información de la tabla `Sales_Tracking`:  
  
```  
SELECT * FROM Sales_Tracking ORDER BY Rep_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Territory_id Rep_id Last_sale            SRep_tracking_user
-----------  ------ -------------------- ------------------
2000         151    Mar 4 1998 10:36AM   ArvinDak
2001         293    May 15 1998 12:00AM  ArvinDak
2003         21392  Mar 4 1998 10:36AM   ArvinDak
2004         24283  Nov 3 1998 12:00AM   ArvinDak
2002         27882  Jun 20 1998 12:00AM  ArvinDak
  
(5 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-systemuser-to-return-the-current-system-user-name"></a>C: usar SYSTEM_USER para devolver el nombre de usuario actual del sistema  
 En el ejemplo siguiente se devuelve el valor actual de `SYSTEM_USER`.  
  
```  
SELECT SYSTEM_USER;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40; Transact-SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40; Transact-SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40; Transact-SQL &#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [USUARIO &#40; Transact-SQL &#41;](../../t-sql/functions/user-transact-sql.md)  
  
  



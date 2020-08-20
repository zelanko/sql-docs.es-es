---
description: 'Tutorial: Ownership Chains and Context Switching'
title: 'Tutorial: Ownership Chains and Context Switching'
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b26b475fbef54f501d1b40dc1c1b35df796b27ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472971"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Cadenas de propiedad y cambio de contexto
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
En este tutorial se usa un escenario para ilustrar los conceptos de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] relacionados con las cadenas de propiedad y el cambio de contexto de usuario.  
  
> [!NOTE]  
> Para ejecutar el código de este tutorial, la seguridad de modo mixto debe estar configurada y la base de datos AdventureWorks2017 debe estar instalada. Para obtener más información sobre la seguridad de modo mixto, consulte [Elegir un modo de autenticación](../relational-databases/security/choose-an-authentication-mode.md).  
  
## <a name="scenario"></a>Escenario  
En este escenario, dos usuarios necesitan cuentas para acceder a los datos de los pedidos de compra almacenados en la base de datos AdventureWorks2017. Los requisitos son los siguientes:  
  
-   La primera cuenta (TestManagerUser) debe poder ver todos los detalles de cada pedido de compra.  
-   La segunda cuenta (TestEmployeeUser) debe poder ver el número de los pedidos de compra, la fecha de los pedidos, la fecha de envío, los números de identificación de los productos y los elementos pedidos y recibidos en cada pedido de compra, ordenados por número de pedido de compra, correspondientes a los elementos para los que se han recibido envíos parciales.  
-   El resto de cuentas deben conservar sus permisos.   
Para cumplir los requisitos de este escenario, el ejemplo se ha dividido en cuatro partes que describen los conceptos de cadenas de propiedad y cambio de contexto:  
  
1.  Configuración del entorno.   
2.  Creación de un procedimiento almacenado para obtener acceso a datos por pedido de compra.   
3.  Acceso a los datos mediante un procedimiento almacenado.  
4.  Restablecimiento del entorno.  

Cada bloque de código incluido en este ejemplo se describe en línea. Para copiar el ejemplo completo, vea [Ejemplo completo](#CompleteExample) al final de este tutorial.

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor que ejecute SQL Server y una base de datos de AdventureWorks.

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargue las [bases de datos de ejemplo de AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Para obtener instrucciones sobre cómo restaurar una base de datos en SQL Server Management Studio, vea [Restauración de una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).   
  
## <a name="1-configure-the-environment"></a>1. Configurar el entorno  
Use [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y el código siguiente para abrir la base de datos `AdventureWorks2017` y use la instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] `CURRENT_USER` para comprobar que el usuario dbo se muestra como contexto.  
  
```sql
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
Para obtener más información sobre la instrucción CURRENT_USER, consulte [CURRENT_USER &#40;Transact-SQL&#41;](../t-sql/functions/current-user-transact-sql.md).  
  
Use este código como el usuario dbo para crear dos usuarios en el servidor y en la base de datos AdventureWorks2017.  
  
```sql
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
Para obtener más información sobre la instrucción CREATE USER, consulte [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md). Para obtener más información sobre la instrucción CREATE LOGIN, consulte [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md).  
  
Use el código siguiente para cambiar la propiedad del esquema `Purchasing` a la cuenta `TestManagerUser` . Esto permite que dicha cuenta use todo el acceso a las instrucciones del lenguaje de manipulación de datos (DML) (por ejemplo, los permisos `SELECT` e `INSERT` ) en los objetos que contiene. `TestManagerUser` también tiene la capacidad de crear procedimientos almacenados.  
  
```sql
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
Para obtener más información sobre la instrucción GRANT, consulte [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md). Para obtener más información sobre los procedimientos almacenados, consulte [Procedimientos almacenados &#40;motor de base de datos&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md). Para ver un cartel de todos los permisos del [!INCLUDE[ssDE](../includes/ssde-md.md)], vea [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster).  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2. Crear un procedimiento almacenado para obtener acceso a los datos  
Para cambiar el contexto dentro de una base de datos, use la instrucción EXECUTE AS. EXECUTE AS requiere permisos IMPERSONATE.  
  
Use la instrucción `EXECUTE AS` en el código siguiente para cambiar el contexto a `TestManagerUser` y crear un procedimiento almacenado que muestre únicamente los datos exigidos por `TestEmployeeUser`. Para cumplir los requisitos, el procedimiento almacenado acepta una variable para el número del pedido de compra y no muestra la información financiera, y la cláusula WHERE limita los resultados a los envíos parciales.  
  
```sql
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
En estos momentos, `TestEmployeeUser` no tiene acceso a ningún objeto de la base de datos. El código siguiente (todavía en el contexto de `TestManagerUser` ) permite que la cuenta de usuario consulte la información de tabla base mediante el procedimiento almacenado.  
  
```sql
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
El procedimiento almacenado forma parte del esquema de `Purchasing` , aunque no se especifica explícitamente ningún esquema, porque `TestManagerUser` se asigna de forma predeterminada al esquema `Purchasing` . La información del catálogo del sistema se puede utilizar para buscar objetos, tal y como se muestra en el código siguiente.  
  
```sql
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
Una vez finalizada esta sección del ejemplo, el código vuelve a cambiar el contexto a dbo mediante la instrucción `REVERT`.  
  
```sql
REVERT;  
GO  
```  
  
Para obtener más información sobre la instrucción REVERT, consulte [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md).  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3. Obtener acceso a los datos mediante el procedimiento almacenado  
`TestEmployeeUser` no tiene ningún permiso en los objetos de la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] aparte del inicio de sesión y los derechos asignados al rol de base de datos pública. El código siguiente devuelve un error cuando `TestEmployeeUser` intenta obtener acceso a las tablas base.  
  
```sql
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  

El error que se devuelve:
```
Msg 229, Level 14, State 5, Line 6
The SELECT permission was denied on the object 'PurchaseOrderHeader', database 'AdventureWorks2017', schema 'Purchasing'.
```
  
Puesto que los objetos a los que hace referencia el procedimiento almacenado, creados en la última sección, pertenecen a `TestManagerUser` en virtud de la propiedad de esquema `Purchasing` , `TestEmployeeUser` puede tener acceso a las tablas base mediante el procedimiento almacenado. El código siguiente, que todavía usa el contexto `TestEmployeeUser` , pasa el pedido de compra 952 como un parámetro.  
  
```sql
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4. Restablecer el entorno  
El código siguiente usa el comando `REVERT` para devolver el contexto de la cuenta actual a `dbo`y, a continuación, restablece el entorno.  
  
```sql
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="complete-example"></a><a name="CompleteExample"></a>Ejemplo completo  
En esta sección se muestra el código de ejemplo completo.  
  
> [!NOTE]  
> Este código no incluye los dos errores esperados que demuestran la incapacidad de `TestEmployeeUser` para seleccionar en las tablas base.  
  
```sql
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2017;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
[Centro de seguridad para el Motor de base de datos de SQL Server y Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  

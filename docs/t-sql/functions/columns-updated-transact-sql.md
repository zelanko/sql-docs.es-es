---
title: COLUMNS_UPDATED (Transact-SQL) | Documentos de Microsoft
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
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ddb7462ee985ee62efa70455d27c91a51193124
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **varbinary** patrón de bits que indica las columnas de una tabla o vista que fueron insertadas o actualizadas. COLUMNS_UPDATED se utiliza en cualquier parte del cuerpo de un desencadenador INSERT o UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)] para comprobar si el desencadenador debe ejecutar determinadas acciones.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>Tipos de valor devuelto
**varbinary**
  
## <a name="remarks"></a>Comentarios  
COLUMNS_UPDATED comprueba las acciones UPDATE o INSERT realizadas en varias columnas. Para comprobar los intentos de UPDATE o INSERT en una columna, use [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md).
  
COLUMNS_UPDATED devuelve uno o varios bytes ordenados de izquierda a derecha, donde el primer bit por la derecha es el menos importante de cada byte. El primer bit por la derecha del byte más a la izquierda representa la primera columna de la tabla, el siguiente bit a la izquierda representa la segunda columna, y así sucesivamente. COLUMNS_UPDATED devuelve varios bytes si la tabla en que se ha creado el desencadenador contiene más de 8 columnas, siendo el menos significativo el primero por la izquierda. COLUMNS_UPDATED devuelve el valor TRUE en todas las columnas de las acciones INSERT porque en las columnas se insertaron valores explícitos o implícitos (NULL).
  
Para comprobar las actualizaciones o inserciones de columnas específicas, siga la sintaxis con un operador bit a bit y una máscara de bits de enteros de las columnas que se están comprobando. Por ejemplo, tabla **t1** contiene columnas **C1**, **C2**, **C3**, **C4**, y **C5** . Para comprobar que las columnas **C2**, **C3**, y **C4** están todos actualizado (con la tabla **t1** tiene un desencadenador UPDATE), siga la sintaxis con **& 14**. Para comprobar si la única columna **C2** está actualizado, especifique **& 2**.
  
COLUMNS_UPDATED puede utilizarse en cualquier parte dentro de un desencadenador INSERT o UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
La columna ORDINAL_POSITION de la vista INFORMATION_SCHEMA.COLUMNS no es compatible con el patrón de bits de las columnas devueltas por COLUMNS_UPDATED. Para obtener un patrón de bits compatible con COLUMNS_UPDATED, haga referencia a la propiedad `ColumnID` de la función del sistema `COLUMNPROPERTY` cuando realice una consulta de la vista `INFORMATION_SCHEMA.COLUMNS`, como se muestra en el siguiente ejemplo.
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  
  
## <a name="column-sets"></a>Conjuntos de columnas
Cuando un conjunto de columnas se define en una tabla, la función COLUMNS_UPDATED se comporta de las maneras siguientes:
-   Cuando una columna que es miembro del conjunto de columnas se actualiza de forma explícita, el bit correspondiente para dicha columna se establece en 1, y el bit para el conjunto de columnas se establece en 1.  
-   Cuando un conjunto de columnas se actualiza de forma explícita, el bit para dicho conjunto de columnas se establece en 1, y los bits para todas las columnas dispersas de la tabla se establecen en 1.  
-   En las operaciones de inserción, todos los bits se establecen en 1.  
  
     Dado que los cambios en un conjunto de columnas hacen que los bits de todas las columnas del conjunto de columnas se establezcan en 1, parecerá que se han modificado las columnas de un conjunto cuyas columnas no se cambiaron. Para obtener más información sobre los conjuntos de columnas, vea [Usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>A. Usar COLUMNS_UPDATED para comprobar las primeras ocho columnas de una tabla.  
En el siguiente ejemplo se crean dos tablas: `employeeData` y `auditEmployeeData`. La tabla `employeeData` contiene información confidencial de los sueldos de los empleados y puede ser modificada por los miembros del departamento de recursos humanos. Si se cambia el número de seguridad social, el sueldo anual o el número de cuenta bancaria de un empleado, se genera un registro de auditoría y se inserta en la tabla de auditoría `auditEmployeeData`.
  
Con la función `COLUMNS_UPDATED()`, las comprobaciones de los cambios en las columnas que contienen información confidencial sobre los empleados se pueden realizar rápidamente. `COLUMNS_UPDATED()` solo se puede utilizar de esta manera para intentar detectar modificaciones en las primeras ocho columnas de la tabla.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/*Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2,(2-1))+power(2,(3-1))+power(2,(4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of >0  
(below).*/
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/*Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated.*/  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/*Inserting a new employee does not cause the UPDATE trigger to fire.*/  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/*Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/*Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>B. Utilizar COLUMNS_UPDATED para comprobar más de ocho columnas  
Si tiene que comprobar actualizaciones que afectan a otras columnas que no sean las ocho primeras de una tabla, utilice la función `SUBSTRING` para comprobar si `COLUMNS_UPDATED` devuelve el bit correcto. En el ejemplo siguiente, se comprueba las actualizaciones que afectan a otras columnas `3`, `5`, y `9` en el `AdventureWorks2012.Person.Person` tabla.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(),1,1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(),2,1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[ACTUALIZACIÓN &#40; &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  


---
title: IDENTITY (propiedad) (Transact-SQL) | Documentos de Microsoft
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
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1eb7f960210ec89a66f1307d8476e6d47494861f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql-identity-property"></a>CREAR la identidad de la tabla (Transact-SQL) (propiedad)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Crea una columna de identidad en una tabla. Esta propiedad se usa con las instrucciones CREATE TABLE y ALTER TABLE de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  La propiedad IDENTITY es diferente de SQL-DMO **identidad** que expone la propiedad de identidad de fila de una columna.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *valor de inicialización*  
 Es el valor que se utiliza para la primera fila cargada en la tabla.  
  
 *incremento*  
 Se trata del valor incremental que se agrega al valor de identidad de la anterior fila cargada.  
  
 Debe especificar tanto el valor de inicialización como el incremento, o bien ninguno de los dos. Si no se especifica ninguno, el valor predeterminado es (1,1).  
  
## <a name="remarks"></a>Comentarios  
 Las columnas de identidad pueden usarse para generar valores de clave. La propiedad de identidad de una columna garantiza lo siguiente:  
  
-   Cada nuevo valor se genera basándose en el valor de inicialización y el incremento actual.  
  
-   Cada nuevo valor de una transacción determinada es diferente de otras transacciones simultáneas de la tabla.  
  
 La propiedad de identidad de una columna no garantiza lo siguiente:  
  
-   **Unicidad del valor** – exclusividad debe exigirse a través de un **PRIMARY KEY** o **UNIQUE** restricción o **UNIQUE** índice.  
  
-   **Valores consecutivos dentro de una transacción** : no se garantiza que una transacción insertar varias filas obtenga valores consecutivos para las filas, ya que podría producirse otras inserciones simultáneas en la tabla. Si los valores deben ser consecutivos, a continuación, la transacción debe usar un bloqueo exclusivo en la tabla o usar el **SERIALIZABLE** nivel de aislamiento.  
  
-   **Valores consecutivos después de reiniciar el servidor u otros errores** –[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría guardar en caché los valores de identidad por motivos de rendimiento y algunos de los valores asignados podrían perderse durante un reinicio del servidor o error de base de datos. Esto puede tener como resultado espacios en el valor de identidad al insertarlo. Si no es aceptable que haya espacios, la aplicación debe usar mecanismos propios para generar valores de clave. Mediante un generador de secuencias con el **NOCACHE** opción puede limitar los espacios a transacciones que nunca se hayan confirmado.  
  
-   **Reutilización de valores** : para una propiedad de identidad especificada con el valor de inicialización e incremento específico, la identidad que el motor no reutiliza los valores. Si una instrucción de inserción concreta produce un error o si la instrucción de inserción se revierte, los valores de identidad utilizados se pierden y no volverán a generarse. Esto puede tener como resultado espacios cuando se generan los valores de identidad siguientes.  
  
 Estas restricciones forman parte del diseño para mejorar el rendimiento y porque son aceptables en muchas situaciones comunes. Si no puede usar valores de identidad debido a estas restricciones, cree una tabla independiente que contenga un valor actual y administre el acceso a la tabla y la asignación de números con su aplicación.  
  
 Si una tabla con una columna de identidad se publica para replicarla, la columna de identidad debe administrarse de manera apropiada para el tipo de replicación utilizado. Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Solo se puede crear una columna de identidad para cada tabla.  
  
 En las tablas con optimización para memoria, el valor de inicialización y el valor de incremento debe establecerse en 1,1. Si se establece el valor de inicialización o el incremento en un valor distinto de 1 da como resultado el siguiente error: el uso de inicialización e incremento de otros valores de 1 no es compatible con tablas optimizadas en memoria.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. Utilizar la propiedad IDENTITY con CREATE TABLE  
 En el siguiente ejemplo se crea una nueva tabla con la propiedad `IDENTITY` para un número de identificación que se incrementa automáticamente.  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. Utilizar la sintaxis genérica para buscar espacios en los valores de identidad  
 En este ejemplo se muestra la sintaxis genérica utilizada para buscar espacios en valores de identidad cuando se quitan datos.  
  
> [!NOTE]  
>  La primera parte del siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] se ha diseñado solo como ejemplo. Puede ejecutar el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] que comienza por el comentario: `-- Create the img table`.  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR &#40; Transact-SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTIDAD &#40; Función &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40; Transact-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  


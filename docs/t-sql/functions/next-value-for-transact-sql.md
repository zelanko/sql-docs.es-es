---
title: "A continuación valor (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aab8020fa04b978d7ec1b657fe0a1084123dfb48
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Genera un número de secuencia a partir del objeto de secuencia especificado.  
  
 Para obtener más información sobre la creación y uso de secuencias, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md). Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para generar reservar un intervalo de números de secuencia.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos que contiene el objeto de secuencia.  
  
 *schema_name*  
 Nombre del esquema que contiene el objeto de secuencia.  
  
 *sequence_name*  
 Nombre del objeto de secuencia que genera el número.  
  
 *over_order_by_clause*  
 Determina el orden en el que se asigna el valor de secuencia a las filas de una partición. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve un número utilizando el tipo de la secuencia.  
  
## <a name="remarks"></a>Comentarios  
 El **NEXT VALUE FOR** función puede utilizarse en procedimientos almacenados y desencadenadores.  
  
 Cuando el **NEXT VALUE FOR** función se utiliza en una consulta o restricción predeterminada, si el mismo objeto de secuencia se usa más de una vez, o si se utiliza el mismo objeto de secuencia en la instrucción que proporciona los valores y en una restricción default que se está ejecutando, se devolverá el mismo valor para todas las columnas que hacen referencia a la misma secuencia dentro de una fila del conjunto de resultados.  
  
 El **NEXT VALUE FOR** función es determinista y solo se permite en contextos donde se define bien el número de valores de secuencia generados. A continuación se encuentra la definición de cuántos valores se utilizarán para cada objeto de secuencia al que se hace referencia en una instrucción determinada:  
  
-   **Seleccione** -para cada objeto de secuencia que se hace referencia, se genera un nuevo valor una vez por cada fila del resultado de la instrucción.  
  
-   **INSERTAR** ... **VALORES** -para cada objeto de secuencia que se hace referencia, se genera un nuevo valor una vez para cada fila insertada en la instrucción.  
  
-   **ACTUALIZACIÓN** -para cada objeto de secuencia que se hace referencia, se genera un nuevo valor para cada fila actualizada por la instrucción.  
  
-   Instrucciones de procedimiento (como **DECLARE**, **establecer**, etc.)-para cada objeto de secuencia que se hace referencia, se genera un nuevo valor para cada instrucción.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 El **NEXT VALUE FOR** función no se puede usar en las situaciones siguientes:  
  
-   Cuando una base de datos está en modo de solo lectura.  
  
-   Como argumento a una función con valores de tabla.  
  
-   Como argumento a una función de agregado.  
  
-   En subconsultas que contienen expresiones de tabla comunes y tablas derivadas.  
  
-   En vistas, en funciones definidas por el usuario o en columnas calculadas.  
  
-   En una instrucción que usa el **DISTINCT**, **UNION**, **UNION ALL**, **EXCEPT** o **INTERSECT** operador.  
  
-   En una instrucción que usa el **ORDER BY** cláusula a menos que **NEXT VALUE FOR** ... **SOBRE** (**ORDER BY** ...) se utiliza.  
  
-   En las cláusulas siguientes: **capturar**, **sobre**, **salida**, **ON**, **PIVOT**,  **Anulación de DINAMIZACIÓN**, **Agrupar por**, **HAVING**, **proceso**, **CALCULE**, o **FOR XML**.  
  
-   En expresiones condicionales mediante **caso**, **elegir**, **COALESCE**, **IIF**, **ISNULL**, o  **NULLIF**.  
  
-   En un **valores** cláusula que no es parte de un **insertar** instrucción.  
  
-   En la definición de una restricción CHECK.  
  
-   En la definición de una regla u objeto predeterminado. (Se puede utilizar en una restricción predeterminada).  
  
-   Como valor predeterminado de un tipo de tabla definido por el usuario.  
  
-   En una instrucción que usa **arriba**, **desplazamiento**, o cuando la **ROWCOUNT** opción está establecida.  
  
-   En el **donde** cláusula de una instrucción.  
  
-   En un **mezcla** instrucción. (Salvo cuando la **NEXT VALUE FOR** función se utiliza en una restricción default en la tabla de destino y se utiliza el valor predeterminado en el **crear** instrucción de la **mezcla** instrucción.)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>Utilizar un objeto de secuencia en una restricción predeterminada  
 Cuando se usa el **NEXT VALUE FOR** función en una restricción predeterminada, se aplican las siguientes reglas:  
  
-   Se puede hacer referencia a un objeto de secuencia único desde restricciones Default en varias tablas.  
  
-   La tabla y el objeto de secuencia deben residir en la misma base de datos.  
  
-   El usuario que agrega la restricción predeterminada debe tener el permiso REFERENCES en el objeto de secuencia.  
  
-   No se puede quitar un objeto de secuencia al que se haga referencia desde una restricción predeterminada antes de quitar la restricción predeterminada.  
  
-   Se devuelve el mismo número de secuencia para todas las columnas de una fila si varias restricciones Default utilizan el mismo objeto de secuencia, o si el mismo objeto de secuencia se utiliza en la instrucción que proporciona los valores y en una restricción Default que se esté ejecutando.  
  
-   Las referencias a la **NEXT VALUE FOR** función en una restricción predeterminada no se puede especificar el **sobre** cláusula.  
  
-   Se puede modificar un objeto de secuencia al que se haga referencia en una restricción predeterminada.  
  
-   En el caso de un `INSERT … SELECT` o `INSERT … EXEC` instrucción procedencia de los datos que se va a insertar en una consulta con un **ORDER BY** cláusula, los valores devueltos por la **NEXT VALUE FOR** será (función) se generan en el orden especificado por el **ORDER BY** cláusula.  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>Utilizar un objeto de secuencia con una cláusula OVER ORDER BY  
 El **NEXT VALUE FOR** función permite generar valores de secuencia ordenados aplicando la **sobre** cláusula para la **NEXT VALUE FOR** llamar. Mediante el uso de la **sobre** cláusula, un usuario se garantiza que los valores que se devuelven se generan en el orden de la **sobre** la cláusula **orden B**Y subcláusula. Las siguientes reglas adicionales se aplican cuando se usa el **NEXT VALUE FOR** funcionando con la **sobre** cláusula:  
  
-   Varias llamadas a la **NEXT VALUE FOR** función para el mismo generador de secuencias en una sola instrucción, todas debe utilizar el mismo **sobre** definición de la cláusula.  
  
-   Varias llamadas a la **NEXT VALUE FOR** función que referencia distintos generadores de secuencias en una sola instrucción pueden tener diferentes **sobre** definiciones de la cláusula.  
  
-   Un **sobre** cláusula que se aplica a la **NEXT VALUE FOR** función no admite la **PARTITION BY** subcláusula.  
  
-   Si todas las llamadas a la **NEXT VALUE FOR** funcionando en un **seleccione** instrucción especifica la **sobre** cláusula, un **ORDER BY** cláusula puede usarse en el **seleccione** instrucción.  
  
-   El **sobre** se permite la cláusula con el **NEXT VALUE FOR** funcionar cuando se utiliza en una **seleccione** instrucción o `INSERT … SELECT …` instrucción. El uso de la **sobre** cláusula con el **NEXT VALUE FOR** función no está permitida en **actualización** o **mezcla** instrucciones.  
  
-   Si otro proceso está teniendo acceso al objeto de secuencia a la vez, los números devueltos podrían tener lagunas.  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información acerca de las secuencias, consulte el [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) vista de catálogo.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere **actualización** permiso en el objeto de secuencia o el esquema de la secuencia. Para obtener un ejemplo de concesión de permisos, vea el ejemplo F más adelante en este tema.  
  
### <a name="ownership-chaining"></a>Encadenamiento de propiedad  
 Los objetos de secuencia son compatibles con el encadenamiento de propiedad. Si el objeto de secuencia tiene el mismo propietario que el procedimiento almacenado, desencadenador o tabla que hace la llamada (y un objeto de secuencia como restricción predeterminada), no se necesita ninguna comprobación de permiso en el objeto de secuencia. Si el objeto de secuencia no pertenece al mismo propietario que el procedimiento almacenado, desencadenador o tabla que hace la llamada, se requiere una comprobación de permiso en el objeto de secuencia.  
  
 Cuando el **NEXT VALUE FOR** función se utiliza como valor predeterminado en una tabla, los usuarios deben tener **insertar** permiso en la tabla, y **actualización** permiso en el objeto de secuencia , para insertar datos utilizando el valor predeterminado.  
  
-   Si la restricción predeterminada tiene el mismo propietario que el objeto de secuencia, no es necesario ningún permiso en el objeto de secuencia cuando se llama a la restricción predeterminada.  
  
-   Si la restricción predeterminada y el objeto de secuencia no son propiedad del mismo usuario, se necesitan permisos en el objeto de secuencia aunque la llamada se haga mediante la restricción predeterminada.  
  
### <a name="audit"></a>Auditar  
 Para auditar la **NEXT VALUE FOR** funcionar, supervise SCHEMA_OBJECT_ACCESS_GROUP.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos de secuencias de creación y uso de la **NEXT VALUE FOR** función para generar números de secuencia, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 En los siguientes ejemplos se utiliza una secuencia denominada `CountBy1` en un esquema denominado `Test`. Ejecute la siguiente instrucción para crear la secuencia `Test.CountBy1`. En los ejemplos C y E se utiliza la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], de modo que la secuencia `CountBy1` se cree en esa base de datos.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. Usar una secuencia en una instrucción SELECT  
 En el siguiente ejemplo se crea una secuencia denominada `CountBy1` que aumenta en uno cada vez que se utiliza.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. Establecer una variable en el siguiente valor de la secuencia  
 En el ejemplo siguiente se muestran tres maneras de establecer una variable en el siguiente valor de un número de secuencia.  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. Usar una secuencia con una función de ventana de categoría  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. Usar la función NEXT VALUE FOR en la definición de una restricción predeterminada  
 Mediante el **NEXT VALUE FOR** se admite la función en la definición de una restricción predeterminada. Para obtener un ejemplo del uso de **NEXT VALUE FOR** en un **CREATE TABLE** instrucción, vea el ejemplo C[números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md). En el siguiente ejemplo se utiliza `ALTER TABLE` para agregar una secuencia como valor predeterminado a una tabla actual.  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. Usar la función NEXT VALUE FOR en una instrucción INSERT  
 En el siguiente ejemplo se crea una tabla denominada `TestTable` y, a continuación, se utiliza la función `NEXT VALUE FOR` para insertar una fila.  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. Usar la función NEXT VALUE FOR con SELECT ... INTO  
 En el ejemplo siguiente se usa el `SELECT … INTO` instrucción para crear una tabla denominada `Production.NewLocation` y usa el `NEXT VALUE FOR` función para numerar cada fila.  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. Conceder permiso para ejecutar NEXT VALUE FOR  
 El siguiente ejemplo se concede **actualización** permiso a un usuario denominado `AdventureWorks\Larry` permiso para ejecutar `NEXT VALUE FOR` mediante el `Test.CounterSeq` secuencia.  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear secuencia de &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  


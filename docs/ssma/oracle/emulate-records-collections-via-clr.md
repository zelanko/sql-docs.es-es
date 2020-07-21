---
title: Emulación de registros y colecciones a través de CLR UDT
description: Explica cómo el SQL Server Migration Assistant (SSMA) para Oracle usa el SQL Server tipos de datos definidos por el usuario (UDT) de Common Language Runtime (CLR) para emular registros y recopilaciones de Oracle.
author: nahk-ivanov
ms.prod: sql
ms.technology: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 73991999cf0a6e7bd2c8cd541ec58a37d1f18f09
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779385"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>Emulación de registros y colecciones a través de CLR UDT

En este artículo se explica cómo el SQL Server Migration Assistant (SSMA) para Oracle usa el SQL Server tipos de datos definidos por el usuario (UDT) de Common Language Runtime (CLR) para emular registros y recopilaciones de Oracle.

## <a name="declaring-record-or-collection-types-and-variables"></a>Declarar tipos de registros o colecciones y variables

SSMA crea tres UDT basados en CLR:

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

El `CollectionIndexInt` tipo está diseñado para emular colecciones indizadas por un entero, como, `VARRAY` tablas anidadas y matrices asociativas basadas en claves enteras. El `CollectionIndexString` tipo se utiliza para las matrices asociativas indizadas por claves de caracteres. La funcionalidad del registro de Oracle está emulada por el `Record` tipo.

Todas las declaraciones de los tipos de registro o colección se convierten en esta declaración de Transact-SQL:

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

Este `<type definition>` es un texto descriptivo que identifica de forma única el tipo PL/SQL de origen.

Considere el ejemplo siguiente:

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

Cuando se convierte mediante SSMA, se convertirá en el siguiente código de Transact-SQL:

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

Aquí, como la `Manager` tabla está asociada a un índice numérico ( `INDEX BY PLS_INTEGER` ), la declaración de T-SQL correspondiente utilizada es de tipo `@CollectionIndexInt$TYPE` . Si la tabla estaba asociada a un índice de juego de caracteres, como `VARCHAR2` , la declaración de T-SQL correspondiente sería de tipo `@CollectionIndexString$TYPE` :

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

La funcionalidad de registro de Oracle solo se emula mediante el `Record` tipo.

Cada uno de los tipos, `CollectionIndexInt` , `CollectionIndexString` y `Record` , tiene una propiedad estática que `[Null]` devuelve una instancia vacía. `SetType`Se llama al método para recibir un objeto vacío de un tipo específico (como se muestra en el ejemplo anterior).

## <a name="constructor-call-conversions"></a>Conversiones de llamadas a constructores

La notación de constructor solo se puede usar para las tablas anidadas y `VARRAY` , por lo que todas las llamadas explícitas a constructores se convierten utilizando el `CollectionIndexInt` tipo. Las llamadas a constructores vacías se convierten mediante una `SetType` llamada invocada en una instancia null de `CollectionIndexInt` . La `[Null]` propiedad devuelve la instancia null. Si el constructor contiene una lista de elementos, se aplican secuencialmente llamadas a métodos especiales para agregar el valor a la colección.

Por ejemplo:

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>Referencia y asignación de elementos de registro y de colección

Cada uno de los UDT tiene un conjunto de métodos que trabajan con elementos de los distintos tipos de datos. Por ejemplo, el `SetDouble` método asigna un `float(53)` valor a record o Collection y `GetDouble` puede leer este valor. Esta es la lista completa de métodos:

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

Estos métodos se usan al hacer referencia o asignar un valor a un elemento de una colección o registro.

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

Al convertir instrucciones de asignación para colecciones multidimensionales o colecciones con elementos de registro, SSMA agrega los siguientes métodos para hacer referencia a un elemento primario dentro del método Set:

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

Por ejemplo, una colección de elementos de registro se crea de esta manera:

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>Métodos integrados de colección

SSMA usa los siguientes métodos UDT para emular los métodos integrados de las colecciones de PL/SQL.

Métodos de colección de Oracle | `CollectionIndexInt`y `CollectionIndexString` equivalente
--- | ---
COUNT | `Count returns int`
Delete | `RemoveAll() returns <UDT_type>`
ELIMINAR (n) | `Remove(@index int) returns <UDT_type>`
ELIMINAR (m, n) | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
ALLÁ | `Extend() returns <UDT_type>`
EXTEND (n) | `Extend() returns <UDT_type>`
EXTEND (n, i) | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | N/D
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM (n) | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>Operación de recopilación masiva

SSMA convierte `BULK COLLECT INTO` instrucciones en SQL Server `SELECT ... FOR XML PATH` instrucción, cuyo resultado se ajusta en una de las siguientes funciones:

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

La elección depende del tipo del objeto de destino. Estas funciones devuelven valores XML que se pueden analizar `CollectionIndexInt` mediante `CollectionIndexString` `Record` tipos y. Una `AssignData` función especial asigna una colección basada en XML al UDT.

SSMA reconoce tres tipos de `BULK COLLECT INTO` instrucciones.

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>La colección contiene elementos con tipos escalares y la `SELECT` lista contiene una columna

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>La colección contiene elementos con tipos de registro y la `SELECT` lista contiene una columna

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>La colección contiene elementos con el tipo escalar y la `SELECT` lista contiene varias columnas

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>SELECCIONAR registro

Cuando el resultado de la consulta de Oracle se guarda en una variable de registro de PL/SQL, tiene dos opciones dependiendo del valor de SSMA para **convertir registro como una lista de variables separadas** (disponible en el menú **herramientas** , **configuración del proyecto**y, a continuación, conversión **General**  ->  **Conversion**). Si el valor de esta opción es **sí** (valor predeterminado), SSMA no crea una instancia del tipo de registro. En su lugar, divide el registro en los campos constitutivos creando una variable de Transact-SQL independiente por cada campo de registro. Si el valor es **no**, se crea una instancia del registro y a cada campo se le asigna un valor mediante `Set` métodos.

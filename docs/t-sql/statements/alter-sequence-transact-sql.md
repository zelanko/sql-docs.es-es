---
title: SECUENCIA de ALTER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de7fd182be8fd79574c098a499a40a34d38aaf21
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Modifica los argumentos de un objeto de secuencia existente. Si se creó la secuencia con el **caché** opción, modificar la secuencia volverá a crear la memoria caché.  
  
 Objetos de secuencia se crean mediante el [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) instrucción. Las secuencias son valores enteros y pueden ser de cualquier tipo de datos que devuelva un entero. El tipo de datos no se puede cambiar mediante la instrucción ALTER SEQUENCE. Para cambiar el tipo de datos, quite y cree el objeto de secuencia.  
  
 Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según una especificación. Se generan nuevos valores de una secuencia llamando a la función NEXT VALUE FOR. Use **sp_sequence_get_range** para obtener varios números de secuencia a la vez. Para obtener información y situaciones que usa CREATE SEQUENCE, **sp_sequence_get_range**y la función NEXT VALUE FOR, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *sequence_name*  
 Especifica el nombre exclusivo por el que se conoce la secuencia en la base de datos. El tipo es **sysname**.  
  
 REINICIAR [WITH \<constante >]  
 El valor siguiente que el objeto de secuencia devolverá. Si se proporciona, el valor RESTART WITH debe ser un entero menor o igual que el valor máximo, y mayor o igual que el valor mínimo del objeto de secuencia. Si se omite el valor WITH, la numeración de la secuencia se reinicia basándose en las opciones de CREATE SEQUENCE iniciales.  
  
 INCREMENT BY \<constante >  
 El valor que se usa para aumentar (o disminuir si es negativo) el valor base del objeto de secuencia para cada llamada a la función NEXT VALUE FOR. Si el incremento es un valor negativo el objeto de secuencia es descendente, de lo contrario, es ascendente. El incremento no puede ser 0.  
  
 [MINVALUE \<constante > | NO MINVALUE]  
 Especifica los límites del objeto de secuencia. Si se especifica NO MINVALUE, se usa el valor mínimo posible del tipo de datos de la secuencia.  
  
 [MAXVALUE \<constante > | NO MAXVALUE  
 Especifica los límites del objeto de secuencia. Si se especifica NO MAXVALUE, se usa el valor máximo posible del tipo de datos de la secuencia.  
  
 [ CYCLE | NO CYCLE ]  
 Esta propiedad especifica si el objeto de secuencia se debe reiniciar desde el valor mínimo (o el valor máximo para los objetos de secuencia descendente) o se debe producir una excepción cuando se supera el valor mínimo o máximo.  
  
> [!NOTE]  
>  Después del recorrido, el valor siguiente es el valor mínimo o máximo, no el valor START VALUE de la secuencia.  
  
 [Caché [\<constante >] | SIN CACHÉ]  
 Aumenta el rendimiento de las aplicaciones que usan los objetos de secuencia minimizando el número de operaciones de E/S necesarias para conservar los valores generados en las tablas del sistema.  
  
 Para obtener más información sobre el comportamiento de la memoria caché, vea [CREATE SEQUENCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información acerca de cómo se crean las secuencias y cómo se administra la memoria caché la secuencia, vea [CREATE SEQUENCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 Los valores MINVALUE de las secuencias ascendentes y MAXVALUE de las secuencias descendentes no se pueden modificar con un valor que no permite el valor START WITH de la secuencia. Para cambiar el valor MINVALUE de una secuencia ascendente a un número mayor que el valor START WITH o cambiar el valor MAXVALUE de una secuencia descendente a un número menor que el valor START WITH, incluya el argumento RESTART WITH para reiniciar la secuencia en un punto deseado que esté dentro del rango mínimo y máximo.  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información sobre las secuencias, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere **ALTER** permiso en la secuencia o **ALTER** permiso en el esquema. Para conceder **ALTER** permiso en la secuencia, use **ALTER ON OBJECT** en el formato siguiente:  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 Se puede transferir la propiedad de un objeto de secuencia mediante el **ALTER AUTHORIZATION** instrucción.  
  
### <a name="audit"></a>Auditar  
 Para auditar **ALTER SEQUENCE**, supervisar el **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos de secuencias de creación y uso de la **NEXT VALUE FOR** función para generar números de secuencia, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="a-altering-a-sequence"></a>A. Modificar una secuencia  
 En el ejemplo siguiente se crea un esquema denominado Test y una secuencia denominada TestSeq utilizando la **int** tipo de datos, con un rango de 0 a 255. La secuencia se inicia con 125 y se incrementa en 25 cada vez que se genera un número. Dado que la secuencia está configurada para recorrerla en ciclo, cuando el valor supera el valor máximo de 200, se reinicia en el valor mínimo de 100.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 En el ejemplo siguiente se modifica la secuencia de TestSeq para que tenga un intervalo de 0 a 255. La secuencia reinicia la serie de la numeración con 100 y se incrementa en 50 cada vez que se genera un número.  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 Dado que no se cambiará la secuencia, el **NEXT VALUE FOR** función producirá un error cuando la secuencia supera los 200.  
  
### <a name="b-restarting-a-sequence"></a>B. Reiniciar una secuencia  
 En el ejemplo siguiente se crea una secuencia denominada CountBy1. La secuencia usa los valores predeterminados.  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 Para generar un valor de secuencia, el propietario ejecuta la siguiente instrucción:  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 El valor devuelto de -9.223.372.036.854.775.808 es el valor más bajo posible para el **bigint** tipo de datos. El propietario se da cuenta de que deseaba que la secuencia comenzase con 1, pero no indicó la **START WITH** cláusula cuando creó la secuencia. Para corregir este error, el propietario ejecuta la siguiente instrucción.  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 A continuación, el propietario ejecuta de nuevo la siguiente instrucción para generar un número de secuencia.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 El número es ahora 1, tal y como se esperaba.  
  
 La secuencia de CountBy1 se creó con el valor predeterminado de NO CYCLE para que deje de funcionar después de generar número 9.223.372.036.854.775.807. Las llamadas subsiguientes al objeto de secuencia devolverán el error 11728. La siguiente instrucción cambia el objeto de secuencia para que se recorra en ciclo y establece una memoria caché de 20.  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 Ahora, cuando el objeto de secuencia alcance 9.223.372.036.854.775.807 se recorrerá en ciclo y el número siguiente al recorrido del ciclo será el mínimo del tipo de datos, -9.223.372.036.854.775.808.  
  
 El propietario se da cuenta que la **bigint** tipo de datos usa 8 bytes cada vez que se utilice. El **int** tipo de datos que utiliza 4 bytes es suficiente. Sin embargo, no se puede modificar el tipo de datos de un objeto de secuencia. Para cambiar a un **int** tipo de datos, el propietario debe quitar el objeto de secuencia y volver a crear el objeto con el tipo de datos correcto.  
  
## <a name="see-also"></a>Vea también  
 [Crear secuencia de &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [Eliminar secuencia &#40; Transact-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [VALOR siguiente para &#40; Transact-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  


---
title: CREAR la secuencia (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a96d101c17f528b9ff14ca523e5dc41ada2f4c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Crea un objeto de secuencia y especifica sus propiedades. Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según la especificación con la que se creó la secuencia. La secuencia de valores numéricos se genera en orden ascendente o descendente en un intervalo definido y se puede configurar para reiniciarse (en un ciclo) cuando se agota. Las secuencias, a diferencia de las columnas de identidad, no se asocian a tablas concretas. Las aplicaciones hacen referencia a un objeto de secuencia para recuperar su valor siguiente. La aplicación controla la relación entre las secuencias y tablas. Las aplicaciones de usuario pueden hacer referencia un objeto de secuencia y coordinar los valores a través de varias filas y tablas.  
  
 A diferencia de los valores de las columnas de identidad que se generan cuando se insertan filas, una aplicación puede obtener el número de secuencia siguiente sin insertar la fila mediante una llamada a la [función NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md). Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para obtener varios números de secuencia a la vez.  
  
 Para obtener información sobre las funciones **CREATE SEQUENCE** y **NEXT VALUE FOR** y escenarios en los que se usan, vea [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *sequence_name*  
 Especifica el nombre exclusivo por el que se conoce la secuencia en la base de datos. El tipo es **sysname**.  
  
 [ built_in_integer_type | user-defined_integer_type  
 Una secuencia se puede definir como de cualquier tipo entero. Están permitidos los siguientes tipos  
  
-   **tinyint** -intervalo de 0 a 255  
  
-   **smallint** -intervalo de -32.768 a 32.767  
  
-   **int** -intervalo de -2.147.483.648 a 2.147.483.647  
  
-   **bigint** -intervalo de -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807  
  
-   **decimal** y **numérico** con una escala de 0.  
  
-   Cualquier tipo de datos definido por el usuario (tipo de alias) que esté basado en uno de los tipos permitidos.  
  
 Si no se proporciona ningún tipo de datos, el **bigint** tipo de datos se utiliza como el valor predeterminado.  
  
 START WITH \<constante >  
 Primer valor devuelto por el objeto de secuencia. El **iniciar** valor debe ser un valor menor o igual que el valor máximo y mayor o igual que el valor mínimo del objeto de secuencia. El valor inicial predeterminado para un nuevo objeto de secuencia es el valor mínimo para un objeto de secuencia ascendente y el valor máximo para uno descendente.  
  
 INCREMENT BY \<constante >  
 Valor que se usa para incrementar (o disminuir si es negativo) el valor del objeto de secuencia para cada llamada a la **NEXT VALUE FOR** (función). Si el incremento es un valor negativo, el objeto de secuencia es descendente; de lo contrario, es ascendente. El incremento no puede ser 0. El incremento predeterminado para un nuevo objeto de secuencia es 1.  
  
 [MINVALUE \<constante > | **NO MINVALUE** ]  
 Especifica los límites del objeto de secuencia. El valor mínimo predeterminado para un nuevo objeto de secuencia es el valor mínimo del tipo de datos del objeto de secuencia. Es cero para el tipo de datos **tinyint** y un número negativo para todos los demás.  
  
 [MAXVALUE \<constante > | **NO MAXVALUE**  
 Especifica los límites del objeto de secuencia. El valor máximo predeterminado para un nuevo objeto de secuencia es el valor máximo del tipo de datos del objeto de secuencia.  
  
 [CICLO | **NINGÚN CICLO** ]  
 Propiedad especifica si el objeto de secuencia se debería reiniciar desde el valor mínimo (o el máximo para los objetos de secuencia descendente) o producir una excepción cuando se supera el valor mínimo o máximo. La opción de ciclo predeterminado para los nuevos objetos de secuencia es NO CYCLE.  
  
 Tenga en cuenta que el ciclo se reinicia a partir del valor mínimo o máximo, no a partir del valor inicial.  
  
 [ **Caché** [\<constante >] | SIN CACHÉ]  
 Aumenta el rendimiento de las aplicaciones que utilizan objetos de secuencia al reducir el número de E/S de disco que se necesitan para generar números de secuencia. El valor predeterminado es CACHÉ.  
  
 Por ejemplo, si se elige un tamaño de caché de 50, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mantiene 50 valores individuales almacenados en memoria caché. Solo almacena en memoria caché el valor actual y el número de valores que se quedan en la memoria caché. Esto significa que la cantidad de memoria necesaria para almacenar la memoria caché siempre es dos veces la del tipo de datos del objeto de secuencia.  
  
> [!NOTE]  
>  Si la opción de memoria caché se habilita sin especificar un tamaño de caché, el Motor de base de datos seleccionará un tamaño. Sin embargo, los usuarios no deben confiar en que la selección sea coherente. [!INCLUDE[msCoName](../../includes/msconame-md.md)] puede cambiar el método de cálculo del tamaño de la memoria caché sin previo aviso.  
  
 Cuando se crean con el **caché** opción, un apagado inesperado (por ejemplo, un error de alimentación) puede provocar la pérdida de números de secuencia que permanecen en la memoria caché.  
  
## <a name="general-remarks"></a>Notas generales  
 Los números de secuencia se generan fuera del ámbito de la transacción actual. Se utilizan tanto si la transacción que usa el número de secuencia se confirma como si se revierte.  
  
### <a name="cache-management"></a>Administración de la memoria caché  
 Para mejorar el rendimiento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preasigna la cantidad de números de secuencia especificados por el **caché** argumento.  
  
 Por ejemplo, imagine que se crea una secuencia nueva con el valor inicial 1 y 15 como tamaño de caché. Cuando se necesita el primer valor, están disponibles los valores 1 a 15 de la memoria. El último valor almacenado en memoria caché (15) se escribe en las tablas del sistema del disco. Cuando se utilizan los 15 números, la solicitud siguiente (la del número 16) hará que la memoria caché sea asignada de nuevo. El nuevo último valor almacenado en memoria caché (30) se escribirá en las tablas del sistema.  
  
 Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se detiene después de utilizar 22 números, el siguiente número de secuencia en memoria (23) se escribe en las tablas del sistema, reemplazando el número almacenado previamente.  
  
 Una vez que SQL Server se reinicia y se necesita un número de secuencia, el número inicial se lee en las tablas del sistema (23). La cantidad de memoria caché de 15 números (23-38) se asigna a la memoria y el siguiente número que no está en memoria caché (39) se escribe en las tablas del sistema.  
  
 Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] deja de modo anómalo por un evento como un error de alimentación, la secuencia se reinicia con el número que se lee de tablas del sistema (39). Cualquier secuencia de números asignados a la memoria (pero nunca fueran solicitados por un usuario o aplicación) se pierden. Esta funcionalidad puede dejar huecos, pero garantiza que el mismo valor nunca se emitirán dos veces para un objeto de secuencia único, a menos que se define como **ciclo** o se reinicie manualmente.  
  
 La memoria caché se mantiene en memoria realizando el seguimiento del valor actual (el último valor emitido) y el número de valores que se dejan en la memoria caché. Por consiguiente, la cantidad de memoria que la memoria caché usa siempre es dos veces la del tipo de datos del objeto de secuencia.  
  
 Si el argumento de la memoria caché se establece en **NO CACHE** escribe el valor de la secuencia actual en las tablas del sistema cada vez que se usa una secuencia. Esto puede ralentizar el rendimiento al aumentar el acceso al disco, pero reduce la posibilidad de que se produzcan huecos imprevistos. Ya se sigan produciendo huecos si los números se solicitan con el **NEXT VALUE FOR** o **sp_sequence_get_range** funciones, pero, a continuación, los números no se utilizan o se utilizan en las transacciones no confirmadas.  
  
 Cuando se utiliza un objeto de secuencia del **caché** opción, si reinicia el objeto de secuencia, o modificar el **incremento**, **ciclo**, **MINVALUE**, **MAXVALUE**, o las propiedades de tamaño de caché, hará que la memoria caché se escriban en las tablas del sistema antes de que se produce el cambio. A continuación, la memoria caché vuelve a cargarse comenzando con el valor actual (es decir, no se salta ningún número). El cambio realizado en el tamaño de la memoria caché surte efecto de forma inmediata.  
  
 **Opción CACHE cuando existen valores almacenados en caché**  
  
 El siguiente proceso se produce cada vez que se solicita un objeto de secuencia para generar el siguiente valor para la **caché** opción si hay valores sin usar en la memoria caché en memoria para el objeto de secuencia.  
  
1.  Se calcula el valor siguiente para el objeto de secuencia.  
  
2.  El nuevo valor actual para el objeto de secuencia se actualiza en la memoria.  
  
3.  El valor calculado se devuelve a la instrucción que realiza la llamada.  
  
 **Opción de caché cuando se agota la memoria caché**  
  
 El siguiente proceso se produce cada vez que se solicita un objeto de secuencia para generar el siguiente valor para la **caché** opción si se ha agotado la memoria caché:  
  
1.  Se calcula el valor siguiente para el objeto de secuencia.  
  
2.  Se calcula el último valor para la nueva memoria caché.  
  
3.  Se bloquea la fila de la tabla del sistema para el objeto de secuencia y el valor calculado en el paso 2 (el último valor) se escribe en la tabla del sistema. Se activa un xevent agotado en caché para notificar al usuario el nuevo valor conservado.  
  
 **NINGUNA opción de caché**  
  
 El siguiente proceso se produce cada vez que se solicita un objeto de secuencia para generar el siguiente valor para la **NO CACHE** opción:  
  
1.  Se calcula el valor siguiente para el objeto de secuencia.  
  
2.  El nuevo valor actual para el objeto de secuencia se escribe en la tabla del sistema.  
  
3.  El valor calculado se devuelve a la instrucción que realiza la llamada.  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información sobre las secuencias, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso **CREATE SEQUENCE**, **ALTER**o **CONTROL** en el SCHEMA.  
  
-   Los miembros de db_owner y db_ddladmin funciones fijas de base de datos pueden crear, modificar y quitar objetos de secuencia.  
  
-   Los miembros de las funciones db_owner y db_datawriter funciones fijas de base de datos pueden actualizar objetos de secuencia haciendo que generen números.  
  
 En el ejemplo siguiente, se concede al usuario permiso de AdventureWorks\Larry para crear secuencias en el esquema de prueba.  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 Se puede transferir la propiedad de un objeto de secuencia mediante el uso de la **ALTER AUTHORIZATION** instrucción.  
  
 Si una secuencia utiliza un tipo de datos definido por el usuario, el creador de la secuencia debe tener el permiso REFERENCES en el tipo.  
  
### <a name="audit"></a>Auditar  
 Para auditar **CREATE SEQUENCE**, supervisar el **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos de cómo crear secuencias y utilizando la **NEXT VALUE FOR** función para generar números de secuencia, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 La mayoría de los ejemplos siguientes crea objetos de secuencia en un esquema denominado Test.  
  
 Para crear el esquema de prueba, ejecute la instrucción siguiente.  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. Crear una secuencia que se incremente en 1  
 En el siguiente ejemplo, Thierry crea una secuencia denominada CountBy1 que aumenta en uno cada vez que se utiliza.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. Crear una secuencia que se disminuya en 1  
 El ejemplo siguiente comienza en 0 y resta uno cada vez que se utiliza.  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. Crear una secuencia que se incremente en 5  
 El siguiente ejemplo crea una secuencia que se incrementa en 5 cada vez que se utiliza.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. Crear una secuencia que se inicia con un número designado  
 Después de importar una tabla, Thierry observa que el mayor número de identificación utilizado es 24.328. Thierry necesita una secuencia que generará números a partir de 24.329. El siguiente código crea una secuencia que comienza en 24.329 y se incrementa en 1.  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. Crear una secuencia utilizando los valores predeterminados  
 En el siguiente ejemplo se crea una secuencia mediante los valores predeterminados.  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 Ejecute la siguiente instrucción para ver las propiedades de la secuencia.  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 Una lista parcial del resultado demuestra los valores predeterminados.  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. Crear una secuencia con un tipo de datos concreto  
 En el ejemplo siguiente se crea una secuencia utilizando el **smallint** tipo de datos, con un intervalo de -32.768 a 32.767.  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. Crear una secuencia utilizando todos los argumentos  
 En el ejemplo siguiente se crea una secuencia denominada DecSeq utilizando la **decimal** tipo de datos, con un rango de 0 a 255. La secuencia se inicia con 125 y se incrementa en 25 cada vez que se genera un número. Dado que la secuencia se configura para recorrer en ciclo cuando el valor supera el valor máximo de 200, la secuencia se reinicia en el valor mínimo de 100.  
  
```  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 Ejecute la siguiente instrucción para ver el primer valor; la opción `START WITH` 125.  
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 Ejecute la instrucción tres veces más para devolver 150, 175 y 200.  
  
 Ejecute la instrucción para ver de nuevo cómo vuelve el valor inicial a la opción `MINVALUE` 100.  
  
 Ejecute el siguiente código para confirmar el tamaño de caché y ver el valor actual.  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Eliminar secuencia &#40; Transact-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [VALOR siguiente para &#40; Transact-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  


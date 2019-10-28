---
title: Solución de problemas de índices de hash para tablas optimizadas para memoria | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 16e3ab81700ca9fed1870a6a98d0aab704b2c1db
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909277"
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>Solución de problemas de índices de hash para tablas optimizadas para memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>Requisito previo  
  
Encontrará información de contexto importante para comprender este artículo en:  
  
- [Índices de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [Índices de hash de tablas con optimización para memoria](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>Números prácticos  
  
Cuando se crea un índice de hash para una tabla optimizada para memoria, se debe especificar el número de depósitos en el momento de la creación. En la mayoría de los casos, lo ideal es que el número de cubos esté entre 1 y 2 veces el número de valores distintos de la clave de índice. 

Sin embargo, aunque el **BUCKET_COUNT** esté moderadamente por debajo o por encima del rango preferido, es probable que el rendimiento del índice de hash sea tolerable o aceptable. Como mínimo, considere asignar al índice de hash un **BUCKET_COUNT** aproximadamente igual al número de filas que prevé que terminará teniendo la tabla optimizada para memoria.  
Suponga que la tabla en aumento tiene 2 000 000 filas, pero la predicción indica que dicha cantidad crecerá 10 veces hasta 20 000 000 filas. Comience por un número de cubos que sea 10 veces el número de filas de la tabla. Esto deja espacio para una mayor cantidad de filas.  
  
- Lo ideal es aumentar el número de cubos cuando la cantidad de filas alcanza el número de cubos inicial.  
- Aunque la cantidad de filas aumente hasta 5 veces más que el número de cubos, el rendimiento seguirá siendo bueno casi siempre.  
  
Suponga que un índice de hash tiene 10 000 000 valores de claves distintos.  
  
- Un número de cubos de 2 000 000 sería la menor cantidad que podría aceptar. El grado de degradación del rendimiento puede ser tolerable.  
  
## <a name="too-many-duplicate-values-in-the-index"></a>¿Demasiados valores duplicados en el índice?  
  
Si los valores de hash indizados tienen una alta tasa de duplicados, los depósitos de hash toleran cadenas más largas.  
  
Suponga que tiene la misma tabla SupportEvent del bloque de código anterior de la sintaxis de T-SQL. El código de T-SQL siguiente muestra cómo buscar y mostrar la proporción de *todos* los valores con respecto a los valores *únicos* :  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- Una proporción de 10,0 o superior significa que un tipo de índice de hash sería deficiente. Sopese la posibilidad de usar un índice no agrupado en su lugar.   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>Solución de problemas de número de cubos de índice de hash  
  
En esta sección se explica cómo resolver problemas relativos al número de cubos del índice de hash.  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>Supervisión de estadísticas de cadenas y depósitos vacíos  
  
Puede supervisar el mantenimiento estadístico de los índices de hash ejecutando la siguiente instrucción SELECT de T-SQL. SELECT usa la vista de administración de datos (DMV) denominada **sys.dm_db_xtp_hash_index_stats**.  
  
```sql
SELECT  
  QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
  i.name                   as [index],   
  h.total_bucket_count,  
  h.empty_bucket_count,  
    
  FLOOR((  
    CAST(h.empty_bucket_count as float) /  
      h.total_bucket_count) * 100)  
                            as [empty_bucket_percent],  
  h.avg_chain_length,   
  h.max_chain_length  
FROM  
        sys.dm_db_xtp_hash_index_stats  as h   
  JOIN sys.indexes                     as i  
          ON h.object_id = i.object_id  
          AND h.index_id  = i.index_id  
JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
JOIN sys.tables t on h.object_id=t.object_id
WHERE ia.type=1
ORDER BY [table], [index];  
```
  
Compare los resultados de SELECT con las siguientes directrices estadísticas:  
  
- Depósitos vacíos:  
  - 33 % es un buen valor de destino, pero un porcentaje mayor (incluso el 90 %) suele funcionar correctamente.  
  - Cuando el número de cubos es igual al número de valores de clave distintos, aproximadamente un 33 % de los cubos están vacíos.  
  - Un valor inferior al 10 % es demasiado bajo.  
- Cadenas dentro de cubos:  
  - Una longitud media de cadena de 1 es ideal en caso de que no haya valores de clave de índice duplicados. Las longitudes de cadena de hasta 10 suelen ser aceptables.  
  - Si la longitud promedio de la cadena es superior a 10 y el porcentaje de depósitos vacíos es superior al 10 %, los datos tienen tantos duplicados que es posible que un índice de hash no sea el tipo más adecuado.  
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>Demostración de cadenas y depósitos vacíos  
  
El siguiente bloque de código de T-SQL constituye un sencillo método de comprobar una instrucción `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. El bloque de código se completa en 1 minuto. Estas son las fases del código de bloque en cuestión:  
  
1. Crea una tabla optimizada para memoria que tiene algunos índices hash.  
2. Rellena la tabla con miles de filas.  
    A. Se usa un operador de módulo para configurar la tasa de valores duplicados en la columna StatusCode.  
    B. El bucle inserta 262,144 filas aproximadamente en un minuto.  
3. PRINT imprime un mensaje pidiéndole que ejecute la instrucción SELECT anterior en **sys.dm_db_xtp_hash_index_stats**.  

```sql
DROP TABLE IF EXISTS SalesOrder_Mem;  
go  
  
  
CREATE TABLE SalesOrder_Mem  
(  
  SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
  OrderSequence  int               NOT NULL,  
  OrderDate      datetime2(3)      NOT NULL,  
  StatusCode     tinyint           NOT NULL,  
  
  PRIMARY KEY NONCLUSTERED  
      HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
  
  INDEX ix_OrderSequence  
      HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
  
  INDEX ix_StatusCode  
      HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
  
  INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
)  
  WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
--------------------  
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
El bucle `INSERT` anterior hace lo siguiente:  
  
- Inserta valores únicos en el índice de clave principal y en *ix_OrderSequence*.  
- Inserta un par de cientos de miles de filas que solo representan 8 valores distintos para `StatusCode`. Por lo tanto, hay una alta tasa de duplicación de valores en el índice *ix_StatusCode*.  
  
Para solucionar problemas cuando el número de cubos no es óptimo, examine la salida siguiente de la instrucción SELECT en **sys.dm_db_xtp_hash_index_stats**. Para estos resultados, hemos agregado `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` a la instrucción SELECT que copiamos de la sección D.1.  
  
Los resultados de nuestra instrucción `SELECT` se muestran después del código, divididos artificialmente en dos tablas de resultados más estrechas para poder verlos mejor.  
  
- Estos son los resultados del *número de cubos*.  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
- Luego tenemos los resultados de *longitud de la cadena*.  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
Vamos a interpretar la tabla de resultados anterior para los tres índices de hash:  
  
*ix_StatusCode:*  
  
- El 50 % de los depósitos están vacíos, lo que es adecuado.  
- Sin embargo, el promedio de longitud de cadena es muy elevado (65 536).  
  - Esto indica una alta tasa de valores duplicados.  
  - Por consiguiente, el uso de un índice de hash no es adecuado en este caso. Se debe usar un índice no clúster en su lugar.  
  
*ix_OrderSequence:*  
  
- El 0 % de los depósitos están vacíos, lo que es demasiado bajo.  
- La longitud promedio de la cadena es 8, aunque todos los valores de este índice sean únicos.  
  - Por lo tanto, el número de cubos debe aumentarse para reducir el promedio de longitud de cadena a un valor más cercano a 2 o 3.  
- Como la clave de índice tiene 262 144 valores únicos, el número de cubos debe ser al menos 262 144.  
  - Si se espera un aumento futuro, el número de cubos debe ser superior.  
  
*Índice de clave principal (PK_SalesOrd_...):*  
  
- El 36 % de los depósitos están vacíos, lo que es adecuado.  
- El promedio de longitud de cadena es 1, lo que también es adecuado. No se requieren cambios.  
  
### <a name="balancing-the-trade-off"></a>Equilibrio de ventajas y desventajas  
  
Las cargas de trabajo de OLTP se centran en filas individuales. Los recorridos de tabla completos no suelen estar en la ruta crítica de rendimiento para cargas de trabajo de OLTP. Por lo tanto, las ventajas y desventajas que debe mantener en equilibrio están entre la **cantidad de uso de memoria** y el **rendimiento de las operaciones de inserción y pruebas de igualdad**.  
  
**Si el uso de memoria es la mayor preocupación:**  
  
- Elija un número de cubos cercano al número de registros de clave de índice.  
- El número de cubos no debería ser significativamente menor que el número de valores de clave de índice, puesto que esto afecta a la mayoría de las operaciones de DML así como al tiempo que lleva recuperar la base de datos después de reiniciar el servidor.  
  
**Si las pruebas de rendimiento de igualdad es la mayor preocupación:**  
  
- Un número mayor de cubos, de dos o tres veces el número de valores de índice únicos, es adecuado. Un número mayor significa:  
  - Recuperaciones más rápidas cuando se busca un valor específico.  
  - Mayor uso de memoria.  
  - Aumento del tiempo necesario para un examen completo del índice de hash.  
  

##  <a name="Additional_Reading"></a> Lecturas adicionales  
 [Índices de hash para tablas optimizadas para memoria](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [Índices no agrupados para tablas optimizadas para memoria](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  

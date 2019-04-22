---
title: Determinar el número correcto de depósitos para los índices Hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b79c0908f8639df869d01a8ff862afc5be77cb
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241963"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>Determinar el número correcto de depósitos para los índices hash
  Debe especificar un valor para el parámetro `BUCKET_COUNT` al crear la tabla optimizada para memoria. En este tema se hacen recomendaciones para determinar el valor adecuado para el parámetro `BUCKET_COUNT`. Si no puede determinar el número de cubos correcto, utilice un índice no clúster en su lugar.  Un valor incorrecto de `BUCKET_COUNT`, especialmente si es demasiado bajo, puede afectar significativamente el rendimiento de la carga de trabajo, así como afectar el tiempo de recuperación de la base de datos. Es mejor sobrestimar el número de cubos.  
  
 Las claves de índice duplicadas pueden reducir el rendimiento con un índice hash porque a las claves se les aplica el algoritmo hash en el mismo cubo, por lo que la cadena del cubo aumenta.  
  
 Para obtener más información sobre índices de hash no clúster, vea [Hash Indexes](hash-indexes.md) y [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Se asigna una tabla hash para cada índice de hash de una tabla optimizada para memoria. El tamaño de la tabla hash asignada para un índice especificado por el `BUCKET_COUNT` parámetro [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) o [CREATE TYPE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql). El número de cubos se redondeará internamente hasta la siguiente potencia de dos. Por ejemplo, especificar un número de cubos de 300.000 producirá un número real de cubos de 524.288.  
  
 Para ver vínculos a un artículo y vídeo en el número de cubos, consulte [Cómo determinar el número de cubos adecuado para índices de hash (OLTP en memoria)](https://www.mssqltips.com/sqlservertip/3104/determine-bucketcount-for-hash-indexes-for-sql-server-memory-optimized-tables/).  
  
## <a name="recommendations"></a>Recomendaciones  
 En la mayoría de los casos el número de cubos debe estar entre 1 y 2 veces el número de valores distintos de la clave de índice. Si la clave de índice contiene muchos valores duplicados, como promedio hay más de 10 filas por cada valor de clave de índice, utilice un índice no clúster en su lugar.  
  
 No podrá siempre predecir cuántos valores puede tener o tendrá una clave de índice determinada. El rendimiento debe ser aceptable si el valor de `BUCKET_COUNT` está en el intervalo de 5 veces el número real de valores de clave.  
  
 Para determinar el número de claves de índice único en los datos existentes, utilice las consultas similares a los siguientes ejemplos:  
  
### <a name="primary-key-and-unique-indexes"></a>Clave principal e índices únicos  
 Dado que el índice de clave principal es único, el número de valores distintos en la clave corresponde al número de filas de la tabla. Para una clave principal de ejemplo en (SalesOrderID, SalesOrderDetailID) de la tabla Sales.SalesOrderDetail de la base de datos AdventureWorks, ejecute la consulta siguiente para calcular el número de valores de clave principal distintos, que corresponde al número de filas de la tabla:  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 Esta consulta muestra un número de filas de 121.317. Use un número de cubos de 240.000 si el recuento de filas no va a cambiar significativamente. Use un número de cubos de 480.000 si se espera que el número de pedidos de la tabla se cuadruplique.  
  
### <a name="non-unique-indexes"></a>Índices no únicos  
 Para otros índices, por ejemplo un índice de varias columnas en (SpecialOfferID, ProductID), ejecute la consulta siguiente para determinar el número de valores de clave de índice único:  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 Esta consulta devuelve un recuento de clave de índice para (SpecialOfferID, ProductID) de 484, lo que indica que se debe usar un índice no clúster en lugar de un índice de hash no clúster.  
  
### <a name="determining-the-number-of-duplicates"></a>Determinar el número de duplicados  
 Para determinar el número promedio de valores duplicados para un valor de clave de índice, divida el número total de filas por el número de claves de índice único.  
  
 Para el índice de ejemplo en (SpecialOfferID, ProductID), esto da como resultado 121317 / 484 = 251. Esto significa que los valores de clave de índice tienen una media de 251 y por consiguiente debe ser un índice no clúster.  
  
## <a name="troubleshooting-the-bucket-count"></a>Solucionar problemas del número de depósitos  
 Para solucionar problemas de recuento de depósitos en tablas optimizadas para memoria, use [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql) para obtener estadísticas sobre los depósitos vacíos y la longitud de cadenas de fila. La siguiente consulta se puede utilizar para obtener estadísticas sobre todos los índices de hash de la base de datos actual. La consulta puede tardar varios minutos en ejecutarse si hay tablas de gran tamaño en la base de datos.  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 Los dos indicadores clave de estado de índice de hash son:  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* indica el número de cubos vacíos del índice de hash.  
  
 Si *empty_bucket_percent* es menos que el 10 por ciento, probablemente el número de cubos es demasiado bajo. Idealmente, *empty_bucket_percent* debe ser el 33 por ciento o mayor. Si el número de cubos coincide con el número de valores de clave de índice, cerca de 1/3 de los cubos está vacío, debido a la distribución de hash.  
  
 *avg_chain_length*  
 *avg_chain_length* indica el promedio de longitud de las cadenas de filas de los cubos de hash.  
  
 Si *avg_chain_length* es mayor que 10 y *empty_bucket_percent* es mayor del 10 por ciento, probablemente hay muchos valores de clave de índice duplicados y un índice no clúster resultaría más adecuado. Un promedio de longitud de cadena de 1 es ideal.  
  
 Existen dos factores que afectan la longitud de cadena:  
  
1.  Duplicados: todas las filas duplicadas forman parte de la misma cadena del índice hash.  
  
2.  Varios valores de clave asignados al mismo cubo. Cuanto menor sea el número de cubos, más cubos tendrán varios valores asignados.  
  
 Por ejemplo, considere la tabla y el script siguientes para insertar filas de ejemplo de la tabla:  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 El script inserta 262.144 filas en la tabla. Inserta valores únicos en el índice de clave principal y en IX_OrderSequence. Inserta muchos valores duplicados en el índice IX_Status: el script genera solo 8 valores distintos.  
  
 El resultado de la consulta de la solución de problemas de BUCKET_COUNT es el siguiente:  
  
|nombre de índice|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 Considere los tres índices de hash en esta tabla:  
  
-   IX_Status: 50 por ciento de los depósitos están vacíos, lo que es bueno. Sin embargo, el promedio de longitud de cadena es muy elevado (65.536). Esto indica un gran número de valores duplicados. Por consiguiente, el uso de un índice de hash no clúster no es adecuado en este caso. Se debe usar un índice no clúster en su lugar.  
  
-   IX_OrderSequence: 0 por ciento de los depósitos están vacíos, que es demasiado bajo. Además, el promedio de longitud de cadena es 8. Como los valores de este índice son únicos, esto significa que por término medio están asignados 8 valores a cada cubo. El número de cubos se debe aumentar. Como la clave de índice tiene 262.144 valores únicos, el número de cubos debe ser al menos 262.144. Si se espera un aumento futuro, el número debe ser superior.  
  
-   Índice de clave principal (PK__SalesOrder...): 36 por ciento de los depósitos están vacíos, lo que es bueno. Además el promedio de longitud de cadena es 1, que también es bueno. No es necesario ningún cambio.  
  
 Para obtener más información sobre problemas de solución de problemas con los índices de hash optimizados para memoria, vea [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md).  
  
## <a name="detailed-considerations-for-further-optimization"></a>Consideraciones detalladas de optimización adicional  
 Esta sección describe las consideraciones adicionales para optimizar el número de cubos.  
  
 Para obtener el mejor rendimiento de los índices de hash, equilibre la cantidad de memoria asignada a la tabla hash y el número de valores distintos en la clave de índice. Hay también un equilibrio entre el rendimiento de las búsquedas de puntos y los recorridos de tablas:  
  
-   Cuanto mayor sea el valor de número de cubos, más cubos vacíos habrá en el índice. Esto tiene un impacto en la utilización de memoria (8 bytes por cada cubo) y en el rendimiento de los recorridos de tablas, ya que cada cubo se examina como parte de un recorrido de tabla.  
  
-   Cuanto menor es el número de cubos, más valores se asignan a un único cubo. Esto reduce el rendimiento de las inserciones y las búsquedas de puntos, porque [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede necesitar recorrer varios valores en un único cubo para encontrar el valor especificado por el predicado de búsqueda.  
  
 Si el número de cubos es significativamente menor que el número de claves de índice único, se asignarán muchos valores a cada cubo. Esto disminuye el rendimiento de la mayoría de las operaciones DML, especialmente para las búsquedas de punto (búsquedas de claves de índice individuales) y para las operaciones de inserción. Por ejemplo, es posible que observe poco rendimiento de las consultas SELECT y de las operaciones UPDATE y DELETE con predicados de igualdad que se corresponden con las columnas de clave de índice en la cláusula WHERE. Un número inferior de depósitos afectará también el tiempo de recuperación de la base de datos, dado que se vuelven a crear los índices durante el inicio de la base de datos.  
  
### <a name="duplicate-index-key-values"></a>Valores de clave de índice duplicados  
 Los valores duplicados pueden aumentar el impacto en el rendimiento de las colisiones de valores hash. No suele ser un problema si cada clave de índice tiene un número bajo de duplicados. Pero puede ser un problema si la discrepancia entre el número de claves de índice único y el número de filas de las tablas se vuelve muy grande.  
  
 Todas las filas con la misma clave de índice entrarán en la misma cadena de duplicados. Si hay varias claves de índice en el mismo cubo debido a una colisión de hash, las exploraciones de índice tienen que examinar siempre la cadena completa de duplicados para el primer valor con el fin de poder ubicar la primera fila correspondiente al segundo valor. Las claves duplicadas también dificultan que la recolección de elementos no utilizados encuentre la fila. Por ejemplo, si hay 1.000 duplicados para cualquier clave y se elimina una de las filas, el recolector de elementos no utilizados debe examinar la cadena de 1.000 duplicados para desvincular la fila del índice. Esto es cierto incluso aunque la consulta que encontró la eliminación utilizara un índice más eficaz (un índice de clave principal) para encontrar la fila, ya que el recolector de elementos no utilizados debe desvincular desde cada índice.  
  
 Para los índices hash, hay dos formas de reducir el trabajo debido a valores de clave de índice duplicados:  
  
-   Use un índice no clúster en su lugar. Puede reducir los duplicados si agrega columnas a la clave de índice sin necesidad de hacer cambios en la aplicación.  
  
-   Especifique un número muy alto de cubos para el índice. Por ejemplo, 20 a 100 veces el número de claves de índice único. Esto reducirá las colisiones de hash.  
  
### <a name="small-tables"></a>Tablas pequeñas  
 Para tablas más pequeñas, el uso de memoria no suele ser un problema, puesto que el tamaño del índice será pequeño en comparación con el tamaño total de la base de datos.  
  
 Ahora debe tomar una decisión basada en el tipo de rendimiento que desea:  
  
-   Si las operaciones de rendimiento crítico en el índice son fundamentalmente búsquedas de puntos u operaciones de inserción, sería adecuado un número mayor de cubos para reducir la probabilidad de colisiones de valores hash. Tres veces el número de filas o incluso más sería la mejor opción.  
  
-   Si las exploraciones completas de índice son las predominantes de rendimiento crítico, use un número de cubos cercano al número real de valores de clave de índice.  
  
### <a name="big-tables"></a>Tablas grandes  
 Para las tablas grandes, el uso de memoria podría llegar a ser un problema. Por ejemplo, con una tabla de 250 millones de filas que tiene 4 índices de hash, cada uno con un número de depósitos de mil millones, la sobrecarga de las tablas hash es 4 índices * mil millones de 1 depósitos \* 8 bytes = 32 gigabytes de uso de memoria. Al elegir un número de cubos de 250 millones para cada uno de los índices, la sobrecarga total de las tablas hash será de 8 gigabytes. Tenga en cuenta que esto es además de los 8 bytes del uso de memoria de cada índice agrega a cada fila individual, que es 8 GB en este escenario (4 índices \* 8 bytes \* 250 millones de filas).  
  
 Las exploraciones de tabla completas no están generalmente en la ruta de acceso de rendimiento crítico para las cargas de trabajo de OLTP. Por consiguiente, la elección está entre el uso de memoria frente al rendimiento de operaciones de búsqueda de puntos e inserción:  
  
-   Si la utilización de memoria es un problema, elija un número de cubos cercano al número de valores de clave de índice. El número de cubos no debería ser significativamente menor que el número de valores de clave de índice, puesto que esto afecta a la mayoría de las operaciones de DML así como al tiempo que lleva recuperar la base de datos después de reiniciar el servidor.  
  
-   Al optimizar el rendimiento de las búsquedas de puntos, un número mayor de cubos de dos o incluso tres veces el número de valores de índice único sería adecuado. Un número mayor de cubos significaría una mayor uso de memoria y un incremento del tiempo necesario para una exploración completa del índice.  
  
## <a name="see-also"></a>Vea también  
 [Índices de las tablas con optimización para memoria](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  

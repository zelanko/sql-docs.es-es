---
title: ALTER DATABASE (Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b17fcc15be4c8faf496c469bb1e46fe2c6d42012
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550496"
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Modifica las opciones de tamaño máximo de la base de datos para las tablas replicadas, tablas distribuidas y el registro de transacciones en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use esta instrucción para administrar las asignaciones de espacio de disco para una base de datos a medida que aumenta o disminuye de tamaño. En el tema también se describe la sintaxis relacionada con la configuración de opciones de base de datos en Almacenamiento de datos paralelos. 
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF } 
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos que se va a modificar. Para mostrar una lista de bases de datos en el dispositivo, use [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 AUTOGROW = { ON | OFF }  
 Actualiza la opción AUTOGROW. Cuando AUTOGROW es ON, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] aumenta automáticamente el espacio asignado para las tablas replicadas, tablas distribuidas y el registro de transacciones según sea necesario para adecuarse al crecimiento de los requisitos de almacenamiento. Cuando AUTOGROW es OFF, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] devuelve un error si las tablas replicadas, tablas distribuidas o el registro de transacciones supera la configuración de tamaño máximo.  
  
 REPLICATED_SIZE = *tamaño* [GB]  
 Especifica el nuevo tamaño máximo en gigabytes por nodo de ejecución para almacenar todas las tablas replicadas en la base de datos que se va a modificar. Si tiene planeado el espacio de almacenamiento del dispositivo, debe multiplicar REPLICATED_SIZE por el número de nodos de ejecución en el dispositivo.  
  
 DISTRIBUTED_SIZE = *tamaño* [GB]  
 Especifica el nuevo tamaño máximo en gigabytes por base de datos para almacenar todas las tablas distribuidas de la base de datos que se va a modificar. El tamaño se distribuye entre todos los nodos de ejecución en el dispositivo.  
  
 LOG_SIZE = *tamaño* [GB]  
 Especifica el nuevo tamaño máximo en gigabytes por base de datos para almacenar todas los registros de transacciones de la base de datos que se va a modificar. El tamaño se distribuye entre todos los nodos de ejecución en el dispositivo.  
  
 ENCRYPTION { ON | OFF }  
 Establece que se cifre (ON) o no se cifre (OFF) la base de datos. Solo se puede configurar el cifrado para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cuando [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) se haya establecido en **1**. Se debe crear una clave de cifrado de base de datos antes de poder configurar el cifrado de datos transparente. Para obtener más información sobre el cifrado de bases de datos, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

 SET AUTO_CREATE_STATISTICS { ON | OFF } Cuando se activa la opción automática de creación de estadísticas, AUTO_CREATE_STATISTICS, el optimizador de consultas crea las estadísticas en columnas individuales en el predicado de consulta, según sea necesario, para mejorar las estimaciones de cardinalidad para el plan de consulta. Estas estadísticas de columna única se crean en las columnas que aún no tienen un histograma en un objeto de estadísticas existente.

 El valor predeterminado es ON para las bases de datos creadas después de actualizar a AU7. El valor predeterminado es OFF para las bases de datos creadas antes de la actualización. 

 Para obtener más información sobre las estadísticas, vea [Estadísticas](/sql/relational-databases/statistics/statistics).

 SET AUTO_UPDATE_STATISTICS { ON | OFF } Cuando se activa la opción automática de actualización de estadísticas, AUTO_UPDATE_STATISTICS, el optimizador de consultas determina cuándo es posible que las estadísticas queden obsoletas y las actualiza cuando una consulta las usa. Las estadísticas se vuelven obsoletas después de que las operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indexada. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

 El valor predeterminado es ON para las bases de datos creadas después de actualizar a AU7. El valor predeterminado es OFF para las bases de datos creadas antes de la actualización. 

 Para obtener más información sobre las estadísticas, vea [Estadísticas](/sql/relational-databases/statistics/statistics).


 SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } La opción de actualización asincrónica de estadísticas, AUTO_UPDATE_STATISTICS_ASYNC, determina si el optimizador de consultas usa actualizaciones de estadísticas sincrónicas o asincrónicas. La opción AUTO_UPDATE_STATISTICS_ASYNC se aplica a los objetos de estadística creados para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS.

 El valor predeterminado es ON para las bases de datos creadas después de actualizar a AU7. El valor predeterminado es OFF para las bases de datos creadas antes de la actualización. 

 Para obtener más información sobre las estadísticas, vea [Estadísticas](/sql/relational-databases/statistics/statistics).

  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
## <a name="error-messages"></a>mensajes de error
Si se deshabilitan las estadísticas automáticas y se intenta modificar la configuración de las estadísticas, PDW genera el error "Esta opción no se admite en PDW". El administrador del sistema puede habilitar las estadísticas automáticas si habilita el modificador de características [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md).

## <a name="general-remarks"></a>Notas generales  
 Los valores para REPLICATED_SIZE, DISTRIBUTED_SIZE y LOG_SIZE pueden ser mayor que, igual o menor que los valores actuales de la base de datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Las operaciones de crecimiento y reducción son aproximadas. Los tamaños reales resultantes pueden variar con respecto a los parámetros de tamaño.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no ejecuta la instrucción ALTER DATABASE como una operación atómica. Si la instrucción se anula durante la ejecución, se conservarán los cambios que ya se han producido.  

La configuración de las estadísticas solo funcionará si el administrador ha habilitado las estadísticas automáticas.  Si es un administrador, use el modificador de características [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) para habilitar o deshabilitar las estadísticas automáticas. 
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Toma un bloqueo compartido en el objeto DATABASE. No se puede modificar una base de datos que está en uso por otro usuario para operaciones lectura o escritura. Esto incluye las sesiones que han emitido una instrucción [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) en la base de datos.  
  
## <a name="performance"></a>Rendimiento  
 Reducir una base de datos puede consumir mucho tiempo y recursos del sistema, en función del tamaño de los datos reales en la base de datos y la cantidad de fragmentación del disco. Por ejemplo, reducir una base de datos puede tardar varias horas o más.  
  
## <a name="determining-encryption-progress"></a>Determinar el progreso del cifrado  
 Use la consulta siguiente para determinar el progreso del cifrado de datos transparente de base de datos como un porcentaje:  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 Para obtener un ejemplo completo en el que se muestran todos los pasos en la implementación de TDE, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Modificación de la configuración de AUTOGROW  
 Establezca AUTOGROW en ON para la base de datos `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Modificación del almacenamiento máximo para las tablas replicadas  
 En el ejemplo siguiente se establece el límite de almacenamiento de tablas replicadas en 1 GB para la base de datos `CustomerSales`. Este es el límite de almacenamiento por nodo de ejecución.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Modificación del almacenamiento máximo para las tablas distribuidas  
 En el ejemplo siguiente se establece el límite de almacenamiento de distribuidas replicadas en 1000 GB (un terabyte) para la base de datos `CustomerSales`. Este es el límite de almacenamiento combinado en todo el dispositivo para todos los nodos de ejecución, no el límite de almacenamiento por nodo de ejecución.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Modificación del almacenamiento máximo para el registro de transacciones  
 En el ejemplo siguiente se actualiza la base de datos `CustomerSales` para que tenga un tamaño máximo de registro de transacciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 10 GB para el dispositivo.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  

### <a name="e-check-for-current-statistics-values"></a>E. Comprobación de los valores de estadísticas actuales

La consulta siguiente devuelve los valores actuales de las estadísticas para todas las bases de datos. El valor 1 significa que la característica está activada, y 0 que está desactivada.

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```
### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. Habilitación de estadísticas de creación y actualización automáticas para una base de datos
Use la instrucción siguiente para habilitar las estadísticas de creación y actualización de manera automática y asincrónica para la base de datos, CustomerSales.  Esto crea y actualiza las estadísticas de columna única según sea necesario para crear planes de consulta de alta calidad.

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON; 
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```
  
## <a name="see-also"></a>Ver también  
 [CREATE DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  

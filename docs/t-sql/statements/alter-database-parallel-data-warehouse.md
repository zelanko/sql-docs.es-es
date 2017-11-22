---
title: ALTER DATABASE (almacenamiento de datos en paralelo) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 522f8c8404e80943e093ebeb0a56698fa790b6c9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="alter-database-parallel-data-warehouse"></a>Modificar base de datos (almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Modifica las opciones de tamaño máximo de la base de datos para las tablas replicadas, tablas distribuidas y el registro de transacciones en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use esta instrucción para administrar las asignaciones de espacio de disco para una base de datos a medida que aumenta o disminuye de tamaño.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 El nombre de la base de datos a modificarse. Para mostrar una lista de bases de datos en el dispositivo, utilice [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 CRECIMIENTO AUTOMÁTICO = {ON | {OFF}  
 Actualiza la opción de crecimiento automático. Cuando el crecimiento automático está activado, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] aumenta automáticamente el espacio asignado para las tablas replicadas, tablas distribuidas y el registro de transacciones según sea necesario para adecuarse al crecimiento de los requisitos de almacenamiento. Cuando el crecimiento automático está desactivado, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] devuelve un error si replica tablas, distribuida en tablas o el registro de transacciones supera el tamaño máximo.  
  
 REPLICATED_SIZE = *tamaño* [GB]  
 Especifica el nuevo gigabytes máximos por nodo de proceso para almacenar todas las tablas replicadas en la base de datos que se va a modificar. Si tiene previsto para el espacio de almacenamiento del dispositivo, debe multiplicar REPLICATED_SIZE por el número de nodos de proceso en el dispositivo.  
  
 DISTRIBUTED_SIZE = *tamaño* [GB]  
 Especifica el nuevo gigabytes máximos por base de datos para almacenar todas las tablas distribuidas en la base de datos que se va a modificar. El tamaño se distribuye entre todos los nodos de proceso en el dispositivo.  
  
 LOG_SIZE = *tamaño* [GB]  
 Especifica el nuevo gigabytes máximos por base de datos para almacenar todos los registros de transacciones en la base de datos que se va a modificar. El tamaño se distribuye entre todos los nodos de proceso en el dispositivo.  
  
 CIFRADO {ON | {OFF}  
 Establece que se cifre (ON) o no se cifre (OFF) la base de datos. Cifrado solo puede configurarse para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cuando [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) se ha establecido en **1**. Una clave de cifrado de base de datos debe crearse antes de que se puede configurar el cifrado de datos transparente. Para obtener más información acerca del cifrado de base de datos, vea [cifrado de datos transparente &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la base de datos.  
  
## <a name="general-remarks"></a>Notas generales  
 Los valores para REPLICATED_SIZE, DISTRIBUTED_SIZE y LOG_SIZE pueden ser mayor que, igual o menor que los valores actuales de la base de datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Crecimiento y las operaciones de reducción son aproximadas. El tamaño real resultante puede variar desde los parámetros de tamaño.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no lleva a cabo la instrucción ALTER DATABASE como una operación atómica. Si la instrucción se anuló durante la ejecución, seguirá siendo cambios que ya se han producido.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Toma un bloqueo compartido en el objeto de base de datos. No se puede modificar una base de datos que está en uso por otro usuario para leer o escribir. Esto incluye las sesiones que han emitido un [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) instrucción en la base de datos.  
  
## <a name="performance"></a>Rendimiento  
 Reducir una base de datos puede tardar una gran cantidad de tiempo y recursos del sistema, dependiendo del tamaño de los datos reales de la base de datos y la cantidad de fragmentación de disco. Por ejemplo, reducir una base de datos puede tardar varias horas o más.  
  
## <a name="determining-encryption-progress"></a>Determinar el progreso del cifrado  
 Utilice la siguiente consulta para determinar el progreso del cifrado de datos transparente de base de datos como un porcentaje:  
  
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
  
 Para obtener un ejemplo completo que muestra todos los pasos en la implementación de TDE, vea [cifrado de datos transparente &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Modificar la configuración de crecimiento automático  
 Establezca el crecimiento automático en ON para la base de datos `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Modificar el máximo de almacenamiento para las tablas replicadas  
 En el ejemplo siguiente se establece el límite de almacenamiento de tabla replicada a 1 GB para la base de datos `CustomerSales`. Este es el límite de almacenamiento por nodo de proceso.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Modificar el máximo almacenamiento para tablas distribuidas  
 En el ejemplo siguiente se establece el límite de almacenamiento de tabla distribuida en 1000 GB (un terabyte) para la base de datos `CustomerSales`. Este es el límite de almacenamiento combinado en el dispositivo para todos los nodos de proceso, no el límite de almacenamiento por nodo de proceso.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Modificar el almacenamiento máximo para el registro de transacciones  
 En el ejemplo siguiente se actualiza la base de datos `CustomerSales` a tener un máximo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 10 GB de tamaño de registro de transacciones para el dispositivo.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear base de datos &#40; Almacenamiento de datos en paralelo &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  

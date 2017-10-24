---
title: Crear base de datos (almacenamiento de datos en paralelo) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52a55d6c275388e03e3f7be09d265a3b918f583f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-parallel-data-warehouse"></a>Crear base de datos (almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Crea una nueva base de datos en un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo. Use esta instrucción para crear todos los archivos asociados con una base de datos del dispositivo y para establecer las opciones de crecimiento automático para las tablas de base de datos y registro de transacciones y el tamaño máximo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 El nombre de la nueva base de datos. Para obtener más información sobre los nombres permitidos de la base de datos, vea "Nombres reservados de base de datos" y "Reglas de nomenclatura de objetos" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 CRECIMIENTO AUTOMÁTICO = ON | **OFF**  
 Especifica si el *replicated_size*, *distributed_size*, y *log_size* parámetros para esta base de datos crecerán automáticamente según sea necesario más allá de sus especificado tamaños. Valor predeterminado es **OFF**.  
  
 Si el crecimiento automático está activado, *replicated_size*, *distributed_size*, y *log_size* aumentará a medida que se requiere (no en bloques del tamaño inicial especificado) con cada inserción de datos actualización, o a otra acción que requiere más almacenamiento que ya se ha asignado.  
  
 Si el crecimiento automático está desactivado, el tamaño no crece automáticamente. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]se devolverá un error al intentar realizar una acción que requiere *replicated_size*, *distributed_size*, o *log_size* crezca más allá de su valor especificado.  
  
 Crecimiento automático es ON para todos los tamaños o OFF para todos los tamaños. Por ejemplo, no es posible establecer ON de crecimiento automático para *log_size*, pero no la estableció *replicated_size*.  
  
 *replicated_size* [GB]  
 Un número positivo. Establece el tamaño (en gigabytes de entero o decimal) para el espacio total asignado a las tablas replicadas y los datos correspondientes *en cada nodo de ejecución*. Para los valores mínimo y máximo *replicated_size* requisitos, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si el crecimiento automático está activado, se permitirá que las tablas replicadas crezca más allá de este límite.  
  
 Si el crecimiento automático está desactivado, se devolverá un error si un usuario intenta crear una nueva tabla replicada, insertar datos en una existente que se replican de tabla, o actualización una existente tabla replicada de una manera que podría aumentar el tamaño más allá de *replicated_size*.  
  
 *distributed_size* [GB]  
 Un número positivo. El tamaño, en gigabytes de entero o decimal, para el espacio total asignado a tablas distribuidas (y los datos correspondientes) *en el dispositivo*. Para los valores mínimo y máximo *distributed_size* requisitos, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si el crecimiento automático está activado, se permitirá tablas distribuidas crezca más allá de este límite.  
  
 Si el crecimiento automático está desactivado, se devolverá un error si un usuario intenta crear una nueva tabla distribuida, insertar datos en una existente que se distribuyen de la tabla, o actualizar una tabla existente distribuida de manera que podría aumentar el tamaño más allá de *distributed_size* .  
  
 *log_size* [GB]  
 Un número positivo. El tamaño (en gigabytes de entero o decimal) del registro de transacciones *en el dispositivo*.  
  
 Para los valores mínimo y máximo *log_size* requisitos, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si el crecimiento automático está activado, se permite el archivo de registro crezca más allá de este límite. Use la [DBCC SHRINKLOG (almacenamiento de datos de SQL Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) instrucción para reducir el tamaño de los archivos de registro a su tamaño original.  
  
 Si el crecimiento automático está desactivado, se devolverá un error al usuario para cualquier acción que se aumente el tamaño de registro en un nodo de proceso individual más allá de *log_size*.  
  
## <a name="permissions"></a>Permissions  
 Requiere la **CREATE ANY DATABASE** permiso en la base de datos maestra o la pertenencia del **sysadmin** rol fijo de servidor.  
  
 En el ejemplo siguiente se proporciona el permiso para crear una base de datos al usuario de base de datos Fay.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>Notas generales  
 Las bases de datos se crean con el nivel de compatibilidad de base de datos 120, que es la compatibilidad de niveles de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Esto garantiza que la base de datos podrá usar toda la [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] funcionalidad que usa PDW.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se permite la instrucción CREATE DATABASE en una transacción explícita. Para obtener más información, consulte [instrucciones](../../t-sql/statements/statements.md).  
  
 Para obtener información sobre las restricciones mínimas y máxima en las bases de datos, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 En el momento en que se crea una base de datos, debe haber suficiente espacio libre disponible *en cada nodo de proceso* para asignar el total combinado de los tamaños siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la base de datos con tablas el tamaño de *replicated_table_size*.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la base de datos con tablas el tamaño de (*distributed_table_size* / número de nodos de proceso).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]registra el tamaño de (*log_size* / número de nodos de proceso).  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto de base de datos.  
  
## <a name="metadata"></a>Metadatos  
 Después de esta operación se realiza correctamente, una entrada para esta base de datos aparecerá en el [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)vistas de metadatos.  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. Ejemplos de creación de base de datos básicos  
 En el ejemplo siguiente se crea la base de datos `mytest` con una asignación de almacenamiento de 100 GB por nodo de proceso para las tablas replicadas, 500 GB por dispositivo para tablas distribuidas y 100 GB por dispositivo para el registro de transacciones. En este ejemplo, el crecimiento automático está desactivado de forma predeterminada.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 En el ejemplo siguiente se crea la base de datos `mytest` con los mismos parámetros que el anterior, excepto que AUTOGROW está activado. Esto permite que la base de datos crezca fuera de los parámetros de ajuste de tamaño especificado.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Crear una base de datos con tamaños de gigabyte parcial  
 En el ejemplo siguiente se crea la base de datos `mytest`, con el crecimiento automático desactivado, una asignación de almacenamiento de 1,5 GB por nodo de proceso para las tablas replicadas, 5,25 GB por dispositivo para tablas distribuidas y 10 GB por dispositivo para el registro de transacciones.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40; Almacenamiento de datos en paralelo &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  


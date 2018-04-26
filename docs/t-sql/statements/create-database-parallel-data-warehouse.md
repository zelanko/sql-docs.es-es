---
title: CREATE DATABASE (Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ed767a4acd2dbe4b202e94ed054da46810e14a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE (Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Crea una base de datos en un dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use esta instrucción para crear todos los archivos asociados con una base de datos del dispositivo y para establecer las opciones de crecimiento automático y de tamaño máximo de las tablas de base de datos y del registro de transacciones.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 El nombre de la nueva base de datos. Para más información sobre los nombres de base de datos permitidos, vea las secciones sobre las reglas de nomenclatura de objetos y sobre los nombres reservados de base de datos en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 AUTOGROW = ON | **OFF**  
 Especifica si los parámetros *replicated_size*, *distributed_size* y *log_size* de esta base de datos van a crecer automáticamente según sea necesario y más allá de sus tamaños establecidos. El valor predeterminado es **OFF**.  
  
 Si AUTOGROW se establece en ON, *replicated_size*, *distributed_size* y *log_size* aumentarán según sea necesario (no en bloques con el tamaño inicial especificado) con cada inserción de datos, actualización u otra acción que requiera más almacenamiento del que ya hay asignado.  
  
 Si AUTOGROW se establece en OFF, el tamaño no aumentará automáticamente. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] devolverá un error si se intenta realizar una acción que requiera que *replicated_size*, *distributed_size* o *log_size* aumenten por encima de su valor especificado.  
  
 AUTOGROW se establece en ON o en OFF invariablemente para todos los tamaños. Por ejemplo, no es posible establecer AUTOGROW en ON para *log_size* y no establecerlo para *replicated_size*.  
  
 *replicated_size* [ GB ]  
 Un número positivo. Establece el tamaño (en gigabytes en forma de número entero o con decimales) del espacio total asignado a las tablas replicadas y a los datos correspondientes *en cada nodo de ejecución*. Para conocer los requisitos mínimos y máximos de *replicated_size*, vea la sección sobre valores mínimos y máximos de la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si AUTOGROW está establecido en ON, las tablas replicadas podrán crecer más allá de este límite.  
  
 Si AUTOGROW está establecido en OFF, se devolverá un error si un usuario intenta crear una tabla replicada, insertar datos en una tabla replicada ya existente o actualizar una tabla replicada ya existente de forma que pueda aumentar el tamaño más allá de *replicated_size*.  
  
 *distributed_size* [ GB ]  
 Un número positivo. Se trata del tamaño (en gigabytes en forma de número entero o con decimales) del espacio total asignado a las tablas distribuidas (y a los datos correspondientes) *en todo el dispositivo*. Para conocer los requisitos mínimos y máximos de *distributed_size*, vea la sección sobre valores mínimos y máximos de la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si AUTOGROW está establecido en ON, las tablas distribuidas podrán crecer más allá de este límite.  
  
 Si AUTOGROW está establecido en OFF, se devolverá un error si un usuario intenta crear una tabla distribuida, insertar datos en una tabla distribuida ya existente o actualizar una tabla distribuida ya existente de forma que pueda aumentar el tamaño más allá de *distributed_size*.  
  
 *log_size* [ GB ]  
 Un número positivo. Se trata del tamaño (en gigabytes en forma de número entero o con decimales) del registro de transacciones *en todo el dispositivo*.  
  
 Para conocer los requisitos mínimos y máximos de *log_size*, vea la sección sobre valores mínimos y máximos de la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Si AUTOGROW está establecido en ON, el archivo de registro podrá crecer más allá de este límite. Use la instrucción [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para reducir el tamaño de los archivos de registro a su tamaño original.  
  
 Si AUTOGROW está establecido en OFF, se devolverá un error al usuario si intenta realizar cualquier acción que suponga aumentar el tamaño del registro más allá de *log_size* en un nodo de ejecución concreto.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **CREATE ANY DATABASE** en la base de datos maestra o pertenecer al rol fijo de servidor **sysadmin**.  
  
 En el ejemplo siguiente se proporciona el permiso para crear una base de datos al usuario de base de datos Fay.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>Notas generales  
 Las bases de datos se crean con el nivel de compatibilidad de base de datos 120, que es el nivel de compatibilidad de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. De este modo, se asegura que la base de datos podrá usar toda la funcionalidad de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] que PDW usa.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 La instrucción CREATE DATABASE no se puede usar en una transacción explícita. Para más información, vea [Statements](../../t-sql/statements/statements.md) (Instrucciones).  
  
 Para más información sobre las limitaciones mínimas y máximas en las bases de datos, vea la sección sobre valores mínimos y máximos de la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 En el momento en que se cree una base de datos, debe haber suficiente espacio libre disponible *en cada nodo de ejecución* que permita asignar el total combinado de los siguientes tamaños:  
  
-   Base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con tablas que tengan el tamaño de *replicated_table_size*.  
  
-   Base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con tablas que tengan un tamaño de (*distributed_table_size*/número de nodos de ejecución).  
  
-   Registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tengan un tamaño de (*log_size*/número de nodos de ejecución).  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto DATABASE.  
  
## <a name="metadata"></a>Metadatos  
 Después de que esta operación se realice correctamente, aparecerá una entrada relativa a esta base de datos en las vistas de metadatos [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. Ejemplos básicos de creación de base de datos  
 En el siguiente ejemplo se crea la base de datos `mytest` con una asignación de almacenamiento de 100 GB por nodo de ejecución para las tablas replicadas, 500 GB por dispositivo para las tablas distribuidas y 100 GB por dispositivo para el registro de transacciones. En este ejemplo, AUTOGROW está desactivado de forma predeterminada.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 En el siguiente ejemplo se crea la base de datos `mytest` con los mismos parámetros que el anterior, excepto que AUTOGROW está activado. Esto permite que la base de datos crezca fuera de los parámetros de tamaño especificado.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Crear una base de datos con tamaños de gigabyte parciales  
 En el siguiente ejemplo se crea la base de datos `mytest` con AUTOGROW desactivado y con una asignación de almacenamiento de 1,5 GB por nodo de ejecución para las tablas replicadas, 5,25 GB por dispositivo para las tablas distribuidas y 10 GB por dispositivo para el registro de transacciones.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>Ver también  
 [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)  (ALTER DATABASE [Almacenamiento de datos paralelos])  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  

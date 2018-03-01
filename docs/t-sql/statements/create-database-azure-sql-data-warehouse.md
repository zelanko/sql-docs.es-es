---
title: CREATE DATABASE (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 02/14/20178
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 3a802dc74793ef79ca35b177b4416d9464a8c34f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Crea una nueva base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
El nombre de la nueva base de datos. Este nombre debe ser único en el servidor SQL, que puede hospedar tanto bases de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], y cumplir con las reglas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obtener más información, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*collation_name*  
Especifica la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, a la base de datos se le asigna la intercalación predeterminada, que es SQL_Latin1_General_CP1_CI_AS.  
  
Para obtener más información sobre los nombres de intercalación de Windows y SQL, consulte [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDITION*  
Especifica el nivel de servicio de la base de datos. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], use "datawarehouse".  
  
*MAXSIZE*  
El valor predeterminado es 245 760 GB (240 TB).  

**Se aplica a:** optimizado para el nivel de rendimiento de Elasticity.

El tamaño máximo permitido para la base de datos. La base de datos no puede superar el valor de MAXSIZE. 

**Se aplica a:** optimizado para el nivel de rendimiento de Compute.

Tamaño máximo permitido para los datos de almacenamiento de filas de la base de datos. Los datos almacenados en tablas de almacenamiento de filas, en el almacén delta de un índice de almacén de columnas o en un índice no agrupado de un índice de almacén de columnas en clúster no pueden superar el valor de MAXSIZE.  Los datos comprimidos en formato de almacén de columnas no tienen un límite de tamaño y no están restringidos por el valor de MAXSIZE.
  
SERVICE_OBJECTIVE  
Especifica el nivel de rendimiento. Para más información sobre los objetivos de servicio para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], vea [Niveles de rendimiento](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="general-remarks"></a>Notas generales  
Use [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) para ver las propiedades de la base de datos.  
  
Use [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) para cambiar el tamaño máximo o los valores de objetivo de servicio más adelante.   

SQL Data Warehouse está establecido en COMPATIBILITY_LEVEL 130 y no se puede cambiar. Para más información, vea [Rendimiento de consultas mejorado con el nivel de compatibilidad 130 en Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
## <a name="permissions"></a>Permisos  
Permisos necesarios:  
  
-   Inicio de sesión principal en el nivel de servidor, creado por el proceso de aprovisionamiento, o  
  
-   Miembro del rol de base de datos `dbmanager`.  
  
## <a name="error-handling"></a>Tratamiento de errores  
Si el tamaño de la base de datos alcanza el valor de MAXSIZE, recibirá el código de error 40544. Cuando esto sucede, no es posible insertar ni actualizar datos, ni tampoco crear nuevos objetos (como tablas, procedimientos almacenados, vistas y funciones). Sin embargo, todavía puede leer y eliminar datos, truncar tablas, quitar tablas e índices, y recompilar índices. Seguidamente, puede actualizar MAXSIZE a un valor mayor que el tamaño actual de la base de datos o eliminar algunos datos para liberar espacio de almacenamiento. Puede haber un retraso de hasta quince minutos antes de que pueda insertar nuevos datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
Debe estar conectado a la base de datos maestra para crear una base de datos.  
  
La instrucción `CREATE DATABASE` debe ser la única de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)].

No se puede cambiar la intercalación de base de datos una vez creada la base de datos.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
Un ejemplo sencillo de cómo crear una base de datos de almacenamiento de datos. De esta forma se crea la base de datos con el tamaño más pequeño, 10 240 GB, la intercalación predeterminada, SQL_Latin1_General_CP1_CI_AS, y la potencia de proceso más reducida, DW100.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Crear una base de datos de almacenamiento de datos con todas las opciones  
Un ejemplo de cómo crear un almacenamiento de datos de 10 terabytes usando todas las opciones.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Ver también  
[ALTER DATABASE &#40;Azure SQL Data Warehouse&#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATABASE &#40;Transact-SQL&#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  


---
title: Crear base de datos (almacenamiento de datos SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 10/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 7406a538eb4c0f236f2e0d444e96fd2c4fa5d585
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="create-database-azure-sql-data-warehouse"></a>Crear base de datos (almacenamiento de datos SQL Azure)
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
El nombre de la nueva base de datos. Este nombre debe ser único en el servidor SQL, que puede hospedar ambos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] bases de datos y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bases de datos y cumplir con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reglas de los identificadores. Para obtener más información, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*collation_name*  
Especifica la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, la base de datos se asigna la intercalación predeterminada, que es SQL_Latin1_General_CP1_CI_AS.  
  
Para obtener más información acerca de los nombres de intercalación de Windows y SQL, consulte [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDICIÓN*  
Especifica el nivel de servicio de la base de datos. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usar 'almacenamiento de datos'.  
  
*MAXSIZE*  
El valor predeterminado es 10240 GB (10 TB).  

**Se aplica a:** optimizado para el nivel de rendimiento de elasticidad

El tamaño máximo permitido para la base de datos. La base de datos no puede crecer más allá de MAXSIZE. 

**Se aplica a:** optimizado para el nivel de rendimiento de proceso

El tamaño máximo permitido para los datos del almacén de la base de datos. Datos almacenados en tablas de almacén de filas, el almacén delta del índice de almacén de columnas o un índice no agrupado en un índice de almacén de columnas agrupado no pueden crecer más allá de MAXSIZE.  Los datos comprimidos en formato de almacén de columnas no tiene un límite de tamaño y no está limitados por MAXSIZE.
  
SERVICE_OBJECTIVE  
Especifica el nivel de rendimiento. Para obtener más información acerca de los objetivos de servicio para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], consulte [niveles de rendimiento](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="general-remarks"></a>Notas generales  
Use [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md) para ver las propiedades de la base de datos.  
  
Use [ALTER DATABASE &#40; Almacenamiento de datos SQL de Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) para cambiar el tamaño máximo, o los valores objetivo de servicio más adelante.   

Almacenamiento de datos de SQL está establecido en COMPATIBILITY_LEVEL 130 y no se puede cambiar. Para obtener más información, consulte [mejora el rendimiento de la consulta con 130 de nivel de compatibilidad de base de datos de SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
## <a name="permissions"></a>Permissions  
Permisos necesarios:  
  
-   Servidor nivel inicio de sesión principal, creado por el proceso de aprovisionamiento, o  
  
-   Miembro de la `dbmanager` rol de base de datos.  
  
## <a name="error-handling"></a>Tratamiento de errores  
Si el tamaño de la base de datos alcanza el valor de MAXSIZE, recibirá el código de error 40544. Cuando esto ocurre, no se puede insertar y actualizar datos o crear nuevos objetos (como tablas, procedimientos almacenados, vistas y funciones). Todavía puede leer y eliminar datos, truncar tablas, quitar tablas e índices y volver a generar índices. Seguidamente, puede actualizar MAXSIZE a un valor mayor que el tamaño actual de la base de datos o eliminar algunos datos para liberar espacio de almacenamiento. Puede haber un retraso de hasta quince minutos antes de que pueda insertar nuevos datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
Debe estar conectado a la base de datos maestra para crear una base de datos.  
  
La instrucción `CREATE DATABASE` debe ser la única de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)].

No se puede cambiar la intercalación de base de datos después de crea la base de datos.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Ejemplos:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
Un ejemplo sencillo para crear una base de datos de almacenamiento de datos. Esto crea la base de datos con el tamaño máximo más pequeño que es 10240 GB, la intercalación predeterminada que es SQL_Latin1_General_CP1_CI_AS y la capacidad de proceso más pequeño que es DW100.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Crear una base de datos de almacenamiento de datos con todas las opciones  
Un ejemplo de cómo crear un un almacenamiento de datos de 10 terabytes con todas las opciones.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Vea también  
[ALTER DATABASE &#40; Almacenamiento de datos SQL de Azure &#40; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
 [Crear una tabla &#40; Almacenamiento de datos SQL de Azure &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
 [Eliminar base de datos &#40; Transact-SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  


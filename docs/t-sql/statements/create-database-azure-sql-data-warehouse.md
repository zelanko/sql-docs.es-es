---
title: Crear base de datos (almacenamiento de datos SQL Azure) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/14/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 42819b93-b757-4b2c-8179-d4be3c512c19
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a178756610f0d0e463c21a2a62a287ada6c863a1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-data-warehouse"></a>Crear base de datos (almacenamiento de datos SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Crea una nueva base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB ,]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' }  
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
El tamaño máximo que puede alcanzar la base de datos. Este valor evita que el crecimiento del tamaño de base de datos más allá del conjunto de tamaño. El valor predeterminado *MAXSIZE* cuando no se especifica es 10240 GB (10 TB).  Otros valores posibles oscilan entre 250 GB hasta 240 TB.  
  
SERVICE_OBJECTIVE  
Especifica el nivel de rendimiento. Para obtener más información acerca de los objetivos de servicio para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], consulte [rendimiento de escala en almacenamiento de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-performance-scale/).  
  
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
  



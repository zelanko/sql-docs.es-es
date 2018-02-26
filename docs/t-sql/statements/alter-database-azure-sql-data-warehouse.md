---
title: ALTER DATABASE (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 02/15/2018
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
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: b70750eebf7727348f9058bea2aecd0508d544bd
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/19/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Modifica el nombre, el tamaño máximo o el objetivo del servicio de una base de datos.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
Especifica el nombre de la base de datos que se va a modificar.  

MODIFY NAME = *new_database_name*  
Reemplaza el nombre de la base de datos por el nombre especificado como *new_database_name*.  
  
MAXSIZE  
El valor predeterminado es 245 760 GB (240 TB).  

**Se aplica a:** optimizado para el nivel de rendimiento de Elasticity.

El tamaño máximo permitido para la base de datos. La base de datos no puede superar el valor de MAXSIZE. 

**Se aplica a:** optimizado para el nivel de rendimiento de Compute.

Tamaño máximo permitido para los datos de almacenamiento de filas de la base de datos. Los datos almacenados en tablas de almacenamiento de filas, en el almacén delta de un índice de almacén de columnas o en un índice no agrupado de un índice de almacén de columnas en clúster no pueden superar el valor de MAXSIZE.  Los datos comprimidos en formato de almacén de columnas no tienen un límite de tamaño y no están restringidos por el valor de MAXSIZE. 
  
SERVICE_OBJECTIVE  
Especifica el nivel de rendimiento. Para más información sobre los objetivos de servicio para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], vea [Niveles de rendimiento](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Permisos  
Se requieren estos permisos:  
  
-   Inicio de sesión principal en el nivel de servidor (creado por el proceso de aprovisionamiento), o  
  
-   Miembro del rol de base de datos `dbmanager`.  
  
El propietario de la base de datos no puede modificarla a menos que sea miembro del rol `dbmanager`.  
  
## <a name="general-remarks"></a>Notas generales  
La base de datos actual debe ser diferente de la base de datos que está modificando, por lo que **ALTER debe ejecutarse mientras se está conectado a la base de datos maestra**.  
  
SQL Data Warehouse está establecido en COMPATIBILITY_LEVEL 130 y no se puede cambiar. Para más información, vea [Rendimiento de consultas mejorado con el nivel de compatibilidad 130 en Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
Para reducir el tamaño de una base de datos, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
Para ejecutar ALTER DATABASE, la base de datos debe estar en línea y no puede encontrarse en estado de pausa.  
  
La instrucción ALTER DATABASE debe ejecutarse en modo de confirmación automática, que es el modo de administración de transacciones predeterminado. Esto se establece en la configuración de conexión.  
  
La instrucción ALTER DATABASE no puede formar parte de una transacción definida por el usuario.

No es posible cambiar la intercalación de base de datos.  
  
## <a name="examples"></a>Ejemplos  
Antes de ejecutar estos ejemplos, asegúrese de que la base de datos que está modificando no es la base de datos actual. La base de datos actual debe ser diferente de la base de datos que está modificando, por lo que **ALTER debe ejecutarse mientras se está conectado a la base de datos maestra**.  

### <a name="a-change-the-name-of-the-database"></a>A. Cambiar el nombre de la base de datos  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. Cambiar el tamaño máximo de la base de datos  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. Cambiar el nivel de rendimiento  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. Cambiar el tamaño máximo y el nivel de rendimiento  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>Ver también  
[CREATE DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[Lista de temas de referencia de SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  

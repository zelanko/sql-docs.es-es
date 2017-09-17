---
title: ALTER DATABASE (almacenamiento de datos SQL Azure) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/03/2017
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
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5e328da952c853409437f7c3a4993f17022de22
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-azure-sql-data-warehouse"></a>Modificar base de datos (almacenamiento de datos SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Modifica el nombre, el tamaño máximo o el objetivo de servicio para una base de datos.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB  
    | SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000'}  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
Especifica el nombre de la base de datos a modificarse.  

MODIFY NAME = *new_database_name*  
Cambia el nombre de la base de datos con el nombre especificado como *new_database_name*.  
  
MAXSIZE  
El tamaño máximo que puede alcanzar la base de datos. Este valor evita que el crecimiento del tamaño de base de datos más allá del conjunto de tamaño. El valor predeterminado *MAXSIZE* cuando no se especifica es 10240 GB (10 TB). Otros valores posibles oscilan entre 250 GB hasta 240 TB.  
  
SERVICE_OBJECTIVE  
Especifica el nivel de rendimiento. Para obtener más información acerca de los objetivos de servicio para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], consulte [rendimiento de escala en almacenamiento de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-manage-compute-overview/).  
  
## <a name="permissions"></a>Permissions  
Estos permisos se necesita:  
  
-   Inicio de sesión principal del nivel de servidor (creado por el proceso de aprovisionamiento uno), o  
  
-   Miembro de la `dbmanager` rol de base de datos.  
  
El propietario de la base de datos no puede modificar la base de datos a menos que el propietario es un miembro de la `dbmanager` rol.  
  
## <a name="general-remarks"></a>Notas generales  
La base de datos actual debe ser otra base de datos a la que se está modificando, por lo tanto, **ALTER debe ejecutarse mientras está conectado a la base de datos maestra**.  
  
Almacenamiento de datos de SQL está establecido en COMPATIBILITY_LEVEL 130 y no se puede cambiar. Para obtener más información, consulte [mejora el rendimiento de la consulta con 130 de nivel de compatibilidad de base de datos de SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
Para reducir el tamaño de una base de datos, utilice [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
Para ejecutar ALTER DATABASE, la base de datos debe estar en línea y no puede estar en un estado de pausa.  
  
La instrucción ALTER DATABASE debe ejecutarse en modo de confirmación automática, que es el modo de administración de transacciones predeterminado. Esto se establece en la configuración de conexión.  
  
La instrucción ALTER DATABASE no puede formar parte de una transacción definida por el usuario.

No se puede cambiar la intercalación de base de datos.  
  
## <a name="examples"></a>Ejemplos  
Antes de ejecutar estos ejemplos, asegúrese de que la base de datos que se está modificando no es la base de datos actual. La base de datos actual debe ser otra base de datos a la que se está modificando, por lo tanto, **ALTER debe ejecutarse mientras está conectado a la base de datos maestra**.  

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
  
## <a name="see-also"></a>Vea también  
[CREATE DATABASE (almacenamiento de datos de SQL Azure)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[lista de almacenamiento de datos SQL de temas de referencia](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  

---
title: Base de datos tempdb - almacenamiento de datos paralelos | Microsoft Docs
description: Base de datos tempdb en almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156964"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>base de datos tempdb en almacenamiento de datos paralelos
**tempdb** es una base de datos del sistema de PDW de SQL Server que almacena las tablas temporales locales para las bases de datos de usuario. Las tablas temporales se usan a menudo para mejorar el rendimiento de las consultas. Por ejemplo, puede usar una tabla temporal para modularizar una secuencia de comandos y reutilizar datos calculados.  
  
Para obtener más información acerca de las bases de datos del sistema, consulte [las bases de datos del sistema](system-databases.md).  
  
## <a name="Basics"></a>Términos y conceptos clave  
*tabla temporal local*  
Un *tabla temporal local* usa el prefijo # antes del nombre de tabla y es una tabla temporal creada por una sesión de usuario local. Cada sesión solo puede tener acceso a los datos en las tablas temporales locales para su propia sesión.  
  
Cada sesión puede ver los metadatos de las tablas temporales locales en todas las sesiones. Por ejemplo, todas las sesiones pueden ver los metadatos de todas las tablas temporales locales con la `SELECT * FROM tempdb.sys.tables` consulta.  
  
tabla temporal global  
*Las tablas temporales globales*, admitidos en SQL Server con la ## sintaxis, no se admiten en esta versión de PDW de SQL Server.  
  
pdwtempdb  
**pdwtempdb** es la base de datos que almacena las tablas temporales locales.  
  
PDW implementar tablas temporales mediante el uso de SQL Server**tempdb** base de datos. En su lugar, PDW almacena en una base de datos denominada pdwtempdb. Esta base de datos existe en cada nodo de proceso y no es visible para el usuario a través de las interfaces PDW. En la consola de administración, en la página de almacenamiento, verá estas contabilizado para en una base de datos del sistema PDW llamado **tempdb sql**.  
  
tempdb  
**tempdb** es la base de datos de tempdb de SQL Server. Usa el registro mínimo. SQL Server utiliza tempdb en los nodos de proceso para almacenar las tablas temporales que necesita en el curso de operaciones de SQL Server.  
  
PDW de SQL Server quita las tablas de **tempdb** cuando:  
  
-   Se ejecuta la instrucción DROP TABLE.  
  
-   Una sesión se desconecta. Se quitan solo las tablas temporales para la sesión.  
  
-   El dispositivo está apagado.  
  
-   El nodo de Control tiene un clúster de conmutación por error.  
  
## <a name="general-remarks"></a>Notas generales  
PDW de SQL Server realiza las mismas operaciones en las tablas temporales y tablas permanentes a menos que indique explícitamente lo contrario. Por ejemplo, los datos en las tablas temporales locales, como tablas permanentes, se distribuye o replicarse a través de los nodos de proceso.  
  
## <a name="LimitationsRestrictions"></a>Limitaciones y restricciones  
Limitaciones y restricciones en el PDW de SQL Server**tempdb** base de datos. Le *no se puede:*  
  
-   Crear una tabla temporal global que empieza por ##.  
  
-   Realizar una copia de seguridad o restauración de **tempdb**.  
  
-   Modificar los permisos de **tempdb** con el **GRANT**, **DENY**, o **REVOCAR** instrucciones.  
  
-   Ejecutar **DBCC SHRINKLOG** para **tempdb**tempdb.  
  
-   Realizar operaciones DDL en **tempdb**. Hay dos excepciones a esto. Para obtener más información, vea la siguiente lista de limitaciones y restricciones en las tablas temporales locales.  
  
Limitaciones y restricciones en las tablas temporales locales. Le *no se puede:*  
  
-   Cambiar el nombre de una tabla temporal  
  
-   Creación de particiones, vistas o índices no agrupados en una tabla temporal. **ALTER INDEX** se puede usar para volver a generar un índice agrupado para una tabla creada con uno.  
  
-   Modificar permisos para las tablas temporales con la instrucción GRANT, DENY, o REVOCAR las instrucciones.  
  
-   Ejecute los comandos de la consola de base de datos en las tablas temporales.  
  
-   Use el mismo nombre para dos o más tablas temporales dentro del mismo lote. Si se usa más de una tabla temporal local dentro de un lote, cada una debe tener un nombre único. Si varias sesiones ejecutan el mismo lote y crear la misma tabla temporal local, SQL Server PDW anexa internamente un sufijo numérico al nombre de tabla temporal local para mantener un nombre único para cada tabla temporal local.  
  
> [!NOTE]  
> Le *puede* crear y actualizar las estadísticas en una tabla temporal. **ALTER INDEX** se puede usar para volver a generar un índice agrupado.  
  
## <a name="permissions"></a>Permisos  
Cualquier usuario puede crear objetos temporales en tempdb. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a tempdb para impedir que un usuario use tempdb, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de tempdb.  
  
## <a name="RelatedTasks"></a>Tareas relacionadas  
  
|Tareas|Descripción|  
|---------|---------------|  
|Crear una tabla en **tempdb**.|Puede crear una tabla temporal del usuario con las instrucciones CREATE TABLE y CREATE TABLE AS SELECT. Para obtener más información, consulte [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) y [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Ver una lista de las tablas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Ver una lista de las columnas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Ver una lista de los objetos existentes en **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

---
title: Base de datos tempdb - almacenamiento de datos paralelos | Documentos de Microsoft
description: Base de datos de tempdb en almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538865"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>base de datos tempdb en almacenamiento de datos paralelos
**tempdb** es una base de datos del sistema de PDW de SQL Server que almacena las tablas temporales locales para las bases de datos de usuario. Tablas temporales se usan a menudo para mejorar el rendimiento de las consultas. Por ejemplo, puede usar una tabla temporal para modularizar una secuencia de comandos y reutilizar los datos calculados.  
  
Para obtener más información acerca de las bases de datos del sistema, consulte [bases de datos de sistema](system-databases.md).  
  
## <a name="Basics"></a>Términos y conceptos clave  
*tabla temporal local*  
A *tabla temporal local* usa el prefijo # antes del nombre de tabla y es una tabla temporal creada por una sesión de usuario local. Cada sesión sólo puede tener acceso a los datos de las tablas temporales locales para su propia sesión.  
  
Cada sesión puede ver los metadatos de las tablas temporales locales en todas las sesiones. Por ejemplo, todas las sesiones pueden ver los metadatos de todas las tablas temporales locales con el `SELECT * FROM tempdb.sys.tables` consulta.  
  
tabla temporal global  
*Las tablas temporales globales*, se admite en SQL Server con el ## sintaxis, no se admiten en esta versión de SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** es la base de datos que almacena las tablas temporales locales.  
  
PDW implementar tablas temporales con el servidor SQL**tempdb** base de datos. En su lugar, PDW almacena en una base de datos denominada pdwtempdb. Esta base de datos existe en cada nodo de ejecución y no está visible al usuario a través de las interfaces PDW. En la consola de administración, en la página de almacenamiento, verá estas representaron para en una base de datos del sistema PDW denominada **tempdb sql**.  
  
tempdb  
**tempdb** es la base de datos de tempdb de SQL Server. Usa el registro mínimo. SQL Server utiliza tempdb en los nodos de proceso para almacenar tablas temporales que necesita en el curso de operaciones de SQL Server.  
  
SQL Server PDW quita tablas de **tempdb** cuando:  
  
-   Se ejecuta la instrucción DROP TABLE.  
  
-   Se desconectó una sesión. Solo las tablas temporales de la sesión se quitan.  
  
-   El dispositivo está apagado.  
  
-   El nodo de Control tiene un clúster de conmutación por error.  
  
## <a name="general-remarks"></a>Notas generales  
PDW de SQL Server realiza las mismas operaciones en tablas temporales y tablas permanentes a menos que establezca explícitamente lo contrario. Por ejemplo, los datos de las tablas temporales locales, como tablas permanentes, se distribuidas o replicar en todos los nodos de proceso.  
  
## <a name="LimitationsRestrictions"></a>Limitaciones y restricciones  
Limitaciones y restricciones en SQL Server PDW**tempdb** base de datos. Se *no se puede:*  
  
-   Crear una tabla temporal global que comienza por ##.  
  
-   Realizar una copia de seguridad o restauración de **tempdb**.  
  
-   Modificar los permisos **tempdb** con el **GRANT**, **DENY**, o **REVOCAR** instrucciones.  
  
-   Ejecutar **DBCC SHRINKLOG** para **tempdb**tempdb.  
  
-   Realizar operaciones DDL en **tempdb**. Hay dos excepciones a esto. Para obtener más información, vea la siguiente lista de limitaciones y restricciones en las tablas temporales locales.  
  
Limitaciones y restricciones en las tablas temporales locales. Se *no se puede:*  
  
-   Cambiar el nombre de una tabla temporal  
  
-   Crear particiones, vistas o índices no clúster en una tabla temporal. **ALTER INDEX** puede utilizarse para volver a generar un índice agrupado para una tabla creada con uno.  
  
-   Modificar los permisos a las tablas temporales con la instrucción GRANT, DENY, o REVOCAR las instrucciones.  
  
-   Ejecutar comandos de la consola de base de datos en las tablas temporales.  
  
-   Utilice el mismo nombre para dos o más tablas temporales dentro del mismo lote. Si se usa más de una tabla temporal local dentro de un lote, cada una debe tener un nombre único. Si varias sesiones están ejecutando el mismo lote y crear la misma tabla temporal local, SQL Server PDW internamente anexa un sufijo numérico al nombre de tabla temporal local para mantener un nombre único para cada tabla temporal local.  
  
> [!NOTE]  
> Se *puede* crear y actualizar las estadísticas en una tabla temporal. **ALTER INDEX** puede utilizarse para volver a generar un índice agrupado.  
  
## <a name="permissions"></a>Permissions  
Cualquier usuario puede crear objetos temporales en tempdb. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a tempdb para impedir que un usuario use tempdb, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de tempdb.  
  
## <a name="RelatedTasks"></a>Tareas relacionadas  
  
|Tareas|Description|  
|---------|---------------|  
|Crear una tabla en **tempdb**.|Puede crear una tabla temporal del usuario con las instrucciones CREATE TABLE y CREATE TABLE AS SELECT. Para obtener más información, consulte [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) y [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Ver una lista de las tablas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Ver una lista de las columnas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Ver una lista de los objetos existentes en **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

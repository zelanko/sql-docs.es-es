---
title: Base de datos Tempdb
description: Base de datos Tempdb en almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3772e2b4cabac84c00854eba85f7a0c2a33d48bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400139"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>base de datos Tempdb en almacenamiento de datos paralelos
**tempdb** es una PDW de SQL Server base de datos del sistema que almacena tablas temporales locales para las bases de datos de usuario. Las tablas temporales suelen usarse para mejorar el rendimiento de las consultas. Por ejemplo, puede usar una tabla temporal para modularr un script y reutilizar los datos calculados.  
  
Para obtener más información acerca de las bases de datos del sistema, vea bases de datos [del sistema](system-databases.md).  
  
## <a name="key-terms-and-concepts"></a><a name="Basics"></a>Términos y conceptos clave  
*tabla temporal local*  
Una *tabla temporal local* usa el prefijo # delante del nombre de la tabla y es una tabla temporal creada por una sesión de usuario local. Cada sesión solo puede tener acceso a los datos de las tablas temporales locales para su propia sesión.  
  
Cada sesión puede ver los metadatos de las tablas temporales locales en todas las sesiones. Por ejemplo, todas las sesiones pueden ver los metadatos de todas las tablas temporales `SELECT * FROM tempdb.sys.tables` locales con la consulta.  
  
tabla temporal global  
En esta versión de PDW de SQL Server no se admiten *tablas temporales globales*, admitidas en SQL Server con la sintaxis # #.  
  
pdwtempdb  
**pdwtempdb** es la base de datos que almacena las tablas temporales locales.  
  
PDW no implementa tablas temporales mediante el SQL Server base de datos**tempdb** . En su lugar, PDW los almacena en una base de datos denominada pdwtempdb. Esta base de datos existe en cada nodo de proceso y no es visible para el usuario a través de las interfaces PDW. En la consola de administración de, en la página almacenamiento, verá estas cuentas en una base de datos del sistema de PDW denominada **tempdb-SQL**.  
  
tempdb  
**tempdb** es la SQL Server base de datos tempdb. Utiliza el registro mínimo. SQL Server usa tempdb en los nodos de proceso para almacenar las tablas temporales que necesita en el transcurso de la realización de operaciones de SQL Server.  
  
PDW de SQL Server quita las tablas de **tempdb** cuando:  
  
-   Se ejecuta la instrucción DROP TABLE.  
  
-   Una sesión está desconectada. Solo se quitan las tablas temporales de la sesión.  
  
-   El dispositivo está apagado.  
  
-   El nodo de control tiene una conmutación por error de clúster.  
  
## <a name="general-remarks"></a>Notas generales  
PDW de SQL Server realiza las mismas operaciones en las tablas temporales y en las tablas permanentes, a menos que se indique explícitamente lo contrario. Por ejemplo, los datos de las tablas temporales locales, al igual que las tablas permanentes, se distribuyen o replican en los nodos de proceso.  
  
## <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a>Limitaciones y restricciones  
Limitaciones y restricciones en el PDW de SQL Server base de datos**tempdb** . *No se puede:*  
  
-   Cree una tabla temporal global que empiece por # #.  
  
-   Realice una copia de seguridad o una restauración de **tempdb**.  
  
-   Modifique los permisos de **tempdb** con las instrucciones **Grant**, **Deny**o **REVOKE** .  
  
-   Ejecute **DBCC SHRINKLOG** para **tempdb tempdb.**  
  
-   Realizar operaciones DDL en **tempdb**. Hay un par de excepciones a esto. Para obtener más información, consulte la siguiente lista de limitaciones y restricciones de las tablas temporales locales.  
  
Limitaciones y restricciones en las tablas temporales locales. *No se puede:*  
  
-   Cambiar el nombre de una tabla temporal  
  
-   Cree particiones, vistas o índices no clúster en una tabla temporal. Se puede usar **ALTER index** para volver a generar un índice clúster para una tabla creada con uno.  
  
-   Modifique los permisos de las tablas temporales con las instrucciones GRANT, DENY o REVOKE.  
  
-   Ejecutar comandos de consola de base de datos en tablas temporales.  
  
-   Use el mismo nombre para dos o más tablas temporales en el mismo lote. Si se usa más de una tabla temporal local dentro de un lote, cada una debe tener un nombre único. Si varias sesiones ejecutan el mismo lote y crean la misma tabla temporal local, PDW de SQL Server anexa internamente un sufijo numérico al nombre de la tabla temporal local para mantener un nombre único para cada tabla temporal local.  
  
> [!NOTE]  
> *Puede* crear y actualizar las estadísticas en una tabla temporal. Se puede usar **ALTER index** para volver a generar un índice clúster.  
  
## <a name="permissions"></a>Permisos  
Cualquier usuario puede crear objetos temporales en tempdb. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a tempdb para impedir que un usuario use tempdb, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de tempdb.  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a>Related Tasks  
  
|Tareas|Descripción|  
|---------|---------------|  
|Cree una tabla en **tempdb**.|Puede crear una tabla temporal de usuario con el CREATE TABLE y CREATE TABLE como instrucciones SELECT. Para obtener más información, vea [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) y [CREATE TABLE como Select](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Ver una lista de tablas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Ver una lista de columnas existentes en **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Ver una lista de objetos existentes en **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

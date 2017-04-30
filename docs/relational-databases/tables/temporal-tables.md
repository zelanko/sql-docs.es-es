---
title: Tablas temporales | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/11/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e442303d-4de1-494e-94e4-4f66c29b5fb9
caps.latest.revision: 47
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a4cdbe630a64ce01c6319dcc5791c0f3f9b3176b
ms.lasthandoff: 04/11/2017

---
# <a name="temporal-tables"></a>Tablas temporales
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incorpora una característica de base de datos que admite tablas temporales con versión del sistema, lo que permite proporcionar información sobre los datos almacenados en la tabla en cualquier momento en el tiempo, en vez de únicamente los datos que son correctos en el momento actual determinado. La característica temporal de las bases de datos surgió con ANSI SQL 2011 y ahora es compatible con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **Inicio rápido**  
  
-   **Introducción:**  
  
    -   [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)  
  
    -   [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
  
    -   [Escenarios de uso de tablas temporales](../../relational-databases/tables/temporal-table-usage-scenarios.md)  
  
    -   [Getting Started with Temporal Tables in Azure SQL Database (Introducción a las tablas temporales de Base de datos SQL de Azure)](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)  
  
-   **Ejemplos:**  
  
    -   [Creación de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
    -   [Trabajo con tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)  
  
    -   [Modificación de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
    -   [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
    -   **Descargue la base de datos de ejemplo Adventure Works:** si quiere empezar a trabajar con las tablas temporales, descargue la [base de datos AdventureWorks para SQL Server 2016 CTP3](https://www.microsoft.com/download/details.aspx?id=49502) con scripts de ejemplo y siga las instrucciones de la carpeta 'Temporal'.  
  
-   **Sintaxis:**  
  
    -   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
    -   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
    -   [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
-   **Vídeo:** si le interesa ver un análisis de 20 minutos sobre las tablas temporales, vea [Temporal in SQL Server 2016](http://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)(Temporal en SQL Server 2016).  
  
## <a name="what-is-a-system-versioned-temporal-table"></a>¿Qué es una tabla temporal con versión del sistema?  
 Una tabla temporal con versión del sistema es un nuevo tipo de tabla de usuario de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]pensada para conservar un historial completo de los cambios de datos y para facilitar los análisis en un momento específico. Este tipo de tabla temporal se conoce como tabla temporal con versión del sistema, porque el período de validez de cada fila se administra por medio del sistema (es decir, del motor de base de datos).  
  
 Cada tabla temporal tiene dos columnas definidas explícitamente, cada una con un tipo de datos **datetime2** . Estas columnas se conocen como columnas de periodo. Estas columnas de periodo son de uso exclusivo por parte del sistema para registrar el período de validez de cada fila cada vez que una fila se modifica.  
  
 Aparte de estas columnas, una tabla temporal contiene también una referencia a otra tabla con un esquema reflejado. El sistema usa esta tabla para almacenar automáticamente la versión anterior de una fila de la tabla temporal cada vez que dicha fila se actualiza o elimina. Esta tabla adicional se conoce como tabla de historial, mientras que la tabla principal que almacena las versiones de fila actuales (reales) se conoce como tabla actual o, simplemente, como tabla temporal. Durante la creación de una tabla temporal, los usuarios pueden especificar una tabla de historial existente (debe admitir esquemas) o dejar que el sistema cree una tabla de historial predeterminada.  
  
## <a name="why-temporal"></a>¿Por qué temporal?  
 Los orígenes de datos reales son dinámicos y, con más frecuencia que las decisiones no empresariales, se basan en la información que los analistas obtienen de la evolución de los datos. Estos son los casos de uso de tablas temporales:  
  
-   Realizar una auditoría de todos los cambios de datos y realizar análisis forenses de datos cuando sea necesario  
  
-   Reconstruir el estado de los datos a partir de cualquier momento en el pasado  
  
-   Calcular las tendencias en el tiempo  
  
-   Mantener una dimensión de variación lenta para aplicaciones de apoyo de decisiones  
  
-   Recuperarse de cambios accidentales de datos y errores de aplicación  
  
## <a name="how-does-temporal-work"></a>¿Cómo funciona la característica temporal?  
 La versión del sistema de una tabla se implementa como un par de tablas: una tabla actual y una tabla de historial. Dentro de cada una de estas tablas, se usan las dos columnas **datetime2** adicionales siguientes para definir el período de validez de cada fila:  
  
-   Columna de inicio del periodo: el sistema registra la hora de inicio de la fila en esta columna, que normalmente se denomina **SysStartTime** .  
  
-   Columna de fin del periodo: el sistema registra la hora de fin de la fila en esta columna, que normalmente se denomina **SysEndTime** .  
  
 La tabla actual contiene el valor actual de cada fila. La tabla de historial contiene cada valor anterior de cada fila, si existe, y las horas de inicio y fin del periodo de validez.  
  
 ![Temporal: cómo funciona](../../relational-databases/tables/media/temporal-howworks.PNG "Temporal: cómo funciona")  
  
 En este sencillo ejemplo se ilustra un escenario con información sobre empleados en una hipotética base de datos de recursos humanos:  
  
```  
CREATE TABLE dbo.Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 **INSERTS:** en una instrucción **INSERT**, el sistema establece el valor de la columna **SysStartTime** en la hora de inicio de la transacción actual (en la zona horaria UTC) según el reloj del sistema y asigna el valor de la columna **SysEndTime** en el valor máximo de 9999-12-31. Esto marca la fila como abierta.  
  
 **UPDATES:** en una instrucción **UPDATE**, el sistema almacena el valor anterior de la fila en la tabla de historial y establece el valor de la columna **SysEndTime** en la hora de inicio de la transacción actual (en la zona horaria UTC) según el reloj del sistema. Esto marca la fila como cerrada, con un periodo registrado durante el que la fila fue válida. En la tabla actual, la fila se actualiza con su nuevo valor y el sistema establece el valor de la columna **SysStartTime** en la hora de inicio de la transacción actual (en la zona horaria UTC) según el reloj del sistema. El valor de la fila actualizada en la tabla actual para la columna **SysEndTime** sigue siendo el valor máximo de 9999-12-31.  
  
 **DELETES:** en una instrucción **DELETES**, el sistema almacena el valor anterior de la fila en la tabla de historial y establece el valor de la columna **SysEndTime** en la hora de inicio de la transacción actual (en la zona horaria UTC) según el reloj del sistema. Esto marca la fila como cerrada, con un periodo registrado durante el que la fila anterior fue válida. En la tabla actual, la fila se quita. Las consultas de la tabla actual no devolverán esa fila. Solo las consultas que tengan que ver con los datos de historial devolverán datos relativos a una fila cerrada.  
  
 **MERGE:** en una instrucción **MERGE**, la operación es exactamente igual a si se ejecutaran hasta las tres instrucciones anteriores ( **INSERT**, **UPDATE**y/o **DELETE**), en función de lo que se haya especificado como acción en la instrucción **MERGE** .  
  
> [!IMPORTANT]  
>  Las horas registradas en las columnas datetime2 del sistema se basan en la hora de inicio de la propia transacción. Por ejemplo, todas las filas insertadas en una única transacción tendrán la misma hora UTC registrada en la columna correspondiente al inicio del período **SYSTEM_TIME** .  
  
## <a name="how-do-i-query-temporal-data"></a>¿Cómo se consultan los datos temporales?  
 La cláusula **FROM***\<table>* de la instrucción **SELECT** tiene una nueva cláusula **FOR SYSTEM_TIME** con cinco subcláusulas específicas para temporal con las que se pueden consultar datos de las tablas actual y de historial. Esta nueva sintaxis de la instrucción **SELECT** se puede usar directamente en una sola tabla, propagarse por varias combinaciones y por las vistas de varias tablas temporales.  
  
 ![Temporal: consultar](../../relational-databases/tables/media/temporal-querying.PNG "Temporal: consultar")  
  
 La siguiente consulta busca versiones de fila para la fila Employee con EmployeeID = 1000 que estaban activas al menos durante una parte del período comprendido entre el 1 de enero de 2014 y el 1 de enero de 2015 (incluido el límite superior):  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
> [!NOTE]  
>  **FOR SYSTEM_TIME** filtra las filas que tienen un período de validez con una duración cero (**SysStartTime** = **SysEndTime**).  
> Estas filas se generarán si realiza varias actualizaciones en la misma clave principal en la misma transacción.  
> En tal caso, las consultas temporales muestran solo las versiones de fila antes de las transacciones y las que pasaron a ser reales después de las transacciones.  
> Si necesita incluir esas filas en el análisis, consulte directamente la tabla de historial.  
  
 En la siguiente tabla, SysStartTime en la columna Filas certificadas representa el valor reflejado en la columna **SysStartTime** de la tabla que se está consultando y **SysEndTime** , el valor reflejado en la columna **SysEndTime** de la tabla que se está consultando. Para obtener la sintaxis completa y ejemplos, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) y [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md).  
  
|Expresión|Filas certificadas|Descripción|  
|----------------|---------------------|-----------------|  
|**AS OF**<date_time>|SysStartTime \<= date_time AND SysEndTime > date_time|Devuelve una tabla con filas que contienen los valores que fueron reales (actuales) en el momento determinado especificado en el pasado. Internamente, se realiza una unión entre la tabla temporal y su tabla de historial y los resultados se filtran para devolver los valores de la fila que era válida en el momento determinado especificado por el parámetro *<date_time>*. El valor de una fila se considera válido si el valor de *system_start_time_column_name* es menor o igual que el valor del parámetro *<date_time>* y el valor de *system_end_time_column_name* es mayor que el valor del parámetro *<date_time>*.|  
|**FROM**<start_date_time>**TO**<end_date_time>|SysStartTime < end_date_time AND SysEndTime > start_date_time|Devuelve una tabla con los valores de todas las versiones de fila que estaban activas dentro del rango de tiempo especificado, independientemente de si empezaron a ser activas antes del valor del parámetro *<start_date_time>* en el argumento FROM o si dejaron de serlo después del valor del parámetro *<end_date_time>* en el argumento TO. Internamente, se realiza una unión entre la tabla temporal y su tabla de historial y los resultados se filtran para devolver los valores de todas las versiones de fila que estaban activas en cualquier momento dentro del intervalo de tiempo especificado. No se incluyen las filas que dejaron de ser activas justamente en el límite inferior definido por el punto de conexión FROM ni tampoco aquellas que se activaron exactamente en el límite superior definido por el punto de conexión TO.|  
|**BETWEEN**<start_date_time>**AND**<end_date_time>|SysStartTime \<= end_date_time AND SysEndTime > start_date_time|Igual que la descripción anterior de **FOR SYSTEM_TIME FROM** <start_date_time>**TO** <end_date_time>, salvo que la tabla de filas devuelta incluye las filas que se activaron en el límite superior definido por el punto de conexión <end_date_time>.|  
|**CONTAINED IN** (<start_date_time> , <end_date_time>)|SysStartTime >= start_date_time AND SysEndTime \<= end_date_time|Devuelve una tabla con los valores de todas las versiones de fila que se abrieron y cerraron dentro del rango de tiempo especificado definido por los dos valores de fecha y hora en el argumento CONTAINED IN. Se incluyen las filas que se activaron justamente en el límite inferior o que dejaron de estarlo exactamente en el límite superior.|  
|**ALL**|Todas las filas|Devuelve la unión de las filas pertenecientes a la tabla actual y a la tabla de historial.|  
  
> [!NOTE]  
>  Si quiere, puede ocultar estas columnas de periodo, de forma que las consultas que no hagan referencia explícitamente a estas columnas de periodo no devuelvan esas columnas (el escenario de **SELECT \* FROM***\<table>*). Para devolver una columna oculta, basta con hacer referencia explícita a dicha columna en la consulta. Del mismo modo, las instrucciones **INSERT** y **BULK INSERT** continuarán como si estas nuevas columnas de periodo no estuvieran presentes (y los valores de columna se rellenarán automáticamente). Para obtener más información sobre cómo usar la cláusula **HIDDEN** , vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) y [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Vea también  
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Escenarios de uso de tablas temporales](../../relational-databases/tables/temporal-table-usage-scenarios.md)   
 [Limitaciones y consideraciones de las tablas temporales](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Creación de particiones con tablas temporales](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Seguridad de la tabla temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  


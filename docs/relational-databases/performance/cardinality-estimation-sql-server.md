---
title: "Estimación de cardinalidad (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 8b45a33dadae04400fbc0602f2aa4f6fc08d5df1
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="cardinality-estimation-sql-server"></a>Estimación de cardinalidad (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
En este artículo se explica cómo evaluar y elegir la mejor configuración de estimación de cardinalidad para su sistema SQL. La mayoría de los sistemas sacan partido de la última estimación de cardinalidad, porque es la más precisa. Con la estimación de cardinalidad se predice cuántas filas va a devolver la consulta casi con toda seguridad. El optimizador de consultas usa la predicción de cardinalidad para generar el mejor plan de consulta posible. Con estimaciones más precisas, el optimizador de consultas normalmente puede hacer mejor su trabajo a la hora de generar un plan de consulta óptimo.  
  
Es bastante probable que el sistema de aplicaciones tenga una consulta importante cuyo plan cambie a un plan más lento debido a la nueva estimación de cardinalidad. Esa consulta podría ser una de las siguientes:  
  
- Una consulta OLTP (procesamiento de transacciones en línea) que se ejecuta con tanta frecuencia que, a menudo, coinciden varias instancias al mismo tiempo.  
- Una instrucción SELECT con agregaciones importantes que se ejecuta durante el horario laboral de OLTP.  
  
Existen diversas técnicas para detectar una consulta que se ralentiza a raíz de la nueva estimación de cardinalidad. También hay diversas opciones para abordar ese problema de rendimiento.  
  
  
## <a name="versions-of-the-ce"></a>Versiones de la estimación de cardinalidad  
  
 En 1998, Microsoft SQL Server 7.0 incorporó una actualización importante de la estimación de cardinalidad, para la que el nivel de compatibilidad fue 70. Las actualizaciones posteriores empezaron por [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], que se tradujo en los niveles de compatibilidad 120 y posteriores. Las actualizaciones de estimación de cardinalidad correspondientes a los niveles 120 y posteriores incorporan hipótesis y algoritmos que funcionan bien en el almacenamiento de datos modernos y en las cargas de trabajo OLTP.  
  
 **Nivel de compatibilidad:** para procurar que la base de datos esté en un nivel determinado, use el siguiente código de Transact-SQL para [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

```tsql  
SELECT ServerProperty('ProductVersion');  
go  
  
ALTER DATABASE <yourDatabase>  
    SET COMPATIBILITY_LEVEL = 130;  
go  
  
SELECT d.name, d.compatibility_level  
    FROM sys.databases AS d  
    WHERE d.name = 'yourDatabase';  
go  
```  
  
 En el caso de una base de datos de SQL Server con el nivel de compatibilidad 120, la activación de la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 obliga al sistema a usar la versión 70 de la estimación de cardinalidad.  
  
 **Estimación de cardinalidad heredada:** En el caso de una base de datos de SQL Server con el nivel de compatibilidad 130, la versión 70 de la estimación de cardinalidad se puede activar con la instrucción [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
  
```tsql  
ALTER DATABASE
    SCOPED CONFIGURATION  
        SET LEGACY_CARDINALITY_ESTIMATION = ON;  
go  
  
SELECT name, value  
    FROM sys.database_scoped_configurations  
    WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
```  
 
 O, a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) `FORCE_LEGACY_CARDINALITY_ESTIMATION`.
 
 ```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01'; 
    OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'));  
```
 
 **Almacén de consultas:**desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, el almacén de consultas es una herramienta muy práctica para examinar el rendimiento de las consultas.  En [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] (SSMS.exe), en el **Explorador de objetos**, debajo del nodo de la base de datos, se muestra un nodo **Almacén de consultas** si el almacén de consultas está activado.  
  
```tsql  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE = ON;  
go  
  
SELECT  
        q.actual_state_desc AS [actual_state_desc-ofQueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
    FROM  
        sys.database_query_store_options  AS q;  
go  
  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE CLEAR;  
```  
  
 > [!TIP] 
 > Se recomienda instalar cada mes la versión más reciente de [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).  
  
 Otra opción para llevar un seguimiento del proceso de estimación de cardinalidad consiste en usar el evento extendido denominado **query_optimizer_estimate_cardinality**.  El siguiente código de ejemplo de T-SQL se ejecuta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Escribe un archivo .xel en C:\Temp\ (aunque la ruta de acceso se puede cambiar). Cuando abra el archivo .xel en SSMS, verá información detallada de forma muy sencilla.  
  
```tsql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
    ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
go  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    STATE = START;  --STOP;  
go  
```  
  
 Para obtener más información sobre los eventos extendidos adaptados para Base de datos SQL de Azure, vea [Eventos extendidos en Base de datos SQL](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).  
  
  
## <a name="steps-to-assess-the-ce-version"></a>Pasos para evaluar la versión de estimación de cardinalidad  
  
 Estos son los pasos que se pueden realizar para saber si alguna de las consultas más importantes tiene un peor rendimiento tras la estimación de cardinalidad más reciente. Algunos de estos pasos se llevan a cabo ejecutando código de ejemplo incluido en una sección anterior.  
  
1.  Abra [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. Asegúrese de que la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está establecida en el nivel de compatibilidad más alto disponible.  
  
2.  Realice los siguientes pasos preliminares:  
  
    1.  Abra [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)].  
  
    2.  Ejecute el código T_SQL para asegurarse de que la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está establecida en el nivel de compatibilidad más alto disponible.  
  
    3.  Asegúrese de que la configuración `LEGACY_CARDINALITY_ESTIMATION` de la base de datos está desactivada.  
  
    4.  BORRE el almacén de consultas. Por supuesto, asegúrese de que el almacén de consultas está activado.  
  
    5.  Ejecute la instrucción `SET NOCOUNT OFF;`.  
  
3.  Ejecute la instrucción `SET STATISTICS XML ON;`.  
  
4.  Ejecute la consulta importante.  
  
5.  En la pestaña **Mensajes** del panel de resultados, anote el número real de filas afectadas.  
  
6.  En la pestaña **Resultados** del panel de resultados, haga doble clic en la celda que contiene las estadísticas en formato XML. Se abre un plan de consulta gráfico.  
  
7.  Haga clic con el botón derecho en el primer cuadro del plan de consulta gráfico y, después, haga clic en **Propiedades**.  
  
8.  A fin de poder compararlos posteriormente con otra configuración, anote los valores de las siguientes propiedades:  
  
    -   **CardinalityEstimationModelVersion**.  
  
    -   **Número de filas estimado**.  
  
    -   **Costo de E/S estimado**y otras propiedades de *estimación* similares que tengan que ver con el rendimiento real más que con las predicciones de números de filas.  
  
    -   **Operación lógica** y **Operación física**. *Paralelismo* es un buen valor.  
  
    -   **Modo de ejecución real**. *Lote* es un buen valor, mejor que *Fila*.  
  
9. Compare el número estimado de filas con el número real de filas. ¿Existe una imprecisión de la estimación de cardinalidad de un 1 % (por encima o por debajo) o de un 10 %?  
  
10. Ejecute `SET STATISTICS XML OFF;`.  
  
11. Ejecute el código T-SQL para rebajar la base de datos un nivel de compatibilidad (por ejemplo, de 130 a 120).  
  
12. Vuelva a ejecutar todos los pasos no preliminares.  
  
13. Compare los valores de propiedad de la estimación de cardinalidad de ambos procesos.  
  
    - ¿Es el porcentaje de imprecisión con la nueva estimación de cardinalidad inferior que con la estimación de cardinalidad anterior?  
  
14. Por último, compare los distintos valores de propiedad de rendimiento de ambos procesos.  
  
    -   ¿Usó la consulta un plan diferente en cada una de las estimaciones de cardinalidad?  
  
    -   ¿Tuvo la consulta un rendimiento inferior con la estimación de cardinalidad más reciente?  
  
    -   A menos que la consulta muestre un mejor rendimiento y con un plan distinto en la estimación de cardinalidad anterior, lo más probable es que la estimación de cardinalidad más reciente sea la que más le convenga.  
  
    -   Pero si la consulta se ejecuta con un plan más rápido en la estimación de cardinalidad anterior, considere la posibilidad de obligar al sistema a usar el plan más rápido y omitir la estimación de cardinalidad. De este modo, dispondrá de la estimación de cardinalidad más reciente para todo y, al mismo tiempo, mantendrá el plan más rápido para el caso inusual.  
  
## <a name="how-to-activate-the-best-query-plan"></a>Cómo activar el mejor plan de consulta  
  
Supongamos que, con la nueva estimación de cardinalidad, se genera un plan de consulta más lento para la consulta. Estas son algunas opciones disponibles para activar el plan más rápido.  
  
El nivel de compatibilidad se podría establecer en un nivel inferior que el último disponible para toda la base de datos.  
  
- Así, se activaría la estimación de cardinalidad heredada, pero esto haría que todas las consultas se sometiesen a la estimación de cardinalidad anterior y menos precisa.  
  
- Es más, al establecer ese nivel de compatibilidad anterior también se pierden muchas de las fantásticas mejoras en el optimizador de consultas.  
  
Puede usar `LEGACY_CARDINALITY_ESTIMATION` para que toda la base de datos use la estimación de cardinalidad anterior (o solo una consulta específica) y conservar al mismo tiempo las mejoras en el optimizador de consultas.  
  
Para tener el mejor control posible, podría *obligar* al sistema SQL a usar el plan que se generó con la estimación de cardinalidad anterior durante las pruebas. Después de *asignar* un plan de su elección, puede configurar toda la base de datos de forma que use el nivel de compatibilidad y la estimación de cardinalidad más recientes. Pasemos a explicar esta opción.  
  
### <a name="how-to-force-a-particular-query-plan"></a>Cómo forzar un plan de consulta particular  
  
El almacén de consultas ofrece diferentes formas para obligar al sistema a usar un plan de consulta en particular:  
  
- Ejecute **sp_query_store_force_plan**.  
  
- En [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], expanda el nodo **Almacén de consultas**, haga clic con el botón derecho en **Consultas que más recursos consumen** y, después, haga clic en **Ver consultas que más recursos consumen**. La pantalla recoge los botones **Forzar plan** y **No forzar plan**.  
  
 Para obtener más información sobre el almacén de consultas, vea [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
  
## <a name="examples-of-ce-improvements"></a>Ejemplos de mejoras en la estimación de cardinalidad  
  
En esta sección se muestran consultas de ejemplo en las que se saca partido de las mejoras implementadas en la estimación de cardinalidad en versiones recientes. Se trata de información general que no precisa de ninguna acción por su parte.  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>Ejemplo A. La estimación de cardinalidad entiende que el valor máximo podría ser superior al de las últimas estadísticas recopiladas  
  
Supongamos que la última vez que se recopilaron estadísticas para OrderTable fue el 30/04/2016, cuando el valor máximo de OrderAddedDate era 30/04/2016. La estimación de cardinalidad para el nivel de compatibilidad 120 (y para niveles más altos) entiende que las columnas en OrderTable con datos *ascendentes* podrían tener valores mayores que el máximo registrado por las estadísticas. Este entendimiento mejora el plan de consulta para instrucciones SELECT de SQL como la siguiente.  
  
```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>Ejemplo B. La estimación de cardinalidad entiende que, a menudo, los predicados filtrados en una misma tabla se correlacionan  
  
En la siguiente instrucción SELECT podemos ver predicados filtrados en Model y ModelVariant. Deducimos de manera intuitiva que, cuando el modelo es "Xbox", hay una posibilidad de que ModelVariant sea "One", dado que Xbox tiene una variante que se llama One.  
  
La estimación de cardinalidad de nivel 120 entiende que podría haber una correlación entre las dos columnas de la misma tabla, Model y ModelVariant. La estimación de cardinalidad hace una estimación más precisa del número de filas que la consulta va a devolver, mientras que el optimizador de consultas genera un plan mucho mejor.  
  
```tsql  
SELECT Model, Purchase_Price  
    FROM dbo.Hardware  
    WHERE  
        Model  = 'Xbox'  AND  
        ModelVariant = 'One';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tablescc"></a>Ejemplo C. La estimación de cardinalidad ya no da por hecho ninguna correlación entre los predicados filtrados de tablas distintas. 
Las nuevas investigaciones exhaustivas en las cargas de trabajo y datos empresariales reales de hoy día han puesto de manifiesto que predicar filtros de tablas distintas no hace que se establezca ningún tipo de correlación entre sí. En la siguiente consulta, la estimación de cardinalidad da por hecho que no hay ninguna correlación entre s.type y r.date. Por tanto, hace una estimación más baja del número de filas devuelto.  
  
```tsql  
SELECT s.ticket, s.customer, r.store  
    FROM  
                   dbo.Sales    AS s  
        CROSS JOIN dbo.Returns  AS r  
    WHERE  
        s.ticket = r.ticket  AND  
        s.type   = 'toy'     AND  
        r.date   = '2016-05-11';  
```  
  
  
## <a name="see-also"></a>Vea también  
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  [Optimizar los planes de consulta con el estimador de cardinalidad de SQL Server 2014](http://msdn.microsoft.com/library/dn673537.aspx)  
 [Sugerencias de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
 [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md)


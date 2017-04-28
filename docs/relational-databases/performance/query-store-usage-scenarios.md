---
title: "Escenarios de uso del Almacén de consultas | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store, usage scenarios
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce278d494e2d5ab7dfc82e244a9d6b8821099cc0
ms.lasthandoff: 04/11/2017

---
# <a name="query-store-usage-scenarios"></a>Escenarios de uso del Almacén de consultas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  El Almacén de consultas se puede usar en un gran número de escenarios en los que es fundamental controlar y procurar un rendimiento de carga de trabajo de predicción. Estos son algunos ejemplos que se pueden tener en cuenta:  
  
-   Localizar y solucionar consultas con regresiones de elección del plan  
  
-   Identificar y ajustar las consultas que consumen más recursos  
  
-   Realizar pruebas A/B  
  
-   Mantener la estabilidad del rendimiento al actualizar a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   Identificar y mejorar las cargas de trabajo ad hoc  
  
## <a name="pinpoint-and-fix-queries-with-plan-choice-regressions"></a>Localizar y solucionar consultas con regresiones de elección del plan  
 Durante una ejecución de consultas normal, el optimizador de consultas puede decidir adoptar un plan diferente porque las entradas importantes ahora son distintas, ya sea porque la cardinalidad de los datos ha cambiado, porque se han creado, modificado o eliminado índices, porque se han actualizado estadísticas, etc.  En gran parte, el nuevo plan elegido será mejor o aproximadamente igual que el que se usó anteriormente. Sin embargo, hay casos en los que el nuevo plan es claramente peor. Es a esta situación a la que denominamos regresión de cambio de elección de plan. Antes de que existiera el almacén de consultas, este era un problema muy difícil de identificar y resolver, ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no proporcionaba un almacén de datos integrado donde los usuarios pudieran buscar los planes de ejecución usados en el tiempo.  
  
 Ahora, con el Almacén de consultas puede hacer lo siguiente rápidamente:  
  
-   Identificar todas las consultas cuyas métricas de ejecución se hayan degradado en el periodo de tiempo especificado (última hora, día, semana, etc.). Use la opción **Consultas devueltas** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para acelerar el análisis.  
  
-   Entre las consultas devueltas es muy fácil distinguir las que tenían varios planes y que se degradaron debido a una mala elección del plan. Use el panel **Resumen del plan** en **Consultas devueltas** para visualizar todos los planes de una consulta devuelta y su rendimiento de consulta en el tiempo.  
  
-   Forzar el plan anterior del historial si está confirmado que es mejor. Use el botón **Forzar plan** en **Consultas devueltas** para forzar el plan seleccionado para la consulta.  
  
 ![consultaDeAlmacénDeUso1](../../relational-databases/performance/media/query-store-usage-1.png "consultaDeAlmacénDeUso1")  
  
 Para ver una descripción detallada del escenario, consulte el blog [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) (Almacén de consultas: una caja negra de su base de datos).  
  
## <a name="identify-and-tune-top-resource-consuming-queries"></a>Identificar y ajustar las consultas que consumen más recursos  
 Aunque la carga de trabajo puede generar miles de consultas, normalmente solo unas pocas usan realmente la mayor parte de los recursos del sistema y, por tanto, requieren su atención. Entre las consultas que más recursos consumen suelen estar las consultas devueltas o aquellas que se pueden ajustar para mejorarlas.  
  
 La forma más sencilla de empezar a explorar es abrir **Principales consultas que consumen recursos** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  La interfaz de usuario se divide en tres paneles: un histograma con las consultas que consumen más recurso (izquierda), un resumen del plan para la consulta seleccionada (derecha) y un plan de consulta visual para el plan seleccionado (abajo). Haga clic en el botón **Configurar** para controlar la cantidad de consultas que quiere analizar y el intervalo de tiempo que le interesa. También puede elegir entre diferentes dimensiones de consumo de recursos (duración, CPU, memoria, E/S, número de ejecución) y la línea base (promedio, mínima, máxima, total, desviación estándar).  
  
 ![consultaDeAlmacénDeUso2](../../relational-databases/performance/media/query-store-usage-2.png "consultaDeAlmacénDeUso2")  
  
 Eche un vistazo al resumen del plan a la derecha para analizar el historial de ejecuciones y conocer los distintos planes y sus correspondientes estadísticas en tiempo de ejecución. Use el panel inferior para examinar los distintos planes o compararlos visualmente poniéndolos uno al lado del otro (para ello, use el botón Comparar).  
  
 Cuando identifique una consulta con un rendimiento deficiente, la acción dependerá de la naturaleza del problema:  
  
1.  Si la consulta se ejecutó con varios planes y el último plan es mucho peor que el anterior, puede usar el mecanismo de forzado de plan para procurar que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use siempre el mejor plan posible en futuras ejecuciones.  
  
2.  Compruebe si el optimizador sugiere que faltan índices en el plan XML. Si así es, cree el índice que falta y use el Almacén de consultas para evaluar el rendimiento de la consulta después de haber creado ese índice.  
  
3.  Asegúrese de que las estadísticas están actualizadas en las tablas subyacentes usadas por la consulta.  
  
4.  Asegúrese de que los índices usados por la consulta están desfragmentados.  
  
5.  Considere si merece la pena volver a escribir una consulta costosa. Por ejemplo, puede aprovechar las ventajas de la parametrización de consultas y reducir el uso de SQL dinámico. Implemente una lógica óptima al leer los datos (aplique el filtrado de datos en la base de datos, no en la aplicación).  
  
## <a name="ab-testing"></a>Realizar pruebas A/B  
 Use el Almacén de consultas para comparar el rendimiento de una carga de trabajo antes y después del cambio de aplicación que tiene previsto realizar.  La siguiente lista contiene ejemplos en los que se puede usar el Almacén de consultas para evaluar el impacto del cambio de entorno o aplicación en el rendimiento de la carga de trabajo:  
  
-   Implementar una nueva versión de la aplicación.  
  
-   Agregar nuevo hardware al servidor.  
  
-   Crear índices que faltan en las tablas a las que hacen referencia las consultas costosas.  
  
-   Aplicar una directiva de filtrado para la seguridad de nivel de fila. Para obtener más información, consulte [Optimizing Row Level Security with Query Store](http://blogs.msdn.com/b/sqlsecurity/archive/2015/07/21/optimizing-rls-performance-with-the-query-store.aspx)(Optimizar la seguridad de nivel de fila con el Almacén de consultas).  
  
-   Agregar versiones de sistema temporales a tablas que las aplicaciones de OLTP modifican con frecuencia.  
  
 En cualquiera de estos escenarios es válido el siguiente flujo de trabajo:  
  
1.  Ejecute la carga de trabajo con el Almacén de consultas antes de efectuar el cambio previsto para generar una base de rendimiento.  
  
2.  Realice el cambio de aplicación en el momento controlado de su elección.  
  
3.  Siga ejecutando la carga de trabajo el tiempo suficiente como para generar una imagen de rendimiento del sistema tras el cambio.  
  
4.  Compare los resultados de los pasos 1 y 3.  
  
    1.  Abra **Consumo general de base de datos** para conocer el impacto en toda la base de datos.  
  
    2.  Abra **Consultas que más recursos consumen** (o ejecute su propio análisis con [!INCLUDE[tsql](../../includes/tsql-md.md)]) para analizar el impacto del cambio en las consultas más importantes.  
  
5.  Decida si mantener el cambio o revertirlo si el nuevo rendimiento es inaceptable.  
  
 En la siguiente ilustración se muestra el análisis del Almacén de consultas (paso 4) cuando se crea un índice que falta. Abra el panel Resumen del plan en **Consultas que más recursos consumen** para obtener una vista de la consulta que debería verse afectada por la creación del índice:  
  
 ![consultaDeAlmacénDeUso3](../../relational-databases/performance/media/query-store-usage-3.png "consultaDeAlmacénDeUso3")  
  
 También puede comparar los planes anterior y posterior a la creación del índice poniéndolos uno al lado del otro (con la opción de barra de herramientas "Comparar los planes de la consulta seleccionada en una ventana independiente" que está marcada con un cuadrado rojo en la barra de herramientas).  
  
 ![consultaDeAlmacénDeUso4](../../relational-databases/performance/media/query-store-usage-4.png "consultaDeAlmacénDeUso4")  
  
 El plan anterior a la creación del índice (con el número 1, arriba) muestra una sugerencia de falta de índice y puede observar que Clustered Index Scan fue el operador más caro de la consulta (enmarcado en un rectángulo rojo).  
  
 El plan posterior a la creación del índice (con el número 15, abajo) tiene ahora Index Seek (Nonclustered), lo que reduce el costo total de la consulta y mejora el rendimiento (enmarcado en un rectángulo verde).  
  
 Según el análisis, probablemente lo más conveniente sea mantener el índice, ya que el rendimiento de la consulta ha mejorado.  
  
## <a name="keep-performance-stability-during-the-upgrade-to-sql-server-2016"></a>Mantener la estabilidad del rendimiento al actualizar a SQL Server 2016  
 Antes de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], los usuarios corrían el riesgo de sufrir una regresión del rendimiento al actualizar a la versión más reciente de la plataforma. Esto se debía a que la versión más reciente del optimizador de consultas se activaba inmediatamente después de que se instalaran los nuevos bits.  
  
 Desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , todos los cambios del optimizador de consultas están vinculados al `COMPATIBILITY_LEVEL`más reciente, por lo que los planes no se cambian en el momento de la actualización, sino cuando un usuario cambie `COMPATIBILITY_LEVEL` a la versión más reciente. Esta función, junto con el Almacén de consultas, confiere al usuario un enorme control sobre el rendimiento de las consultas en el proceso de actualización. En la siguiente imagen se muestra el flujo de trabajo de actualización recomendado:  
  
 ![consultaDeAlmacénDeUso5](../../relational-databases/performance/media/query-store-usage-5.png "consultaDeAlmacénDeUso5")  
  
1.  Actualice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin cambiar `COMPATIBILITY_LEVEL`. No dispondrá del optimizador de consultas más reciente, pero sí características de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] como el Almacén de consultas.  
  
2.  Habilite el Almacén de consultas: capture consultas y planes y establezca la base de rendimiento del `COMPATIBILITY_LEVEL`anterior. Permanezca en este paso el tiempo suficiente como para capturar todos los planes y obtener una base estable.  
  
3.  Avance al nivel de compatibilidad más reciente: exponga su carga de trabajo al optimizador de consultas más reciente y deje que cree posibles nuevos planes.  
  
4.  Use el Almacén de consultas para realizar correcciones de regresión y análisis, si bien la mayoría de las veces el nuevo optimizador de consultas debería generar mejores planes. Con todo, el Almacén de consultas le proporcionará una forma fácil de identificar las regresiones de elección del plan y de corregirlos mediante el mecanismo de forzado de plan.  
  
## <a name="identify-and-improve-ad-hoc-workloads"></a>Identificar y mejorar las cargas de trabajo ad hoc  
 Algunas cargas de trabajo no tienen consultas dominantes que se pueden ajustar para mejorar el rendimiento general de la aplicación. Estas cargas de trabajo se suelen caracterizar por un número relativamente grande de consultas diferentes, y todas ellas consumen parte de los recursos del sistema. Al ser únicas, estas consultas se ejecutan con poca frecuencia (normalmente una sola vez, de ahí la nomenclatura “ad hoc”), por lo que su consumo de tiempo de ejecución no es crítico. Por otro lado, dado que la aplicación genera nuevas consultas netas todo el tiempo, se dedica una parte significativa de los recursos del sistema a compilar consultas de una forma que no es óptima. Esta situación tampoco es ideal para el Almacén de consultas, dado que el elevado número de consultas y planes acapara el espacio que tiene reservado, lo que significa que el Almacén de consultas probablemente acabe en modo de solo lectura muy rápidamente. Si activó la **directiva de limpieza según el tamaño** ([muy recomendable](https://msdn.microsoft.com/library/mt604821.aspx) para mantener el almacén de consultas siempre en funcionamiento), el proceso en segundo plano limpiará las estructuras del almacén de consultas prácticamente todo el tiempo, lo que también consume muchos recursos del sistema.  
  
 La vista**Consultas que más recursos consumen** proporcionará un primer indicio de la naturaleza ad hoc de la carga de trabajo:  
  
 ![consultaDeAlmacénDeUso6](../../relational-databases/performance/media/query-store-usage-6.png "consultaDeAlmacénDeUso6")  
  
 Use la métrica **Recuento de ejecuciones** para analizar si las consultas principales son ad hoc (para ello, debe ejecutar el almacén de consultas con `QUERY_CAPTURE_MODE = ALL`). En el diagrama anterior, puede ver que el 90 % de **Principales consultas que consumen recursos** se ejecuta solo una vez.  
  
 Opcionalmente, puede ejecutar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] para obtener el número total de textos de consulta, consultas y planes en el sistema y conocer sus diferencias comparando sus query_hash y plan_hash:  
  
```  
/*Do cardinality analysis when suspect on ad-hoc workloads*/  
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
 Este es un posible resultado que puede obtener en el caso de cargas de trabajo con consultas ad hoc:  
  
 ![consultaDeAlmacénDeUso7](../../relational-databases/performance/media/query-store-usage-7.png "consultaDeAlmacénDeUso7")  
  
 El resultado de la consulta muestra que, a pesar del gran número de planes y consultas en el Almacén de consultas, sus query_hash y plan_hash no son realmente diferentes. Una relación entre textos de consulta únicos y query_hash únicos que esté muy por encima de 1 es indicativa de que esa carga de trabajo es una buena candidata para la parametrización, dado que la única diferencia entre las consultas es la constante literal (parámetro) que se proporciona como parte del texto de la consulta.  
  
 Normalmente, esta situación puede ocurrir si la aplicación genera consultas (en lugar de llamar a procedimientos almacenados o a consultas con parámetros) o si depende de marcos de trabajo de asignación relativos a objetos que generan consultas de forma predeterminada.  
  
 Si tiene el control del código de la aplicación, sopese la posibilidad de volver a escribir la capa de acceso a datos para que se usen procedimientos almacenados o consultas parametrizadas. Pese a todo lo anterior, esta situación también se puede mejorar considerablemente sin cambios en la aplicación. Basta con forzar la parametrización de consultas de toda la base de datos (todas las consultas) o de las plantillas de consulta individuales con el mismo query_hash.  
  
 El método de las plantillas de consulta individuales requiere crear una guía de plan:  
  
```  
  
/*Apply plan guide for the selected query template*/  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
 Una solución con guías de plan es más precisa, pero requiere más trabajo.  
  
 Si todas las consultas (o la mayoría de ellas) son aptas para la parametrización automática, cambiar `FORCED PARAMETERIZATION` para toda la base de datos puede ser una mejor opción:  
  
```  
  
/*Apply forced parameterization for entire database*/  
ALTER DATABASE <database name> SET PARAMETERIZATION  FORCED;  
```  
  
 Después de aplicar cualquiera de estos pasos, **Principales consultas que consumen recursos** mostrará una imagen distinta de la carga de trabajo.  
  
 ![consultaDeAlmacénDeUso8](../../relational-databases/performance/media/query-store-usage-8.png "consultaDeAlmacénDeUso8")  
  
 En algunos casos, la aplicación puede generar una gran cantidad de consultas diferentes que no son aptas para la parametrización automática. En ese caso, verá un gran número de consultas en el sistema, pero la relación entre las consultas únicas y los query_hash únicos está bastante próxima a 1.  
  
 En consecuencia, puede que convenga especificar 'optimize for ad hoc workloads' para no desperdiciar memoria caché con consultas que probablemente no vuelvan a ejecutarse. Para evitar que se capturen esas consultas en el Almacén de consultas, establezca `QUERY_CAPTURE_MODE` en `AUTO`.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
  
sp_configure 'optimize for ad hoc workloads', 1;  
GO  
RECONFIGURE;  
GO  
  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)  
  
  


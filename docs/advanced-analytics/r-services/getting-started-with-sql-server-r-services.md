---
title: "Introducci&#243;n a SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 32
---
# Introducci&#243;n a SQL Server R Services
 Un flujo de trabajo típico para compilar una solución de análisis avanzada comienza con la exploración de datos y el modelado predictivo, mientras que el científico de datos desarrolla modelos y scripts R que son eficaces para la tarea en cuestión. Después de que los modelos y scripts estén listos, se pueden implementar en producción e integrar con aplicaciones nuevas o existentes.   
  
SQL Server R Services está diseñado para ayudarle a completar estas tareas de ciencia de datos. Puede seguir trabajando con sus herramientas de R o SQL favoritas, pero escale el análisis a miles de millones de registros sin hardware adicional, mejore el rendimiento y evite movimientos de datos innecesarios. Ahora puede poner código R en producción sin tener que volver a escribirlo en otro idioma. También facilita el uso de R para cálculos estadísticos que podrían ser difíciles de implementar mediante SQL. Al mismo tiempo, puede sacar provecho de la eficacia de SQL Server para lograr el máximo rendimiento, con características como los índices de almacén de columnas y motor de base de datos en memoria.  
  
En las secciones siguientes, se proporciona una introducción de alto nivel a algunos flujos de trabajo analíticos típicos y sobre cómo habilitarlos con SQL Server R Services.  

> [!TIP] Vea este tutorial para comenzar rápido. Aprenderá cómo se podría usar el aprendizaje automático en una empresa de alquiler de esquís para predecir alquileres futuros y programar al personal para satisfacer la demanda.
> 
> [Compilar una aplicación inteligente con SQL Server y R](https://www.microsoft.com/sql-server/developer-get-started/r)


  
-   **Desarrollo**  
  
     Los científicos de datos suelen usar R para explorar datos y generar modelos predictivos desde su estación de trabajo con el IDE de R que elijan. Los científicos de datos iteran pruebas y ajustes hasta que consiguen un buen modelo predictivo. 
     
     Los clientes de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] proporcionan a los científicos de datos todas las herramientas que necesitan para experimentar y desarrollar soluciones. Estas herramientas incluyen el tiempo de ejecución de R, la biblioteca Intel Math Kernel Library para mejorar el rendimiento de las operaciones estándar de R y un conjunto de paquetes de R mejorados con los que puede ejecutarse código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Los científicos de datos pueden conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mover los datos al cliente para realizar un análisis local del modo habitual. En cambio, una solución más eficaz consiste en usar las API de **ScaleR** para enviar los cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], lo que evita tener que realizar los costosos y poco seguros movimientos de datos.  
  
     Para desarrollar soluciones en R, los científicos de datos pueden usar cualquier IDE basado en Windows que admita R, incluidos [R Tools para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) o RStudio.  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     Para obtener más información, consulte [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  

  
-   **Optimización**  
  
     Al analizar grandes conjuntos de datos con R, los científicos de datos suelen encontrarse con problemas de rendimiento y escalado, ya que la implementación en runtime comunes se realiza en un solo proceso y solo puede albergar los conjuntos de datos que caben en la memoria disponible en el equipo local. Para obtener un mejor rendimiento y trabajar con más datos, los científicos de datos pueden usar las API de **ScaleR** que se proporcionan como parte de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. El paquete **RevoScaleR** contiene implementaciones de algunas de las funciones de R más populares, que se han vuelto a diseñar para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y la escalabilidad mediante la inserción de cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que, normalmente, tiene mayor memoria y potencia de cálculo.  
  
     Para obtener más información, consulte [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
-   **Implementación**  
  
     Después de que el modelo o script R estén listos para usarse en producción, un desarrollador de bases de datos puede insertar el código o el modelo en procedimientos almacenados e invocar el código guardado de una aplicación. Almacenar y ejecutar código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene muchas ventajas: puede usar la cómoda interfaz de [!INCLUDE[tsql](../../includes/tsql-md.md)] y todos los cálculos realizados en la base de datos, con lo que se evita realizar movimientos de datos innecesarios. Puede usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para generar puntuaciones a partir de un modelo predictivo en producción, o bien devolver gráficos generados mediante R y presentarlos en una aplicación como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     Para optimizar aún más el código R insertado en procedimientos almacenados del sistema, se recomienda usar las API de paquetes [ScaleR](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-getting-started), que pueden operar en conjuntos de datos de gran tamaño. Estos paquetes admiten la funcionalidad de ejecución en la base de datos para poder realizar cálculos multiproceso y de núcleo múltiple.  
  
     Cuando necesite implementar código R en producción, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece lo mejor de los lenguajes R y SQL. Puede usar R para realizar cálculos estadísticos que son difíciles de implementar con SQL, pero aprovechando la eficacia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obtener el máximo rendimiento, mediante la implementación de características como el motor de base de datos en memoria y los índices de almacén de columnas.  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     Para obtener más información, consulte [Hacer operativo el código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
 
 > [!TIP]Obtenga más información sobre cómo puede integrar SQL Server con la ciencia de datos en este libro, disponible como descarga gratuita de Microsoft Virtual Academy: [Data Science with Microsoft SQL Server 2016](https://mva.microsoft.com/ebooks/) (Ciencia de datos con Microsoft SQL Server 2016)

-   **Administración y supervisión**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa una nueva arquitectura de extensibilidad que mantiene el motor de base de datos seguro y aísla las sesiones de R. También podrá controlar los usuarios que pueden ejecutar scripts de R y especificar qué bases de datos pueden acceder al código R. Puede controlar la cantidad de recursos asignados al runtime de R y, de este modo, evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.  
  
     Cuando se ejecutan trabajos de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también puede controlar y auditar los datos que usan los analistas, o bien programar trabajos y crear flujos de trabajo que contengan scripts R, al igual que haría con otros procedimientos almacenados.  
  
     Para obtener más información, consulte [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
  
-   **Integración**  
  
     Ya no tendrá que dedicar su presupuesto de TI a obtener las herramientas de empresa necesarias para trabajar con algún entorno de runtime de R externo. Puede trabajar en el entorno familiar de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y desarrollar soluciones de generación de informes y flujos de trabajo integrados mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     Para obtener más información, consulte [Crear flujos de trabajo que usan R en SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
  
## <a name="how-do-i-get-it"></a>¿Cómo lo consigo?  
   
  
+   **Instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o una versión posterior y habilitación de R Services (En base de datos)**  
  
    [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
  
-   **Configuración de una estación de trabajo cliente**  
  
     [Configurar un cliente de ciencia de datos](../../advanced-analytics/r-services/set-up-a-data-science-client.md)  
   
> [!TIP]   
>   
> ¿Necesita crear un servidor para trabajos de R pero no necesita SQL Server? Pruebe [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>Cómo ejecutar código de R mediante SQL Server R Services  
 Una vez completada la instalación, puede ejecutar código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al insertar R en los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] o al escribir scripts R ad hoc que funcionen con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Obtenga información sobre cómo llamar a código R con una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] y devolver los resultados en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
     [Uso de código de R en Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   Comprenda el flujo completo de creación de una solución de análisis avanzada y cómo implementarla mediante SQL Server R Services  
  
     [Tutorial integral de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   Obtenga información sobre cómo usar el paquete de RevoScaleR para el análisis escalable y de alto rendimiento y cómo insertar cálculos de R en el equipo con SQL Server  
  
     [Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   Inserte scripts R operativos en procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] para poder llamar a modelos para obtener predicciones, volver a entrenar modelos u obtener predicciones de aplicaciones  
  
     [Análisis avanzado en base de datos para desarrolladores de SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   Use [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y herramientas de inteligencia empresarial relacionadas en la pila de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para automatizar los procesos de aprendizaje automático. Es posible automatizar la preparación de los datos y la generación de informes mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]; muestre los trazados de R junto con otros informes por medio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o Power View.  
  
+ Más ejemplos, como plantillas de solución y código R de muestra  
   [SQL Server R Services Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Introducción a Microsoft R Server &#40;independiente&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  
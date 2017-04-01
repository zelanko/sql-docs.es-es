---
title: "Caracter&#237;sticas y tareas de SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# Caracter&#237;sticas y tareas de SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] combina la eficacia y flexibilidad del lenguaje R abierto con herramientas de nivel empresarial para el almacenamiento de datos y administración, desarrollo de flujo de trabajo, informes y visualización. Es compatible con las necesidades de los profesionales de cuatro datos diferentes y escenarios.  
  
## Científicos de datos: análisis, modelado y puntuación mediante R y SQL Server  
 Los científicos de datos podrán disfrutar de una amplia gama de herramientas de análisis de datos y aprendizaje automático, desde las conocidas plataformas de código abierto y Excel hasta costosos conjuntos de aplicaciones de estadística que requieren vastos conocimientos técnicos. Entre ellos, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] confiere ventajas exclusivas porque permite a los científicos de datos insertar los cálculos en la base de datos, con lo que se evita tener que mover los datos y se respetan las directivas de seguridad empresariales. Además, el código de R creado por los científicos de datos se puede implementar fácilmente en la fase de producción y las soluciones y herramientas empresariales conocidas pueden llamarlo de forma sencilla: aplicaciones basadas en bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , herramientas de generación de informes de inteligencia empresarial y paneles. Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], los científicos de datos pueden implementar y actualizar una solución de análisis al tiempo que se cumplen los requisitos de los estándares que rigen la administración de los datos empresariales, como la seguridad, la facilidad de implementación, administración y supervisión, y la auditoría del acceso.  
  
-   **Interfaz de usuario conocida.**  Desarrolle y pruebe sus soluciones con el entorno de desarrollo de R que prefiera.  
  
-   **Procesamiento en la base de datos.**  Ejecute código R y haga que los cálculos se realicen en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Así se elimina la necesidad de mover los datos.  
  
-   **Rendimiento y escalabilidad.**  Incluye escalable paquetes de R y las API, por lo que ya no está restringidos por la arquitectura de un único subproceso, el límite de memoria de R. Puede trabajar con grandes conjuntos de datos y cálculos multiproceso, núcleos múltiples, varios procesos.  
    
-   **Portabilidad del código.**  El mismo código de R que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos pueden ser fácilmente volver a usar en otros orígenes de datos, como Hadoop.  
  
 Para obtener información detallada sobre los conceptos y tareas relacionadas, vea [exploración de datos y modelado predictivo con R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
## Desarrolladores de bases de datos y aplicaciones: implementación de soluciones en R  
 A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. Estos profesionales trabajan con desarrolladores de aplicaciones, programadores de SQL y científicos de datos para diseñar soluciones, recomendar métodos de administración de datos, así como idear e implementar soluciones. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece numerosas ventajas para desarrolladores que trabajen con científicos de datos:  
  
-   **Interactuar con secuencias de comandos de R mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].**  Sus desarrolladores de informes, analistas y programadores de bases de datos podrán invocar scripts de R llamando a procedimientos almacenados del sistema. Si la solución utiliza agregaciones complejas o implica grandes conjuntos de datos, puede hacer cálculos ejecutar en bases de datos o utilizar una combinación de R y [!INCLUDE[tsql](../../includes/tsql-md.md)], en función de lo que proporciona el mejor rendimiento. La integración sin problemas con  [!INCLUDE[tsql](../../includes/tsql-md.md)] resulta de especial utilidad cuando tiene que ejecutar tareas reiteradamente en grandes cantidades de datos, como a la hora de generar puntuaciones de predicción de datos de producción.  
  
     La integración con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también se traduce en que puede ejecutar scripts de R desde cualquier aplicación que utilice [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por ejemplo, puede llamar fácilmente un procedimiento almacenado desde un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informe para invocar el script de R y generar un gráfico junto con las predicciones en el informe.  
  
-   **Rendimiento y escalabilidad.**  Aunque el lenguaje R abierto se sabe que tienen limitaciones, proporciona el paquete de RevoScaleR API [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pueden operar en conjuntos de datos grandes y beneficiarse de multiproceso, núcleos múltiples, varios procesos cálculos en base de datos.  
  
-   **Herramientas de administración y desarrollo estándar.**  No se requiere ninguna herramienta adicional para la administración o la implementación; es posible llamar a todos los trabajos de R invocando un procedimiento almacenado. Además, el mismo código de R que se ejecuta con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede utilizar con otros orígenes de datos, como Hadoop.  
  
 Para obtener información detallada sobre los conceptos y tareas relacionadas, vea [de funcionamiento de código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
## Administradores de bases de datos: administración de soluciones de análisis avanzados  
 Los administradores de bases de datos deben integrar prioridades y proyectos rivales en un único punto de contacto: el servidor de la base de datos. Deben proporcionar acceso a los datos no solo a los científicos de datos, sino a una amplia variedad de desarrolladores de informes, analistas empresariales y consumidores de datos empresariales. Además, deben hacerlo a la vez que mantienen los almacenes de datos de informes y operativos en buen estado. En las empresas, este profesional desempeña un papel esencial en la creación e implementación de una infraestructura eficaz para cultivar la ciencia de datos. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece numerosas ventajas para los administradores de bases de datos que respalden las iniciativas de ciencias de datos:  
  
-   **Securidad.**  La arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de R de la operación de la instancia de base de datos.  
  
     Puede especificar quién tiene permiso para ejecutar scripts de R y asegúrese de que los datos utilizados en los trabajos de R se administraban mediante los mismos roles de seguridad que se definen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Confiabilidad.**  Las sesiones de R se ejecutan en un proceso independiente para garantizar que el servidor sigue ejecutándose como de costumbre, aunque surja algún problema en dichas sesiones.  
  
-   **Gobierno de los recursos.**  Puede controlar la cantidad de recursos asignados al runtime de R y, de este modo, evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.  
  
 Para obtener información más detallada sobre las tareas y los conceptos relacionados, consulte [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
## Arquitectos y diseñadores ETL: creación de flujos de trabajo integrados que abarquen R y SQL Server  
 Los ingenieros de datos diseñan y crean soluciones ETL. Los arquitectos diseñan plataformas de datos que satisfacen necesidades empresariales rivales y complementarias. Dado que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está profundamente integrado con otras herramientas de Microsoft como inteligencia empresarial y la pila de almacenamiento de datos, nube empresarial y herramientas de movilidad y Hadoop, ofrece una serie de ventajas para el arquitecto de ingeniería o sistema de datos que desea promover análisis avanzado.  
  
-   **Amplio conjunto de herramientas de desarrollo conocidas.**  Cuando desarrolle soluciones de R, utilice [!INCLUDE[tsql](../../includes/tsql-md.md)] y procedimientos almacenados del sistema para rellenar conjuntos de datos, ejecutar trabajos de R u obtener predicciones. Se acabó el diseñar flujos de trabajo paralelos en herramientas de ciencias de datos; construya sus canalizaciones de datos en el entorno conocido de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     ¿Necesita utilizar datos en la nube? Compatibilidad con la factoría de datos y base de datos de SQL Azure facilita la transformar y administrar datos y orígenes de datos de nube de uso en flujos de trabajo simplemente como, por ejemplo para local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos.  
  
-   **Creación y administración de flujos de trabajo.**  Programar trabajos y crear flujos de trabajo que contiene secuencias de comandos de R, mediante procedimientos almacenados del sistema.  
  
 Para obtener información detallada sobre los conceptos y tareas relacionadas, consulte [creación de flujos de trabajo que R de uso en SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
## Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  
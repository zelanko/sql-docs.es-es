---
title: 'Aprendizaje automático de ciclo de vida y el proceso de equipo: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2218034dd6ac4cc3e7926b214c5c021815e57ed3
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432208"
---
# <a name="machine-learning-lifecycle-and-personas"></a>Roles y ciclo de vida de machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Proyectos de aprendizaje automático pueden ser complejos, ya que requieren las habilidades y colaboración de un conjunto dispar de los profesionales de TI. En este artículo se describe las tareas principales del ciclo de vida de aprendizaje de máquina, el tipo de los profesionales de datos que se ocupan de aprendizaje automático y cómo SQL Server es compatible con las necesidades.

> [!TIP]
> 
> Antes de comenzar en un proyecto de machine learning, se recomienda que revise las herramientas y procedimientos recomendados proporcionados por el [proceso de ciencia de datos de equipo de Microsoft](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), o TDSP. Este proceso se creó con consultores de Microsoft para consolidar las prácticas recomendadas de planificación y efectuar una iteración en los proyectos de aprendizaje automático de aprendizaje automático. El TDSP tiene sus raíces en estándares del sector como CRISP-DM, pero incorpora varias prácticas recientes como DevOps y visualización.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de Machine learning

Machine learning es un proceso complejo que afecta a todos los aspectos de los datos de la empresa y muchos proyectos de aprendizaje automático acaban tarda más tiempo y ser más compleja de lo previsto. Estas son algunas de las formas en que el aprendizaje automático requiere la compatibilidad de los profesionales de datos de la empresa:

+ Aprendizaje automático comienza con la identificación de los objetivos y las reglas de negocios.
+ Los profesionales de TI de Machine learning deben ser conscientes de las directivas para almacenar, extraer y datos de auditoría.
+ Es el siguiente conjunto de datos potencialmente aplicables.  Se deben identificar los orígenes de datos y los datos extraen de sensores y aplicaciones empresariales. 
+ La calidad de los esfuerzos de machine learning es sumamente dependiente no solo del tipo de datos que está disponibles, pero los procesos muy utilizados para extraer, procesamiento y almacenamiento de datos. 
+ Ningún proyecto de machine learning estaría completa sin una estrategia para informes y análisis y posiblemente compromiso del cliente y comentarios.

SQL Server ayuda a cerrar muchas de las brechas entre los profesionales de datos empresariales y expertos en aprendizaje automático:

+ Los datos pueden almacenarse localmente o en la nube
+ SQL Server está integrado en cada fase de procesamiento de datos de empresa, incluido reporting y ETL
+ SQL Server admite la seguridad de los datos, redundancia de datos y auditoría
+ Proporciona la regulación de recursos

## <a name="data-scientists"></a>Científicos de datos

Los científicos de datos usan una variedad de herramientas de análisis de datos y aprendizaje automático, que abarcan desde Excel o plataformas de código abierto gratuitas, hasta costosos conjuntos de estadísticos que requieren vastos conocimientos técnicos. Sin embargo, mediante R o Python con SQL Server proporciona algunas ventajas exclusivas en comparación con estas herramientas tradicionales:

+ Puede desarrollar y probar una solución mediante el entorno de desarrollo que prefiera y luego implementar el código de R o Python como parte del código de T-SQL.
+ Mover los cálculos complejos portátil de los científicos de datos y en el servidor, evitar el movimiento de datos para cumplir con las directivas de seguridad empresarial.
+ Se han mejorado de escala y rendimiento a través de paquetes de R especiales y las API. Ya no están restringidos por la arquitectura de un único subproceso, enlazada a memoria de R y puede trabajar con grandes conjuntos de datos y cálculos multiproceso, multinúcleo, varios procesos.
+ Portabilidad del código: Pueden ejecutar soluciones en SQL Server o en Hadoop o en Linux, mediante [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). El código una vez, implementar en cualquier parte.

## <a name="application-and-database-developers"></a>Desarrolladores de aplicaciones y base de datos

A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. El desarrollador de la base de datos funciona con los desarrolladores de aplicaciones, los desarrolladores de SQL y científicos de datos diseñar soluciones, recomendar métodos de administración de datos y crear o implementar soluciones.

Integración con SQL Server ofrece numerosas ventajas para desarrolladores de datos:

+ Los científicos de datos pueden trabajar en RStudio, mientras que el desarrollador de datos implementa la solución con SQL Server Management Studio. Volver a codificar no más de las soluciones de R o Python.
+ Optimizar sus soluciones utilizando lo mejor de Python, R y T-SQL. Se pueden ejecutar operaciones complejas en grandes conjuntos de datos mucho más eficaz usar SQL Server que en R. Aproveche el conocimiento de los profesionales de TI de sus base de datos para mejorar el rendimiento de las soluciones de aprendizaje automático, mediante el uso de los índices de almacén de columnas en memoria, y agregaciones mediante operaciones basadas en conjuntos SQL. 
+ Sin esfuerzo automatizar las tareas que deben ejecutarse varias veces en grandes cantidades de datos, como generar puntuaciones de predicción en los datos de producción. 
+ Acceso con parámetros de script de R o Python desde cualquier aplicación que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Simplemente llame a un procedimiento almacenado para entrenar un modelo, generar un trazado o generar predicciones.
+ Las API pueden transmitir grandes conjuntos de datos y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de.

Para obtener información sobre las tareas relacionadas, consulte:
+ [Operacionalización del código de R](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de base de datos

Los administradores de bases de datos deben integrar prioridades y proyectos opuestos en un único punto de contacto: el servidor de la base de datos. Deben proporcionar acceso a los datos no solo a los científicos de datos, sino a una amplia variedad de desarrolladores de informes, analistas empresariales y consumidores de datos empresariales. Además, deben hacerlo a la vez que mantienen los almacenes de datos de informes y operativos en buen estado. En las empresas, estos profesionales desempeñan un papel esencial en la creación e implementación de una infraestructura eficaz para cultivar la ciencia de datos. 

SQL Server proporciona características exclusivas para el Administrador de base de datos que debe admitir el rol de ciencia de datos:

+ Seguridad de SQL Server: La arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de script externo desde el funcionamiento de la instancia de base de datos. Puede especificar quién tiene permiso para ejecutar scripts de machine learning y usar roles de base de datos para administrar los paquetes.

+ Sesiones de R y Python se ejecutan en un proceso independiente para asegurarse de que el servidor sigue ejecutándose como de costumbre, incluso si el script externo encuentra problemas.

+ Regulación de recursos mediante SQL Server le permite controlar la memoria y los procesos asignados a los tiempos de ejecución externos, para evitar que unos cálculos masivos pongan en peligro el rendimiento global del servidor.

Para obtener información sobre las tareas relacionadas, consulte:
+ [Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Ingenieros de datos y arquitectos

Los arquitectos diseñar flujos de trabajo integrados que abarcan todos los aspectos del ciclo de vida de machine learning. Los ingenieros de datos diseñar y compilación soluciones ETL y determinan cómo optimizar las tareas de ingeniería de características para el aprendizaje automático. La plataforma de datos global debe diseñarse para equilibrar las necesidades del negocio competencia.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mantiene una estrecha integración con otras herramientas de Microsoft (como la pila de almacenamiento de datos e inteligencia empresarial), con herramientas de movilidad y de nube empresarial y con Hadoop, ofrece un amplio abanico de ventajas a los ingenieros de datos o arquitectos del sistema que quieran promover los análisis avanzados.

+ Llamar a cualquier script de Python o R mediante el uso de procedimientos almacenados del sistema, para rellenar conjuntos de datos, generar gráficos u obtener predicciones. No más diseñar flujos de trabajo paralelos en ciencia de datos y herramientas de ETL. Compatibilidad con Azure Data Factory y Azure SQL Database hace más fácil de usar orígenes de datos en la nube en los flujos de trabajo de aprendizaje automático.

+ Para la programación y administración de tareas de aprendizaje automático, use los flujos de trabajo de automatización estándar en SQL Server, en función de Integration Services, Agente SQL o Azure Data Factory. O bien, use el [características de puesta en marcha](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) en Machine Learning Server.

Para obtener información sobre las tareas relacionadas, consulte:

+ [Crear flujos de trabajo de aprendizaje automático en SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)


---
title: Equipos de aprendizaje del ciclo de vida y el proceso del equipo | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ca7d0acf3097ec031cba5f3a7245d5594b7927bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>Ciclo de vida de aprendizaje de máquina y roles
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Proyectos de aprendizaje de máquina pueden ser complejos, ya que requieren los conocimientos teóricos y colaboración de un conjunto dispares de profesionales de TI. Este artículo describen las tareas principales en el ciclo de vida de aprendizaje de máquina, el tipo de profesionales de datos que actúan en aprendizaje automático y cómo SQL Server es compatible con las necesidades.

> [!TIP]
> 
> Antes de empezar a trabajar en un proyecto de aprendizaje automático, se recomienda que revise las herramientas y procedimientos recomendados proporcionados por el [proceso de ciencia de datos de equipo de Microsoft](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), o TDSP. Este proceso se creó con consultores de TI de Microsoft para consolidar las prácticas recomendadas en planeación y efectuar una iteración en los proyectos de aprendizaje automático de aprendizaje automático. El TDSP tiene sus raíces en estándares del sector como CRISP-DM, pero incorpora las prácticas recientes como DevOps y visualización.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de aprendizaje de máquina

Aprendizaje automático es un proceso complejo que toca todos los aspectos de los datos de la empresa, y muchos proyectos de aprendizaje de máquina terminan tarda más tiempo y son más complejos de lo esperado. Estas son algunas de las formas que aprendizaje automático requiere la compatibilidad con los profesionales de datos de la empresa:

+ Aprendizaje automático comienza con la identificación de los objetivos y las reglas de negocios.
+ Los profesionales de aprendizaje de máquina deben tener en cuenta las directivas para almacenar, extraer y datos de auditoría.
+ Recopilación de datos potencialmente aplicables es el siguiente.  Se deben identificar los orígenes de datos, y ha extraen los datos apropiados de sensores y aplicaciones empresariales. 
+ La calidad de los esfuerzos de aprendizaje de máquina depende en gran no solo el tipo de datos que están disponibles, pero los procesos muy utilizados para extraer, procesamiento y almacenamiento de datos. 
+ Ningún proyecto de aprendizaje automático estaría completa sin una estrategia para informes y análisis y posiblemente compromiso del cliente y comentarios.

SQL Server ayuda a salvar muchos de los espacios entre los expertos de aprendizaje de máquina y profesionales de datos de empresa:

+ Los datos pueden ser almacenada localmente o en la nube
+ SQL Server se integra en cada fase de procesamiento de datos de empresa, incluidos los informes y ETL
+ SQL Server admite la seguridad de los datos, la redundancia de los datos y la auditoría
+ Proporciona la regulación de recursos

## <a name="data-scientists"></a>Científicos de datos

Científicos de datos utilizar diversas herramientas de análisis de datos y aprendizaje automático, desde Excel o plataformas de código abierto gratuitas, a los conjuntos de estadísticos costosos que requieren vastos conocimientos técnicos. Sin embargo, el uso de R o Python con SQL Server proporciona algunas ventajas exclusivas en comparación con estas herramientas tradicionales:

+ Se puede desarrollar y probar una solución mediante el entorno de desarrollo de su elección, a continuación, implementar el código de R o Python como parte del código de T-SQL.
+ Mover cálculos complejos portátil de los científicos de datos y en el servidor, lo que evita el movimiento de datos para cumplir con las directivas de seguridad corporativas.
+ Rendimiento y escalabilidad se han mejorado mediante API y paquetes de R especial. Ya no están restringidas por la arquitectura de un único subproceso, el límite de memoria de R y poder trabajar con grandes conjuntos de datos y cálculos multiproceso, varios núcleos, varios procesos.
+ Portabilidad del código: pueden ejecutar soluciones en SQL Server, o en Hadoop o en Linux, con [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Una vez el código, implementar en cualquier lugar.

## <a name="application-and-database-developers"></a>Desarrolladores de aplicaciones y bases de datos

A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. El desarrollador de la base de datos funciona con los desarrolladores de aplicaciones, los desarrolladores de SQL y científicos de datos para diseñar soluciones, recomendar métodos de administración de datos y diseñar o implementar soluciones.

Integración con SQL Server ofrece numerosas ventajas para desarrolladores de datos:

+ Los científicos de datos pueden trabajar en RStudio, mientras que el programador de datos implementa la solución con SQL Server Management Studio. Volver a codificar no más de las soluciones de R o Python.
+ Optimizar sus soluciones mediante lo mejor de T-SQL, R y Python. Se pueden ejecutar operaciones complejas en grandes conjuntos de datos mucho más eficaz usar SQL Server que en R. aprovechar el conocimiento de los profesionales de la base de datos para mejorar el rendimiento de las soluciones de aprendizaje de máquina, mediante el uso de índices columnstore en memoria, y agregaciones mediante operaciones basadas en conjuntos SQL. 
+ Sin esfuerzo automatizar las tareas que deben ejecutarse varias veces en grandes cantidades de datos, como generar puntuaciones de predicción de datos de producción. 
+ Acceso con parámetros de script de R o Python desde cualquier aplicación que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Llame a un procedimiento almacenado para entrenar un modelo, generar un gráfico o generar predicciones.
+ Pueden transmitir grandes conjuntos de datos y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de API.

Para obtener información sobre las tareas relacionadas, vea:
+ [El código de R en marcha](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de base de datos

Los administradores de bases de datos deben integrar prioridades y proyectos opuestos en un único punto de contacto: el servidor de la base de datos. Deben proporcionar acceso a los datos no solo a los científicos de datos, sino a una amplia variedad de desarrolladores de informes, analistas empresariales y consumidores de datos empresariales. Además, deben hacerlo a la vez que mantienen los almacenes de datos de informes y operativos en buen estado. En las empresas, estos profesionales desempeñan un papel esencial en la creación e implementación de una infraestructura eficaz para cultivar la ciencia de datos. 

SQL Server proporciona características únicas para el Administrador de base de datos que debe admitir las iniciativas de ciencias de datos:

+ Seguridad de SQL Server: la arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de script externo desde el funcionamiento de la instancia de base de datos. Puede especificar quién tiene permiso para ejecutar scripts de aprendizaje de máquina y usar roles de base de datos para administrar paquetes.

+ Sesiones de R y Python se ejecutan en un proceso independiente para asegurarse de que el servidor sigue ejecutándose como de costumbre, incluso si el script externo encuentra problemas.

+ La regulación de recursos mediante SQL Server le permite controlar la memoria y los procesos asignados a los tiempos de ejecución externos, para evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.

Para obtener información sobre las tareas relacionadas, vea:
+ [Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Ingenieros de arquitectos y datos

Los arquitectos diseñan flujos de trabajo integrados que abarcan todos los aspectos del ciclo de vida de aprendizaje de máquina. Ingenieros de datos diseñan y crear soluciones ETL y determinan cómo optimizar las tareas de ingeniería de característica para el aprendizaje automático. La plataforma de datos global debe diseñarse para equilibrar las necesidades del negocio competencia.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mantiene una estrecha integración con otras herramientas de Microsoft (como la pila de almacenamiento de datos e inteligencia empresarial), con herramientas de movilidad y de nube empresarial y con Hadoop, ofrece un amplio abanico de ventajas a los ingenieros de datos o arquitectos del sistema que quieran promover los análisis avanzados.

+ Llamar a cualquier script de Python o R utilizando procedimientos almacenados del sistema, para rellenar conjuntos de datos, generar gráficos u obtener predicciones. No hay más diseñar flujos de trabajo paralelos en herramientas ETL y la ciencia de datos. Compatibilidad para Data Factory de Azure y base de datos de SQL Azure hace más fácil de usar orígenes de datos en la nube en los flujos de trabajo de aprendizaje automático.

+ Para programar y administración de las tareas de aprendizaje automático, usar flujos de trabajo de automatización estándar en SQL Server, en función de Integration Services, Agente SQL o Data Factory de Azure. O bien, use la [características de puesta en marcha](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) en el servidor de aprendizaje de máquina.

Para obtener información sobre las tareas relacionadas, vea:

+ [Crear flujos de trabajo de aprendizaje de máquina en SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)


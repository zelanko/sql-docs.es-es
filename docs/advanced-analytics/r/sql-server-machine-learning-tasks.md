---
title: "Tareas de aprendizaje de máquina SQL Server | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: es-es
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>Tareas de aprendizaje automático SQL Server

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] combina la eficacia y flexibilidad del lenguaje R de código abierto con herramientas de nivel empresarial para ofrecer características de administración y almacenamiento de datos, de desarrollo de flujos de trabajo, y de generación y visualización de informes. Este tema describe el ciclo de vida y cómo SQL Server es compatible con las necesidades de cuatro profesionales de datos diferentes que sean enagged en aprendizaje automático de aprendizaje de automático.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de aprendizaje automático

Aprendizaje automático no es una tarea a corto plazo, pero en su lugar un proceso a largo plazo que entra en contacto con todos los aspectos de los datos de la empresa. Aprendizaje automático comienza con la identificación de los objetivos empresariales y las reglas y recopilación de datos de sensores y aplicaciones empresariales. Aprendizaje automático dependen en gran medida en procesos de extracción, el procesamiento y almacenamiento de datos y es cada vez más importante al considerar las directivas para almacenar, extraer y datos de auditoría. Por último, el aprendizaje automático ahora es un importante Component de estrategias para informes y análisis, así como compromiso del cliente y comentarios.



SQL Server es ideal para encajar en aprendizaje automático, ya que une muchos de los espacios en el proceso de aprendizaje automático:

+ Funciona en local o en la nube
+ Integrado en cada fase de procesamiento de datos de enterprise, incluida la inteligencia empresarial
+ Admite la seguridad de datos mejoradas
+ Proporciona la regulación de recursos y auditoría

## <a name="data-professionals-and-how-they-use-machine-learning"></a>Datos profesionales y cómo se aprendizaje automático de uso

### <a name="data-scientists"></a>Científicos de datos

Los científicos de datos tienen acceso a una variedad de herramientas de análisis de datos y aprendizaje automático, desde Excel o plataformas de código abierto gratuitas, a los conjuntos de estadísticos costosos que requieren vastos conocimientos técnicos. Sin embargo, la integración con SQL Server proporciona ventajas exclusivas:

+ Desarrolle y pruebe sus soluciones con el entorno de desarrollo de R que prefiera.
+ Insertar cálculos en la base de datos evita el movimiento de datos mientras se respetan las directivas de seguridad empresariales.
+ Rendimiento y escalabilidad se han mejorado mediante API y paquetes de R especial. Ya no están restringidas por la arquitectura de un único subproceso, el límite de memoria de R y poder trabajar con grandes conjuntos de datos y cálculos multiproceso, varios núcleos, varios procesos.
+ Código R puede ser implementado en producción y llama a paneles, aplicaciones, otras bases de datos y herramientas empresariales fácilmente.
+ Pueden implementar y actualizar una solución de análisis al tiempo que satisface los requisitos de los estándares para la administración de datos empresariales, incluida la seguridad y auditoría de acceso a los científicos de datos
+ Portabilidad del código: fácilmente volver a usar el código de R con otros orígenes de datos, como Hadoop

### <a name="application-and-database-developers"></a>Los programadores de la base de datos y aplicaciones

A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. Estos profesionales trabajan con desarrolladores de aplicaciones, programadores de SQL y científicos de datos para diseñar soluciones, recomendar métodos de administración de datos, así como idear e implementar soluciones. 

Integración con SQL Server ofrece estas ventajas para desarrolladores de datos que trabajen con aprendizaje automático:

+ Utilice herramientas conocidas para interactuar con scripts de R. Permitir que los científicos de datos trabajen en RStudio mientras el programador de datos implementa la solución con SQL Server Management Studio. Volver a codificar no más de las soluciones de R o Python.
+ Optimizar al mezclar y hacer coincidir SQL y R, o SQL y Python. Muchas veces, las operaciones complejas en grandes conjuntos de datos se pueden ejecutar mucho más eficaz con características de SQL Server, como columnstoreindexes en memoria, o muy rápidos agregados en T-SQL. Utilice un lenguaje de aprendizaje automático siempre que tenga sentido y SQL para mover y procesar los datos.
+ Sin esfuerzo automatizar las tareas que deben ejecutarse varias veces en grandes cantidades de datos, como generar puntuaciones de predicción de datos de producción.
+ Ejecutar script de R o Python desde cualquier aplicación que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Llame a un procedimiento almacenado para crear un modelo con parámetros, generar un gráfico complejo o generar predicciones.
+ El **RevoScaleR** y **revoscalepy** pueden operar en conjuntos de datos grandes y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de API.

Para obtener información sobre las tareas relacionadas, vea:
+ [Operacionalización del código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de base de datos

Los administradores de bases de datos deben integrar prioridades y proyectos opuestos en un único punto de contacto: el servidor de la base de datos. Deben proporcionar acceso a los datos no solo a los científicos de datos, sino a una amplia variedad de desarrolladores de informes, analistas empresariales y consumidores de datos empresariales. Además, deben hacerlo a la vez que mantienen los almacenes de datos de informes y operativos en buen estado. En las empresas, estos profesionales desempeñan un papel esencial en la creación e implementación de una infraestructura eficaz para cultivar la ciencia de datos. 

SQL Server proporciona características únicas para el Administrador de base de datos que debe admitir las iniciativas de ciencias de datos:

+ Seguridad de SQL Server: la arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de script externo desde el funcionamiento de la instancia de base de datos. Puede especificar quién tiene permiso para ejecutar scripts de aprendizaje de máquina y quién puede instalar nuevos paquetes de R, mediante roles de base de datos.

+ Sesiones de R y Python se ejecutan en un proceso independiente para asegurarse de que el servidor sigue ejecutándose como de costumbre, incluso si el script externo encuentra problemas.

+ La regulación de recursos mediante SQL Server le permite controlar la memoria y los procesos asignados a los tiempos de ejecución externos, para evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.

Para obtener información sobre las tareas relacionadas, vea:
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>Arquitectos y diseñadores ETL

Los arquitectos diseñan flujos de trabajo integrados que abarcan todos los aspectos del ciclo de vida de aprendizaje de máquina. Ingenieros de datos diseñar y crear soluciones ETL y determinar cómo optimizar la ingeniería de característica empleado tareas forman parte del proceso de aprendizaje automático. A menudo, la plataforma de datos global debe diseñarse para equilibrar las necesidades empresariales rivales y complementarias.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mantiene una estrecha integración con otras herramientas de Microsoft (como la pila de almacenamiento de datos e inteligencia empresarial), con herramientas de movilidad y de nube empresarial y con Hadoop, ofrece un amplio abanico de ventajas a los ingenieros de datos o arquitectos del sistema que quieran promover los análisis avanzados.

+ Herramientas de desarrollo conocidas para desarrollar soluciones de R y Python. Se puede llamar a cualquier script de Python o R mediante procedimientos almacenados del sistema, para rellenar conjuntos de datos, generar gráficos u obtener predicciones. No hay más diseñar flujos de trabajo paralelos en herramientas ETL y la ciencia de datos. Compatibilidad con Data Factory de Azure y base de datos de SQL Azure resulta más fácil transformar y administrar datos y usar orígenes de datos en la nube en los flujos de trabajo de aprendizaje automático.

+ La programación y administración usando las características de puesta en marcha de Microsoft R Server.

Para obtener información sobre las tareas relacionadas, vea:

+ [Crear flujos de trabajo que usan R en SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)



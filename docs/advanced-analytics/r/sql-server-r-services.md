---
title: SQL Server del equipo aprendizaje y R Services (In-Database) | Documentos de Microsoft
ms.date: 03/16/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: ''
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Active
ms.openlocfilehash: f84f61721bca14a78694a9df6c7af8b7f7d74ea7
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server del equipo aprendizaje y R Services (en bases de datos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Una instalación de base de datos de aprendizaje automático funciona en el contexto de una instancia de motor de base de datos de SQL Server, proporcionar soporte de script externo de R y Python para los datos residentes en la instancia de SQL Server. Dado que aprendizaje automático se integra con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.

Dado que el motor de base de datos es de varias instancias, puede instalar más de una instancia en bases de datos análisis de, o incluso más antiguos y más recientes versiones en paralelo. Incluyen opciones [Machine Learning Services (In-Database) de SQL Server de 2017](../install/sql-machine-learning-standalone-windows-install.md) con R y Python, o [SQL Server 2016 R Services (In-Database)](../install/sql-r-standalone-windows-install.md) con solo R. 

También se pueden instalar componentes de aprendizaje de máquina como instancia independiente [servidores independientes](r-server-standalone.md). Por lo general, se recomienda que trate (independiente) y (en bases de datos) instalaciones como mutuamente exclusivos para evitar la contención de recursos, pero si tiene suficientes recursos, no hay ninguna prohibición en instalar ambos en el mismo equipo físico.

## <a name="choosing-between-in-database-and-standalone-analytics"></a>Elegir entre análisis independiente y en bases de datos

Descripción de los requisitos de desarrollo puede ayudarle a elegir entre (en bases de datos) y se aproxime (independiente). Un servidor independiente es más fácil de configurar y administrar si desea tener una flexibilidad máxima en cómo se utiliza, o si desea conectarse a una variedad de orígenes de datos fuera de SQL Server. 

Análisis en bases de datos están diseñados para la integración profunda con datos de SQL Server. Puede escribir consultas de T-SQL que llamar a funciones de R o Python y ejecutan el script en SQL Server Management Studio o cualquier herramienta o aplicación se usa para T-SQL externo o incrustado. Si tiene que ejecutar código R o Python [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mediante procedimientos almacenados o mediante el servidor SQL Server de la instancia como el [contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context), debe instalar análisis en bases de datos. Esta opción proporciona seguridad de máximo de los datos y la integración con herramientas de SQL Server.

Tanto en bases de datos y servidores independientes pueden aliviar las restricciones de memoria y procesamiento de código abierto R y Python. Ambas opciones incluyen los mismos paquetes y herramientas, con la capacidad para cargar y procesar grandes cantidades de datos en varios núcleos y agrupar los resultados en una única salida consolidada. Las funciones y los algoritmos están diseñados para escalabilidad y utilidad: entrega de análisis predictivos, modelo estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial de aprendizaje de automático de vanguardia ingeniería y compatible con Microsoft. 

## <a name="components-of-an-in-database-installation"></a>Componentes de una instalación de base de datos

SQL Server 2016 solo es R. SQL Server 2017 admite R y Python. La tabla siguiente describen las características de cada versión. Salvo el servicio Launchpad de SQL Server, esta tabla es idéntica al proporcionado en el [artículo de servidor independiente](r-server-standalone.md).

| Componente | Description |
|-----------|-------------|
| Servicio SQL Server Launchpad | Un servicio que administra las comunicaciones entre los tiempos de ejecución de R y Python externos y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. |
| Paquetes de R | [RevoScaleR](revoscaler-overview.md) es la biblioteca principal para R escalable con funciones de manipulación de datos, transformación, visualzation y análisis.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, análisis de imágenes y análisis de opiniones. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) web de ofertas de implementación de servicio (en SQL Server 2017). <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) es para especificar las consultas MDX en R.|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Utilice siempre la versión de MRO agrupado en el programa de instalación. |
| Herramientas de R | Ventanas de la consola de R y símbolo del sistema son herramientas estándares en una distribución de R. Puede encontrarlos en \Program Server\140\R_SERVER\bin\x64 de SQL. |
| Ejemplos de R y secuencias de comandos |  Paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que pueda crear y ejecutar script con datos previamente instalados. Mire para ellos \Program SQL Server\140\R_SERVER\library\datasets y \library\RevoScaleR. |
| Paquetes de Python | [revoscalepy](../python/what-is-revoscalepy.md) es la biblioteca principal para Python ampliables con funciones de manipulación de datos, transformación, visualzation y análisis. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, análisis de imágenes y análisis de opiniones.  |
| Herramientas de Python | La herramienta de línea de comandos integrada de Python es útil para pruebas ad hoc y tareas. La herramienta se encuentra en \Program Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esenciales. |
| Las secuencias de comandos y ejemplos de Python | Al igual que con R, Python incluye conjuntos de datos integrados y secuencias de comandos. Buscar los datos revoscalepy en \Program SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente entrenados en R y Python | Modelos previamente entrenados son compatibles y se puede usar en un servidor independiente, pero no se puede instalar mediante el programa de instalación de SQL Server. El programa de instalación para el servidor de aprendizaje de máquina de Microsoft proporciona los modelos, que puede instalar de forma gratuita. Para obtener más información, consulte [instalar previamente entrenada modelos de aprendizaje automático en SQL Server](install-pretrained-models-sql-server.md). |

## <a name="get-started-step-by-step"></a>Introducción paso a paso

Iniciar el programa de instalación, adjuntar los archivos binarios a la herramienta de desarrollo que prefiera y escribir su primera secuencia de comandos.

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

Instalar cualquiera de estas versiones:

+ [Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R Services (en bases de datos) - R solo](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Configurar las herramientas de desarrollo para usar los archivos binarios del servidor de aprendizaje de máquina. Para obtener más información acerca de Python, consulte [archivos binarios de Python de vínculo](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obtener instrucciones sobre cómo conectar en R Studio, consulte [utilizando diferentes versiones de R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) y seleccione la herramienta C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. También puede intentar [R Tools para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

Los científicos de datos utilizan normalmente R o Python en su propia estación de trabajo portátil o de desarrollo, para explorar datos y generar y ajustar modelos predictivos hasta que consigue un buen modelo predictivo. 

Con funciones analíticas en bases de datos en SQL Server, no es necesario que cambie este proceso. Una vez completada la instalación, puede ejecutar código R o Python en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tanto local como remotamente:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Usar el IDE prefiere**. Los clientes de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] proporcionan a los científicos de datos todas las herramientas que necesitan para experimentar y desarrollar soluciones. Estas herramientas incluyen el tiempo de ejecución de R, la biblioteca Intel Math Kernel Library para mejorar el rendimiento de las operaciones estándar de R y un conjunto de paquetes de R mejorados con los que puede ejecutarse código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

+ **Trabajar de forma local como remota**. Los científicos de datos pueden conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mover los datos al cliente para realizar un análisis local del modo habitual. Sin embargo, una solución mejor es usar el **RevoScaleR** o **revoscalepy** API para insertar los cálculos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo, evitar el movimiento de datos costosos y poco seguros.

+ **Incruste scripts de R o Python en [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados**. Cuando el código está totalmente optimizado, inclúyala en un procedimiento almacenado para evitar movimientos de datos innecesarios y optimizar las tareas de procesamiento de datos.

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Llamar a funciones de R o Python desde script T-SQL:
  
  + [R: Usar el código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R: Análisis avanzado en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python: Ejecutar Python mediante T-SQL](../tutorials/run-python-using-t-sql.md)
  + [Python: Análisis avanzado en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Elegir el mejor lenguaje para la tarea. R es más adecuado para realizar cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en conjunto sobre datos, aprovechan la eficacia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Usar el motor de base de datos en memoria para realizar cálculos muy rápidos a través de las columnas.

### <a name="step-4-optimize-your-solution"></a>Paso 4: Optimizar la solución

Cuando el modelo está listo para escalar de datos empresariales, los científicos de datos a menudo funciona con el programador de DBA o SQL para optimizar los procesos, como:

+ Ingeniería de características
+ Recopilación de datos y transformación de datos
+ Puntuaciones

Tradicionalmente científicos de datos con R han tenido problemas con el rendimiento y la escalabilidad, especialmente cuando se usa el conjunto de datos grande. Eso es porque la implementación en tiempo de ejecución común es de subproceso único y puede dar cabida a los conjuntos de datos que caben en la memoria disponible en el equipo local. Integración con servicios de aprendizaje de máquina de SQl Server proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**: paquete de R esta contiene implementaciones de algunas de las funciones de R más populares, rediseñadas para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y la escalabilidad mediante la inserción de cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que, normalmente, tiene mayor memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python, disponible en SQL Server 2017, implementa las funciones más populares en RevoScaleR, por ejemplo, los contextos de proceso remoto y el procesamiento distribuyen de muchos algoritmos que admiten.

**Recursos**

+ [Caso práctico de rendimiento](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R y optimización de datos](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>Paso 5: Implementar y consumir

Después de la secuencia de comandos o el modelo está listo para su uso en producción, un desarrollador de la base de datos puede incrustar el código o el modelo en un procedimiento almacenado, para que el código de R o Python guardado se puede llamar desde una aplicación. Almacenar y ejecutar código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene muchas ventajas: puede usar la cómoda interfaz de [!INCLUDE[tsql](../../includes/tsql-md.md)] y todos los cálculos realizados en la base de datos, con lo que se evita realizar movimientos de datos innecesarios.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Seguro y extensible**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] utiliza una nueva arquitectura de extensibilidad que mantiene el motor de base de datos segura y aísla las sesiones de R y Python. También tiene control sobre los usuarios que pueden ejecutar scripts, y puede especificar qué bases de datos pueden obtener acceso al código. Puede controlar la cantidad de recursos asignados al tiempo de ejecución, para evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.

+ **Programación y auditoría**. Cuando se ejecutan los trabajos de script externo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede controlar y auditar los datos utilizados por los científicos de datos. También puede programar trabajos y crear flujos de trabajo que contiene scripts de R o Python externos, al igual que haría programar cualquier otro trabajo de T-SQL o procedimiento almacenado.

Para aprovechar las ventajas de las características de seguridad y administración de recursos de SQL Server, el proceso de implementación puede incluir estas tareas:

+ Convertir yourcode a una función que se puede ejecutar de forma óptima en un procedimiento almacenado
+ Configurar la seguridad y el bloqueo utilizados por una tarea determinada de paquetes
+ Habilitar el regulador de recursos (requiere la edición Enterprise)

**Recursos**

+ [Regulador de recursos para R](resource-governance-for-r-services.md)
+ [Administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md)

## <a name="see-also"></a>Vea también

 [SQL Server del equipo aprendizaje y R Server (independiente)](sql-server-r-services.md)

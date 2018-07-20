---
title: SQL Server Machine Learning y R Services (In-Database) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 05a2a17988912d7066b0d9f6bf398b889a3cd882
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174782"
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server Machine Learning y R Services (en bases de datos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Una instalación de base de datos de aprendizaje automático funciona dentro del contexto de una instancia de motor de base de datos de SQL Server, proporcione soporte de script externo de R y Python para datos residentes en la instancia de SQL Server. Dado que machine learning se integra con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede mantener análisis cerca de los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.

Dado que el motor de base de datos es de varias instancias, puede instalar más de una instancia de análisis en bases de datos, o incluso más antiguos y más recientes versiones side-by-side. Incluyen opciones [SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-standalone-windows-install.md) con R y Python, o [SQL Server 2016 R Services (In-Database)](../install/sql-r-standalone-windows-install.md) con simplemente R. 

También se pueden instalar componentes de aprendizaje automático como instancia independiente del [servidores independientes](r-server-standalone.md). Por lo general, se recomienda tratar (independiente) y (en bases de datos) instalaciones como mutuamente exclusivos para evitar la contención de recursos, pero si tiene suficientes recursos, no hay ninguna prohibiciones frente a instalación ambos en el mismo equipo físico.

## <a name="choosing-between-in-database-and-standalone-analytics"></a>Elegir entre realizar análisis en bases de datos e independiente

Descripción de los requisitos de desarrollo puede ayudarle a elegir entre (In-Database) y se aproxime (independiente). Un servidor independiente es más fácil de configurar y administrar si desea obtener la máxima flexibilidad en cómo se utiliza, o si desea conectarse también a una variedad de orígenes de datos fuera de SQL Server. 

Análisis en bases de datos están diseñados para la integración profunda con datos de SQL Server. Puede escribir consultas de T-SQL que llamar a funciones de R o Python y ejecutan el script de SQL Server Management Studio o cualquier herramienta o aplicación se usa para T-SQL externo o incrustado. Si necesita ejecutar código R o Python en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya sea mediante el uso de procedimientos almacenados o mediante el uso de SQL Server de la instancia como el [contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context), debe instalar análisis en bases de datos. Esta opción proporciona seguridad máxima de datos e integración con herramientas de SQL Server.

Tanto en bases de datos y servidores independientes pueden aliviar las restricciones de memoria y procesamiento de código abierto R y Python. Ambas opciones incluyen los mismos paquetes y herramientas, con la capacidad de cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una única salida consolidada. Los algoritmos y las funciones están diseñados para el escalado y utilidad: entrega de análisis predictivo, modelado estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial de aprendizaje de automático de vanguardia diseñada y compatibles con Microsoft. 

## <a name="components-of-an-in-database-installation"></a>Componentes de una instalación de base de datos

SQL Server 2016 solo es R. SQL Server 2017 admite R y Python. En la tabla siguiente se describe las características de cada versión. Salvo el servicio Launchpad de SQL Server, esta tabla es idéntica al proporcionado en el [artículo de servidor independiente](r-server-standalone.md).

| Componente | Descripción |
|-----------|-------------|
| Servicio Launchpad de SQL Server | Un servicio que administra las comunicaciones entre los tiempos de ejecución de R y Python externo y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. |
| Paquetes de R | [RevoScaleR](revoscaler-overview.md) es la biblioteca principal de R escalable con funciones de manipulación de datos, transformación, visualzation y análisis.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) web de ofertas de implementación de servicio (en SQL Server 2017). <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) sirve para especificar las consultas MDX en R.|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Utilice siempre la versión de MRO agrupado en el programa de instalación. |
| Herramientas de R | Símbolos del sistema y las ventanas de la consola de R son herramientas estándares en una distribución de R. Puede encontrarlos en \Program files\Microsoft Server\140\R_SERVER\bin\x64 SQL. |
| Ejemplos de R y las secuencias de comandos |  Paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que se puede crear y ejecutar el script con datos previamente instalado. Examine para ellos \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets y \library\RevoScaleR. |
| Paquetes de Python | [revoscalepy](../python/what-is-revoscalepy.md) es la biblioteca principal para Python escalables con funciones de manipulación de datos, transformación, visualzation y análisis. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto.  |
| Herramientas de Python | La herramienta de línea de comandos de Python integrada es útil para pruebas ad hoc y tareas. Encontrar la herramienta en \Program files\Microsoft Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esencial. |
| Secuencias de comandos y ejemplos de Python | Al igual que con R, Python incluye conjuntos de datos integrados y secuencias de comandos. Encontrar los datos de revoscalepy en \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente entrenados en R y Python | Modelos previamente entrenados son compatibles y se pueden usar en un servidor independiente, pero no instalarlas a través del programa de instalación de SQL Server. El programa de instalación de Microsoft Machine Learning Server proporciona los modelos, que puede instalar de forma gratuita. Para obtener más información, consulte [instalar previamente entrenada modelos de aprendizaje automático en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="get-started-step-by-step"></a>Introducción paso a paso

Comience con el programa de instalación, adjuntar los archivos binarios a la herramienta de desarrollo que prefiera y escribir la primera secuencia de comandos.

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

Instale cualquiera de estas versiones:

+ [SQL Server 2017 Machine Learning Services (en bases de datos)](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R Services (en bases de datos) - R solo](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Configurar las herramientas de desarrollo para usar los archivos binarios de Machine Learning Server. Para obtener más información acerca de Python, consulte [binarios de Python de vínculo](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obtener instrucciones sobre cómo conectar en R Studio, consulte [con diferentes versiones de R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) y elija la herramienta C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. También puede probar [R Tools para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

Científicos de datos normalmente usan R o Python en su propia estación de trabajo portátil o desarrollo, para explorar datos y crear y ajustar modelos predictivos hasta que se logra un buen modelo predictivo. 

Con análisis en bases de datos en SQL Server, no hay ninguna necesidad de cambiar este proceso. Una vez completada la instalación, puede ejecutar código R o Python en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local o remota:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Usar el IDE que prefiera**. Los clientes de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] proporcionan a los científicos de datos todas las herramientas que necesitan para experimentar y desarrollar soluciones. Estas herramientas incluyen el tiempo de ejecución de R, la biblioteca Intel Math Kernel Library para mejorar el rendimiento de las operaciones estándar de R y un conjunto de paquetes de R mejorados con los que puede ejecutarse código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

+ **Trabajar de forma local o remota**. Los científicos de datos pueden conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mover los datos al cliente para realizar un análisis local del modo habitual. Sin embargo, una solución mejor es usar el **RevoScaleR** o **revoscalepy** API para enviar los cálculos a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo, evitar el movimiento de datos costosos y poco seguros.

+ **Insertar scripts de R o Python en [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados**. Cuando el código está totalmente optimizado, bien, ajústelo en un procedimiento almacenado para evitar el movimiento de datos innecesarios y optimizar las tareas de procesamiento de datos.

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Llamar a funciones de R o Python desde dentro de la secuencia de comandos de T-SQL:
  
  + [R: Usar el código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R: Análisis avanzado en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python: Ejecutar Python mediante T-SQL](../tutorials/run-python-using-t-sql.md)
  + [Python: Análisis avanzado en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Elegir el mejor lenguaje para la tarea. R es más adecuado para cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en datos, aproveche la eficacia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Utilizar el motor de base de datos en memoria para los cálculos muy rápidos a través de las columnas.

### <a name="step-4-optimize-your-solution"></a>Paso 4: Optimizar la solución

Cuando el modelo está listo para crecer con datos empresariales, los científicos de datos a menudo funciona con el desarrollador DBA o SQL para optimizar los procesos, como:

+ Ingeniería de características
+ Ingesta de datos y transformación de datos
+ Puntuaciones

Tradicionalmente los científicos de datos mediante R han tenido problemas de rendimiento y escalabilidad, especialmente cuando se usa el conjunto de datos grande. Eso es porque la implementación en tiempo de ejecución común es de subproceso único y puede dar cabida a solo esos conjuntos de datos que caben en la memoria disponible en el equipo local. Integración con SQl Server Machine Learning Services proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**: paquete de R esta contiene implementaciones de algunas de las funciones de R más populares, rediseñadas para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y la escalabilidad mediante la inserción de cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que, normalmente, tiene mayor memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python, disponible en SQL Server 2017, implementa las funciones más populares de RevoScaleR, por ejemplo, los contextos de cálculo remoto y el procesamiento distribuyen de muchos algoritmos que admiten.

**Recursos**

+ [Caso práctico de rendimiento](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R y optimización de datos](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>Paso 5: Implementación y consumo

Después de la secuencia de comandos o el modelo está listo para su uso en producción, un desarrollador de la base de datos podría incrustar el código o el modelo en un procedimiento almacenado, para que el código de R o Python guardado puede llamarse desde una aplicación. Almacenar y ejecutar código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene muchas ventajas: puede usar la cómoda interfaz de [!INCLUDE[tsql](../../includes/tsql-md.md)] y todos los cálculos realizados en la base de datos, con lo que se evita realizar movimientos de datos innecesarios.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Seguro y extensible**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] utiliza una nueva arquitectura de extensibilidad que mantiene el motor de base de datos segura y aísla las sesiones de R y Python. También tiene control sobre los usuarios que pueden ejecutar scripts, y puede especificar qué bases de datos pueden tener acceso a código. Puede controlar la cantidad de recursos asignados al tiempo de ejecución, para evitar que unos cálculos masivos pongan en peligro el rendimiento global del servidor.

+ **Programación y auditoría**. Cuando se ejecutan los trabajos de script externo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede controlar y auditar los datos utilizados por los científicos de datos. También puede programar trabajos y crear flujos de trabajo que contiene scripts de R o Python externos, al igual que haría programar cualquier otro trabajo de Transact-SQL o procedimiento almacenado.

Para aprovechar las ventajas de las características de seguridad y administración de recursos de SQL Server, el proceso de implementación podría incluir estas tareas:

+ Convertir yourcode a una función que se puede ejecutar de forma óptima en un procedimiento almacenado
+ Configurar la seguridad y bloqueo de los paquetes utilizados por una tarea determinada
+ Habilitar regulación de recursos (requiere la edición Enterprise)

**Recursos**

+ [Regulación de recursos para R](resource-governance-for-r-services.md)
+ [Administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md)

## <a name="see-also"></a>Vea también

 [SQL Server Machine Learning y R Server (independiente)](sql-server-r-services.md)

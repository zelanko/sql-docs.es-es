---
title: Información general sobre Machine Learning Services de SQL Server (R, Python)
description: Información general de la característica Machine Learning Services en SQL Server, donde puede integrar Python y R con datos relacionales para la ciencia de datos y el modelado estadístico, modelos de aprendizaje automático, análisis predictivo, visualización de datos, etc.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/24/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4ab4cd7c93cfd1a98a819a849e643d590450cd28
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714670"
---
# <a name="sql-server-machine-learning-services-r-python"></a>SQL Server Machine Learning Services (R, Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services es una característica de SQL Server, que se usa para ejecutar scripts de R y Python en la base de datos. La característica incluye los [paquetes de Microsoft R y Python](#components) para el análisis predictivo y el aprendizaje automático de alto rendimiento. Los datos relacionales se pueden usar en scripts de R y Python a través de procedimientos almacenados, script T-SQL que contiene instrucciones de R y Python, o código R y Python que contiene T-SQL.

En Azure SQL Database, [Machine Learning Services (con R)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) se encuentra actualmente en versión preliminar pública.

## <a name="bring-compute-power-to-the-data"></a>Llevar la potencia de proceso a los datos

La propuesta de valor clave de Machine Learning Services es la potencia de sus paquetes de R y Python de la empresa para ofrecer análisis avanzados a escala, y la capacidad de llevar cálculos y procesamiento a la ubicación de los datos, lo que elimina la necesidad de extraer datos. la red. Esto proporciona varias ventajas:

+ Seguridad de datos. La ejecución de la ejecución de R y Python más cerca del origen de datos evita el movimiento de datos excesivo o inseguro.
+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las innovaciones recientes en las bases de datos, como las tablas en memoria, hacen resúmenes y agregaciones, y son un complemento perfecto para la ciencia de datos.
+ Facilidad de implementación e integración. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]es el punto central de operaciones para muchas otras tareas y aplicaciones de administración de datos. Mediante el uso de datos que residen en la base de datos o en el almacenamiento de informes, se asegura de que los datos usados por las soluciones de aprendizaje automático son coherentes y actualizados. 
+ Eficacia en la nube y en el entorno local. En lugar de procesar los datos en las sesiones de R o Python, puede confiar en las canalizaciones de datos empresariales que incluyen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y Azure data factory. Los informes de análisis o de resultados son sencillos a través de Power BI o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].

Si usan la combinación adecuada de SQL y R para distintas tareas de procesamiento y análisis de datos, los científicos de datos y los desarrolladores lograrán ser más productivos.

<a name="components"></a>

## <a name="components"></a>Componentes

SQL Server admite R y Python. En la tabla siguiente se describen los componentes de.

| Componente | Descripción |
|-----------|-------------|
| Servicio de SQL Server Launchpad | Servicio que administra las comunicaciones entre los tiempos de ejecución de R y Python externos y la instancia del motor de base de datos. |
| Paquetes de R | [**RevoScaleR**](r/ref-r-revoscaler.md) es la biblioteca principal para R. las funciones escalables de esta biblioteca están entre las más usadas. En estas bibliotecas se encuentran las transformaciones y la manipulación de datos, el resumen estadístico, la visualización y muchas formas de modelado y análisis. Además, las funciones de estas bibliotecas distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para el procesamiento en paralelo, con la capacidad de trabajar en fragmentos de datos que el motor de cálculo coordina y administra.  <br/>[**MicrosoftML (R)** ](r/ref-r-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. <br/>[**sqlRUtils**](r/ref-r-sqlrutils.md) proporciona funciones auxiliares para colocar scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutar el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**olapr**](r/ref-r-olapr.md) es para compilar o ejecutar una consulta MDX en un script de R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Use siempre la versión de MRO instalada por el programa de instalación. |
| Herramientas de R | Las ventanas de la consola de r y los símbolos del sistema son herramientas estándar en una distribución de R.  |
| Ejemplos y scripts de R |  Los paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que pueda crear y ejecutar scripts con datos preinstalados. |
| Paquetes de Python | [**revoscalepy**](python/ref-py-revoscalepy.md) es la biblioteca principal para Python escalable con funciones para la manipulación, transformación, visualización y análisis de datos. <br/>[**microsoftml (Python)** ](python/ref-py-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones.  |
| Herramientas de Python | La herramienta de línea de comandos de Python integrada es útil para las pruebas y tareas ad hoc.  |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esenciales. |
| Ejemplos y scripts de Python | Al igual que con R, Python incluye scripts y conjuntos de datos integrados.  |
| Modelos previamente entrenados en R y Python | Los modelos previamente entrenados se crean para casos de uso específicos y los mantiene el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados tal cual para puntuar la opinión positiva negativa en el texto o para detectar características en las imágenes, con las nuevas entradas de datos que proporcione. Los modelos se ejecutan en Machine Learning Services, pero no se pueden instalar a través de SQL Server instalación. Para obtener más información, consulte [instalación de modelos de aprendizaje automático entrenados previamente en SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Usar el MLS de SQL

Los desarrolladores y analistas suelen tener código que se ejecuta sobre una instancia de SQL Server local. Al agregar Machine Learning Services y habilitar la ejecución de scripts externos, tiene la capacidad de ejecutar código de R y Python en SQL Server modalidades: incluir scripts en procedimientos almacenados, almacenar modelos en una tabla de SQL Server o combinar funciones T-SQL y R o Python en las consultas.

La ejecución del script se encuentra dentro de los límites del modelo de seguridad de datos: los permisos en la base de datos relacional son la base del acceso a datos en el script. Un usuario que ejecute un script de R o Python no debe ser capaz de usar ningún dato al que no pueda tener acceso ese usuario en una consulta SQL. Necesita los permisos de lectura y escritura de la base de datos estándar, además de un permiso adicional para ejecutar el script externo. Los modelos y el código que se escriben para los datos relacionales se incluyen en procedimientos almacenados, se serializan en un formato binario y se almacenan en una tabla, o se cargan desde el disco si se serializa la secuencia de bytes sin formato en un archivo.

El enfoque más común para el análisis en bases de datos es usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), pasando el script de R o Python como parámetro de entrada.

Las interacciones de cliente y servidor clásicas son otro enfoque. Desde cualquier estación de trabajo cliente que tenga un IDE, puede instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) o las [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)y, a continuación, escribir código que inserte la ejecución (denominada "contexto de *cálculo remoto*") en datos y operaciones en un SQL Server remoto. 

Por último, si usa un [servidor independiente](r/r-server-standalone.md) y la edición para desarrolladores, puede compilar soluciones en una estación de trabajo cliente con las mismas bibliotecas e intérpretes y, a continuación, implementar el código de producción en SQL Server Machine Learning Services (en base de datos). 

## <a name="how-to-get-started"></a>Cómo empezar

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

+ [SQL Server Machine Learning Services (in-Database)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Los científicos de datos suelen usar R o Python en su propia estación de trabajo de desarrollo o portátil, para explorar los datos y compilar y ajustar los modelos predictivos hasta que se logre un buen modelo predictivo. Con el análisis de bases de datos en SQL Server, no es necesario cambiar este proceso. Una vez completada la instalación, puede ejecutar código de R o Python en SQL Server de forma local y remota.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Use el IDE que prefiera**. Puede vincular las bibliotecas de R y Python a la herramienta de desarrollo que prefiera. Para obtener más información, consulte [configuración de herramientas de R](r/set-up-a-data-science-client.md) y configuración de herramientas de [Python](python/setup-python-client-tools-sql.md).  

+ **Trabajar de forma remota o local**. Los científicos de datos pueden conectarse a SQL Server y llevar los datos al cliente para su análisis local, como de costumbre. Sin embargo, una solución mejor es usar las API de **RevoScaleR** o **revoscalepy** para enviar los cálculos al equipo SQL Server, evitando un movimiento de datos costoso y poco seguro.

+ **Inserte scripts de R o Python en SQL Server procedimientos almacenados**. Cuando el código está totalmente optimizado, inclúyalo en un procedimiento almacenado para evitar el movimiento de datos innecesario y optimizar las tareas de procesamiento de datos.

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir el primer script

Llame a las funciones de R o Python desde el script T-SQL:

+ [R: Aprenda a usar análisis en bases de datos con R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: Tutorial de un extremo a otro con R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python Ejecución de Python con T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python Aprendizaje de análisis en base de datos con Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Elija el mejor idioma para la tarea. R es la mejor opción para los cálculos estadísticos que son difíciles de implementar con SQL. En el caso de las operaciones basadas en conjuntos en los datos, aproveche el potencial de SQL Server para obtener el máximo rendimiento. Usar el motor de base de datos en memoria para cálculos muy rápidos en columnas.

### <a name="step-4-optimize-your-solution"></a>Paso 4: Optimizar la solución

Cuando el modelo está listo para escalar en los datos empresariales, el científico de datos suele trabajar con el DBA o el desarrollador de SQL para optimizar procesos como:

+ Ingeniería de características
+ Ingesta de datos y transformación de datos
+ Puntuaciones

Tradicionalmente, los científicos de datos que usan R tenían problemas con el rendimiento y la escala, especialmente cuando se usa un conjunto de datos grande. Esto se debe a que la implementación en tiempo de ejecución común es de subproceso único y solo puede alojar los conjuntos de datos que caben en la memoria disponible en el equipo local. La integración con SQL Server Machine Learning Services proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**: Este paquete de R contiene implementaciones de algunas de las funciones de R más populares, que se han rediseñado para proporcionar paralelismo y escalado. El paquete también incluye funciones que mejoran el rendimiento y la escala mediante la inserción de cálculos en el SQL Server equipo, que suele tener mucha más memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python implementa las funciones más populares en RevoScaleR, como contextos de cálculo remotos y muchos algoritmos que admiten el procesamiento distribuido.

Para obtener más información sobre el rendimiento, vea este [caso práctico de rendimiento](r/performance-case-study-r-services.md) y la [optimización de datos y R](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Paso 5: Implementación y consumo

Una vez que el script o el modelo estén listos para su uso en producción, un desarrollador de bases de datos podría incrustar el código o el modelo en un procedimiento almacenado para que se pueda llamar al código de R o Python guardado desde una aplicación. Almacenar y ejecutar código de R desde SQL Server tiene muchas ventajas: puede usar la práctica SQL Server interfaz y todos los cálculos se realizan en la base de datos, evitando el movimiento de datos innecesario.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Seguro y extensible**. SQL Server usa una nueva arquitectura de extensibilidad que mantiene el motor de base de datos seguro y aísla las sesiones de R y Python. También tiene control sobre los usuarios que pueden ejecutar scripts y puede especificar las bases de datos a las que se puede tener acceso mediante código. Puede controlar la cantidad de recursos asignados al tiempo de ejecución para evitar que los cálculos masivos cocomprometan el rendimiento general del servidor.

+ **Programación y auditoría**. Cuando se ejecutan trabajos de scripts externos en SQL Server, puede controlar y auditar los datos utilizados por los científicos de datos. También puede programar trabajos y crear flujos de trabajo que contengan scripts de R o Python externos, de la misma manera que programaría cualquier otro trabajo o procedimiento almacenado de T-SQL.

Para aprovechar las ventajas de la administración de recursos y las características de seguridad de SQL Server, el proceso de implementación puede incluir estas tareas:

+ Convertir el código en una función que se puede ejecutar de forma óptima en un procedimiento almacenado
+ Configurar la seguridad y bloquear los paquetes utilizados por una tarea determinada
+ Habilitar la regulación de recursos (requiere la edición Enterprise)

Para obtener más información, consulte [regulación de recursos para r](r/resource-governance-for-r-services.md) y [r administración de paquetes para SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="portability-and-related-products"></a>Portabilidad y productos relacionados

La portabilidad de su código personalizado de R y Python se dirige a través de la distribución de paquetes e intérpretes integrados en varios productos. Los mismos paquetes que se distribuyen en SQL Server también están disponibles en otros productos y servicios de Microsoft, lo que incluye una versión que no es de SQL llamada [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/). 

Los clientes gratuitos que incluyen nuestros intérpretes de R y Python son [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) y las [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

En Azure, los paquetes e intérpretes de R y Python de Microsoft también están disponibles en Azure Machine Learning y en servicios de Azure como [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)y [Azure virtual machines](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). El [Data Science Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) incluye una estación de trabajo de desarrollo totalmente equipada con herramientas de varios proveedores, así como las bibliotecas e intérpretes de Microsoft.

## <a name="see-also"></a>Vea también

[Instalar SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)

---
title: R y Python de Machine Learning Services en SQL Server | Microsoft Docs
description: R en SQL Server y Python en SQL Server, la integración con datos relacionales para ciencia de datos y modelado estadístico, modelos de aprendizaje automático, análisis predictivo, visualización de datos y mucho más.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cf67348b703677035435e54c323334478a1dfdf4
ms.sourcegitcommit: a083e9d59e2014a06cda9138b7e17c17ecab90e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2018
ms.locfileid: "44343120"
---
# <a name="machine-learning-services-r-python-in-sql-server-2017"></a>Machine Learning Services (R, Python) en SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017 Machine Learning Services es un complemento a una instancia del motor de base de datos, utilizado para ejecutar código R y Python en SQL Server. Código se ejecuta en un marco de extensibilidad, aislada de los procesos del motor principal, pero totalmente disponible para datos relacionales como procedimientos almacenados, como script de Transact-SQL que contiene instrucciones de R o Python o como código de R o Python con T-SQL. 

Si usó anteriormente [SQL Server 2016 R Services](r/sql-server-r-services.md), Machine Learning Services en SQL Server 2017 es la próxima generación de soporte técnico de R, con las versiones actualizadas de base R, RevoScaleR, MicrosoftML, y otras bibliotecas incorporaron en 2016.

La propuesta de valor de clave de Machine Learning Services es la potencia de su empresa R y paquetes de Python para ofrecer análisis avanzado a escala y la capacidad de poner los cálculos y procesamiento de donde residen los datos, lo que elimina la necesidad de extraer los datos a través de la red.

## <a name="components"></a>Components

SQL Server 2017 admite R y Python. En la tabla siguiente se describe los componentes.

| Componente | Descripción |
|-----------|-------------|
| Servicio Launchpad de SQL Server | Un servicio que administra las comunicaciones entre los tiempos de ejecución de R y Python externo y la instancia del motor de base de datos. |
| Paquetes de R | [**RevoScaleR** ](r/revoscaler-overview.md) es la biblioteca principal para funciones escalables de R. en esta biblioteca se encuentran entre los más usados. Muchas formas de modelado y análisis y manipulación, resumen estadístico, visualización y transformaciones de datos se encuentran en estas bibliotecas. Además, las funciones de estas bibliotecas distribución automáticamente las cargas de trabajo entre núcleos disponibles para el procesamiento en paralelo, con la capacidad de trabajar en fragmentos de datos que se coordina y administra el motor de cálculo.  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto. <br/>[**sqlRUtils** ](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) proporciona funciones auxiliares para colocar los scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutando el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**olapR** ](r/how-to-create-mdx-queries-using-olapr.md) es para compilar o ejecutar una consulta MDX en el script de R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Utilice siempre la versión de MRO instalado el programa de instalación. |
| Herramientas de R | Símbolos del sistema y las ventanas de la consola de R son herramientas estándares en una distribución de R.  |
| Ejemplos de R y las secuencias de comandos |  Paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que se puede crear y ejecutar el script con datos previamente instalado. |
| Paquetes de Python | [**revoscalepy** ](python/what-is-revoscalepy.md) es la biblioteca principal para Python escalables con funciones de manipulación de datos, transformación, visualización y análisis. <br/>[**microsoftml (Python)** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto.  |
| Herramientas de Python | La herramienta de línea de comandos de Python integrada es útil para pruebas ad hoc y tareas.  |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esencial. |
| Secuencias de comandos y ejemplos de Python | Al igual que con R, Python incluye conjuntos de datos integrados y secuencias de comandos.  |
| Modelos previamente entrenados en R y Python | Modelos previamente entrenados se crean para casos de uso específicos y mantenidos por el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados como-es la puntuación de opiniones positivas y negativas en texto, o bien detectar características de imágenes, con nuevas entradas de datos que proporcione. Los modelos de ejecución en Machine Learning Services, pero no se puede instalar a través del programa de instalación de SQL Server. Para obtener más información, consulte [instalar previamente entrenado modelos de machine learning en SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Uso de SQL MLS

Los programadores y analistas suelen tengan código que se ejecutan en una instancia de SQL Server local. Adición de Machine Learning Services y habilitar la ejecución de scripts externos, ofrece la posibilidad de ejecutar código R y Python en modalidades de SQL Server: ajuste el script en los procedimientos almacenados, almacenar modelos en una tabla de SQL Server o combinación de funciones de R o Python y T-SQL en las consultas.

Ejecución del script está dentro de los límites del modelo de seguridad de datos: los permisos en la base de datos relacional son la base de acceso a datos en la secuencia de comandos. Un usuario que ejecuta el script de R o Python no debe ser capaz de utilizar los datos que no se pudieran tener acceso a dicho usuario en una consulta SQL. Necesita permisos de escritura y lectura de la base de datos estándar, además de un permiso adicional para ejecutar scripts externos. Modelos y el código que se escribe para datos relacionales son ajustados en procedimientos almacenados, serializar a un formato binario y almacenan en una tabla o cargados desde el disco si serializa la secuencia de bytes sin procesar en un archivo.

El enfoque más común para realizar análisis en bases de datos es usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), pasando el script de R o Python como un parámetro de entrada.

Las interacciones de cliente-servidor clásico es otro enfoque. Desde cualquier estación de trabajo cliente que tenga un IDE, puede instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) o [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)y, a continuación, escribir código que inserta la ejecución (denominados un *proceso remoto contexto*) a los datos y las operaciones a un servidor SQL remoto. 

Por último, si está utilizando un [servidor independiente](r/r-server-standalone.md) y Developer edition, puede crear soluciones en una estación de trabajo cliente usando las mismas bibliotecas y los intérpretes y, a continuación, implementar código de producción en SQL Server Machine Learning Servicios (en bases de datos). 

## <a name="how-to-get-started"></a>Cómo empezar a trabajar

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

+ [SQL Server Machine Learning Services (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Científicos de datos normalmente usan R o Python en su propia estación de trabajo portátil o desarrollo, para explorar datos y crear y ajustar modelos predictivos hasta que se logra un buen modelo predictivo. Con análisis en bases de datos en SQL Server, no hay ninguna necesidad de cambiar este proceso. Una vez completada la instalación, puede ejecutar código R o Python en SQL Server local y remota.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Usar el IDE que prefiera**. Puede vincular las bibliotecas de R y Python a su herramienta de desarrollo que prefiera. Para obtener más información, consulte [configurar herramientas de R](r/set-up-a-data-science-client.md) y [configurar herramientas de Python](python/setup-python-client-tools-sql.md).  

+ **Trabajar de forma local o remota**. Los científicos de datos pueden conectarse a SQL Server y llevar los datos al cliente para el análisis local, como de costumbre. Sin embargo, una solución mejor es usar el **RevoScaleR** o **revoscalepy** API para enviar los cálculos al equipo de SQL Server, evitar el movimiento de datos costosos y poco seguros.

+ **Insertar scripts de R o Python en procedimientos almacenados de SQL Server**. Cuando el código está totalmente optimizado, bien, ajústelo en un procedimiento almacenado para evitar el movimiento de datos innecesarios y optimizar las tareas de procesamiento de datos.

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Llamar a funciones de R o Python desde dentro de la secuencia de comandos de T-SQL:

+ [R: Aprenda análisis en bases de datos mediante R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: tutorial to-end con R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python: Ejecutar Python mediante T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python: Obtenga información sobre los análisis en bases de datos mediante Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Elegir el mejor lenguaje para la tarea. R es más adecuado para cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en datos, aproveche la eficacia de SQL Server para lograr el máximo rendimiento. Utilizar el motor de base de datos en memoria para los cálculos muy rápidos a través de las columnas.

### <a name="step-4-optimize-your-solution"></a>Paso 4: Optimizar la solución

Cuando el modelo está listo para crecer con datos empresariales, los científicos de datos a menudo funciona con el desarrollador DBA o SQL para optimizar los procesos, como:

+ Ingeniería de características
+ Ingesta de datos y transformación de datos
+ Puntuaciones

Tradicionalmente, los científicos de datos mediante R han tenido problemas de rendimiento y escalabilidad, especialmente cuando se usa el conjunto de datos grande. Eso es porque la implementación en tiempo de ejecución común es de subproceso único y puede dar cabida a solo esos conjuntos de datos que caben en la memoria disponible en el equipo local. Integración con SQL Server Machine Learning Services proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**: paquete de R esta contiene implementaciones de algunas de las funciones de R más populares, rediseñadas para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y escalabilidad mediante la inserción de cálculos al equipo de SQL Server, que normalmente tiene mayor memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python implementa las funciones más populares de RevoScaleR, por ejemplo, los contextos de cálculo remoto y el procesamiento distribuyen de muchos algoritmos que admiten.

Para obtener más información sobre el rendimiento, consulte este [caso práctico de rendimiento](r/performance-case-study-r-services.md) y [R y los datos de optimización](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Paso 5: Implementación y consumo

Después de la secuencia de comandos o el modelo está listo para su uso en producción, un desarrollador de la base de datos podría incrustar el código o el modelo en un procedimiento almacenado para que el código de R o Python guardado puede llamarse desde una aplicación. Almacenar y ejecutar código de R desde SQL Server tienen muchas ventajas: puede usar la cómoda interfaz de SQL Server y todos los cálculos tienen lugar en la base de datos, evitar el movimiento de datos innecesarios.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Seguro y extensible**. SQL Server utiliza una nueva arquitectura de extensibilidad que mantiene el motor de base de datos segura y aísla las sesiones de R y Python. También tiene control sobre los usuarios que pueden ejecutar scripts, y puede especificar qué bases de datos pueden tener acceso a código. Puede controlar la cantidad de recursos asignados al tiempo de ejecución, para evitar que unos cálculos masivos pongan en peligro el rendimiento global del servidor.

+ **Programación y auditoría**. Cuando se ejecutan trabajos de scripts externos en SQL Server, puede controlar y auditar los datos utilizados por los científicos de datos. También puede programar trabajos y crear flujos de trabajo que contiene scripts de R o Python externos, al igual que haría programar cualquier otro trabajo de Transact-SQL o procedimiento almacenado.

Para aprovechar las ventajas de las características de seguridad y administración de recursos de SQL Server, el proceso de implementación podría incluir estas tareas:

+ Convertir el código a una función que se puede ejecutar de forma óptima en un procedimiento almacenado
+ Configurar la seguridad y bloqueo de los paquetes utilizados por una tarea determinada
+ Habilitar regulación de recursos (requiere la edición Enterprise)

Para obtener más información, consulte [regulación de recursos para R](r/resource-governance-for-r-services.md) y [administración de paquetes de R para SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="version-history"></a>Historial de versiones

SQL Server 2017 Machine Learning Services es la próxima generación de SQL Server 2016 R Services, que se han mejorado para incluir Python. En la tabla siguiente es una lista completa de todas las versiones de producto, desde el comienzo a la versión actual. 

| Nombre del producto | Versión del motor | Fecha de la versión |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning Services (en bases de datos) | R Server 9.2.1 <br/> Server 9.2 de Python | Octubre de 2017 |
| Machine Learning Server (independiente) de SQL Server 2017 | R Server 9.2.1 <br/> Server 9.2 de Python | Octubre de 2017 |
| SQL Server 2016 R Services (In-Database) | R Server 9.1  | Julio de 2017  |
| SQL Server 2016 R Server (independiente)  |  R Server 9.1 | Julio de 2017 |

Para las versiones de paquete por versión, vea la versión de mapa en [actualizar R y Python componentes](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map).

## <a name="portability-and-related-products"></a>Portabilidad y productos relacionados

Portabilidad del código R y Python personalizado se dirige a través de la distribución de paquetes y los intérpretes que están integrados en varios productos. Los mismos paquetes que se incluyen en SQL Server también están disponibles en varios otros productos de Microsoft y servicios, incluida una versión que no sea de SQL llamada [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). 

Los clientes gratuita que incluyen nuestro intérpretes de R y Python son [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) y [bibliotecas de Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

En Azure, paquetes R y Python y los intérpretes de Microsoft también están disponibles en Azure Machine Learning y servicios de Azure como [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight), y [máquinas virtuales de Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). El [Data Science Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) incluye una estación de trabajo de desarrollo completamente equipado con herramientas de varios proveedores así como las bibliotecas y los intérpretes de Microsoft.

## <a name="see-also"></a>Vea también

[Instalar SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
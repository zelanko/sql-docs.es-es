---
title: 'Instalación Standalone R Server o Machine Learning Server: SQL Server Machine Learning Services'
description: Introducción de introducción a R Server independiente y Machine Learning Server en el programa de instalación de SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 47edd434445d57c5ca25373b5dc15fa328f94019
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513242"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (independiente) y Machine Learning Server (independiente) en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server proporciona compatibilidad con la instalación de un R Server independiente o Machine Learning Server que se ejecuta de forma independiente de SQL Server. Dependiendo de la versión de SQL Server, un servidor independiente tiene una base de R de código abierto y, posiblemente, Python, que se superpone con bibliotecas de alto rendimiento de Microsoft que agregar análisis predictivo y estadística a escala. Bibliotecas también permiten tareas de aprendizaje automático en scripts en R o Python. 

En SQL Server 2016, esta característica se denomina **R Server (independiente)** y es solo para R. En SQL Server 2017, se llama a **Machine Learning Server (independiente)** e incluye R y Python.  

> [!Note]
> Tal como se instala con el programa de instalación de SQL Server, un servidor independiente es funcionalmente equivalente a las versiones sin marca de SQL de [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), que admiten los mismos escenarios de usuario, incluida la ejecución remota puesta en marcha y los servicios web y el conjunto completo de bibliotecas de R y Python.

## <a name="components"></a>Componentes

SQL Server 2016 solo es R. SQL Server 2017 admite R y Python. En la tabla siguiente se describe las características de cada versión.

| Componente | Descripción |
|-----------|-------------|
| Paquetes de R | [**RevoScaleR** ](ref-r-revoscaler.md) es la biblioteca principal de R escalable con funciones de manipulación de datos, transformación, visualización y análisis.  <br/>[**MicrosoftML** ](ref-r-microsoftml.md) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto. <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) proporciona funciones auxiliares para colocar los scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutando el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) web de ofertas de implementación de servicio (en SQL Server 2017). <br/>[**olapR** ](ref-r-olapr.md) sirve para especificar las consultas MDX en R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Utilice siempre la versión de MRO agrupado en el programa de instalación. |
| Herramientas de R | Símbolos del sistema y las ventanas de la consola de R son herramientas estándares en una distribución de R. Puede encontrarlos en \Program files\Microsoft Server\140\R_SERVER\bin\x64 SQL. |
| Ejemplos de R y las secuencias de comandos |  Paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que se puede crear y ejecutar el script con datos previamente instalado. Examine para ellos \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets y \library\RevoScaleR. |
| Paquetes de Python | [**revoscalepy** ](../python/ref-py-revoscalepy.md) es la biblioteca principal para Python escalables con funciones de manipulación de datos, transformación, visualización y análisis. <br/>[**microsoftml** ](../python/ref-py-microsoftml.md) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto.  |
| Herramientas de Python | La herramienta de línea de comandos de Python integrada es útil para pruebas ad hoc y tareas. Encontrar la herramienta en \Program files\Microsoft Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esencial. |
| Secuencias de comandos y ejemplos de Python | Al igual que con R, Python incluye conjuntos de datos integrados y secuencias de comandos. Encontrar los datos de revoscalepy en \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente entrenados en R y Python | Modelos previamente entrenados se crean para casos de uso específicos y mantenidos por el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados como-es la puntuación de opiniones positivas y negativas en texto, o bien detectar características de imágenes, con nuevas entradas de datos que proporcione. Modelos previamente entrenados son compatibles y se pueden usar en un servidor independiente, pero no instalarlas a través del programa de instalación de SQL Server. Para obtener más información, consulte [instalar previamente entrenada modelos de aprendizaje automático en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso de un servidor independiente

Los desarrolladores de R y Python suele elegir un servidor independiente para ir más allá de las restricciones de memoria y procesamiento de código abierto R y Python. Ejecutar en un servidor independiente de bibliotecas de R y Python pueden cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una única salida consolidada. Funciones de alto rendimiento que están diseñadas para el escalado y utilidad: entrega de análisis predictivo, modelado estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial de aprendizaje de automático de vanguardia diseñada y compatibles con Microsoft.

Como un servidor independiente desacoplado de SQL Server, se configura el entorno de R y Python, segura y a los que accede con el sistema operativo subyacente y las herramientas estándares proporcionadas en el servidor independiente, no de SQL Server. No hay ninguna compatibilidad integrada para datos relacionales de SQL Server. Si desea utilizar datos de SQL Server, puede crear objetos de origen de datos y las conexiones como lo haría desde cualquier cliente.

Como un complemento a SQL Server, un servidor independiente también es útil como un entorno de desarrollo eficaz si necesita la informática local y remoto. Los paquetes de R y Python en un servidor independiente son las mismas que las proporcionadas con una instalación del motor de base de datos, lo que permite la portabilidad del código y [cambio de contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Cómo empezar a trabajar

Comience con el programa de instalación, adjuntar los archivos binarios a la herramienta de desarrollo que prefiera y escribir la primera secuencia de comandos.

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

Instale cualquiera de estas versiones:

+ [Machine Learning Server (independiente) de SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (independiente) - R solo](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

En un servidor independiente, es común para trabajar localmente con un desarrollo instalado en el mismo equipo.

+ [Configuración de las herramientas de R](set-up-a-data-science-client.md)
+ [Configuración de las herramientas de Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Escribir el script de R o Python mediante las funciones de RevoScaleR y revoscalepy con los algoritmos de aprendizaje automático.
  
  + [Explorar R y RevoScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Comience con los comandos básicos de R y, a continuación, avanzar a las funciones analíticas distribuibles de RevoScaleR que proporcionan alto rendimiento y escalabilidad para soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

  + [Inicio rápido: Un ejemplo de clasificación binaria con el paquete de Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): Crear un modelo de clasificación binaria mediante las funciones de microsoftml y el conjunto de datos de cáncer de mama conocido.

Elegir el mejor lenguaje para la tarea. R es más adecuado para cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en datos, aproveche la eficacia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Utilizar el motor de base de datos en memoria para los cálculos muy rápidos a través de las columnas.

### <a name="step-4-operationalize-your-solution"></a>Paso 4: Poner la solución

Pueden usar servidores independientes el [operacionalización](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidad de la que no son SQL-marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Puede configurar un servidor independiente para la puesta en marcha, lo que le ofrece estas ventajas: implementar y alojar el código como servicios web, ejecute los diagnósticos, comprobar la capacidad del servicio web.

### <a name="step-5-maintain-your-server"></a>Paso 5: Mantener el servidor

SQL Server libera las actualizaciones acumulativas de forma periódica. Aplicar las actualizaciones acumulativas agrega mejoras funcionales y seguridad a una instalación existente. 

Pueden encontrar descripciones de las funcionalidades nuevas o modificadas en la [CAB descargas](../install/sql-ml-cab-downloads.md) artículo y en las páginas web para [actualizaciones acumulativas de SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) y [las actualizaciones acumulativas de SQL Server 2017 ](https://support.microsoft.com/help/4047329). 

Para obtener más información sobre cómo aplicar actualizaciones a una instancia existente, consulte [aplicar actualizaciones](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) en las instrucciones de instalación.

## <a name="see-also"></a>Vea también

 [Instalar R Server (independiente) o Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)


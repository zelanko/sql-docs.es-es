---
title: Aprendizaje de máquina SQL Server (independiente) y R Server (independiente) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2c416049692f8860e4ba608e58f401ce527b135c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>Aprendizaje de máquina SQL Server (independiente) y R Server (independiente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Un servidor independiente es una instalación de componentes de aprendizaje de máquina, articulado como características de R y Python, que se ejecutan independientemente de instancias del motor de base de datos de SQL Server. Puede instalar a un servidor independiente por sí mismo, sin dependencias de SQL Server. Dado que un servidor independiente es independiente de SQL Server, configuración y tareas de administración y herramientas son más similares a una versión no son de SQL del servidor de aprendizaje de máquina, que puede leer acerca de [este artículo](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server).

El objetivo de un servidor de aprendizaje de máquina independiente consiste en proporcionar un entorno de desarrollo enriquecido, con el procesamiento distribuido y paralelo de las cargas de trabajo de R y Python en pequeñas a grandes conjuntos de datos, utilizando los paquetes propietarios y los motores de cálculo instalado con el servidor. Los paquetes de R y Python en un servidor independiente son los mismos que los mostrados en una instalación de SQL Server (In-Database), lo que permite la portabilidad del código y [cambio de contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

Los desarrolladores de la razón principal elegir que un servidor de aprendizaje de máquina independiente es algo más que las restricciones de memoria y procesamiento de código abierto R y Python. Servidores independientes pueden cargar y procesar grandes cantidades de datos en varios núcleos y agrupar los resultados en una única salida consolidada. Las funciones y los algoritmos están diseñados para escalabilidad y utilidad: entrega de análisis predictivos, modelo estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial de aprendizaje de automático de vanguardia ingeniería y compatible con Microsoft.

Por lo general, se recomienda que trate (independiente) y (en bases de datos) instalaciones como mutuamente exclusivos para evitar la contención de recursos, pero si tiene recursos suficientes, no hay ninguna prohibición de la instalación de ambos en el mismo equipo físico.

Solo puede tener un servidor independiente en el equipo: cualquier [máquina aprendizaje Server (independiente) de SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md) o [R Server (independiente) de SQL Server 2016](../install/sql-r-standalone-windows-install.md). Debe desinstalar manualmente una versión antes de instalar una versión diferente.

## <a name="components-of-a-standalone-server"></a>Componentes de un servidor independiente

SQL Server 2016 solo es R. SQL Server 2017 admite R y Python. La tabla siguiente describen las características de cada versión.

| Componente | Description |
|-----------|-------------|
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

+ [Servidor de aprendizaje de SQL Server de 2017 máquina (independiente)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (independiente) - R solo](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Configurar las herramientas de desarrollo para usar los archivos binarios del servidor de aprendizaje de máquina. Para obtener más información acerca de Python, consulte [archivos binarios de Python de vínculo](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obtener instrucciones sobre cómo conectar en R Studio, consulte [utilizando diferentes versiones de R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) y seleccione la herramienta C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. También puede intentar [R Tools para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Escribir el script de R o Python mediante funciones de RevoScaleR, revoscalepy y los algoritmos de aprendizaje automático.
  
  + [Explorar R y RevoScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): inicio con comandos básicos de R y, a continuación, en curso para las funciones analíticas distribuibles de RevoScaleR que proporcionan un alto rendimiento y escalado a soluciones en R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

  + [Inicio rápido: Un ejemplo de clasificación binaria con el paquete de Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): crear un modelo de clasificación binaria mediante las funciones de microsoftml y el conjunto de datos de ejemplo de cáncer de mama conocido.

Elegir el mejor lenguaje para la tarea. R es más adecuado para realizar cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en conjunto sobre datos, aprovechan la eficacia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Usar el motor de base de datos en memoria para realizar cálculos muy rápidos a través de las columnas.

### <a name="step-4-operationalize-your-solution"></a>Paso 4: Incorporación de operatividad a su solución

Pueden usar servidores independientes el [puesta en marcha](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidad de la sin SQL-marca [aprendizaje de máquina de Microsoft Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Puede configurar un servidor independiente para la puesta en marcha, que ofrece estas ventajas: implementar y alojar el código como servicios web, ejecute los diagnósticos, prueba la capacidad del servicio web.

## <a name="see-also"></a>Vea también

 [Equipo con SQL Server (en bases de datos) de servicios de aprendizaje](sql-server-r-services.md)


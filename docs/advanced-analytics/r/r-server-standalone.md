---
title: SQL Server Machine Learning Server (independiente) y R Server (independiente) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8cdceabc26c55b6eade57712fa610d3e84808f5
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174792"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server Machine Learning Server (independiente) y R Server (independiente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Un servidor independiente es una instalación de componentes de aprendizaje automático, articuladas como características de R y Python, que se ejecutan independientemente de instancias del motor de base de datos de SQL Server. Puede instalar a un servidor independiente por sí mismo, sin dependencias de SQL Server. Dado que un servidor independiente es independiente de SQL Server, configuración y administración de tareas y herramientas son más similares a una versión que no sea de SQL de Machine Learning Server, que puede leer sobre en [en este artículo](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server).

El objetivo de un servidor independiente de machine learning es proporcionar un entorno de desarrollo eficaz, con el procesamiento paralelo y distribuido de cargas de trabajo de R y Python en pequeños a grandes conjuntos de datos, mediante los paquetes de propiedad y los motores de cálculo se instala con el servidor. Los paquetes de R y Python en un servidor independiente son los mismos que los proporcionados en una instalación de SQL Server (en bases de datos), lo que permite la portabilidad del código y [cambio de contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

Los desarrolladores de la razón principal por elegir que un servidor independiente de machine learning consiste en mover más allá de las restricciones de memoria y procesamiento de código abierto R y Python. Servidores independientes pueden cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una única salida consolidada. Los algoritmos y las funciones están diseñados para el escalado y utilidad: entrega de análisis predictivo, modelado estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial de aprendizaje de automático de vanguardia diseñada y compatibles con Microsoft.

Por lo general, se recomienda tratar (independiente) y (en bases de datos) instalaciones como mutuamente exclusivos para evitar la contención de recursos, pero si tiene recursos suficientes, no hay ninguna prohibición de la instalación de ambos en el mismo equipo físico.

Solo puede tener un servidor independiente en el equipo: cualquier [Machine Learning Server (independiente) de SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md) o [SQL Server 2016 R Server (independiente)](../install/sql-r-standalone-windows-install.md). Debe desinstalar manualmente una versión antes de instalar una versión diferente.

## <a name="components-of-a-standalone-server"></a>Componentes de un servidor independiente

SQL Server 2016 solo es R. SQL Server 2017 admite R y Python. En la tabla siguiente se describe las características de cada versión.

| Componente | Descripción |
|-----------|-------------|
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

+ [Machine Learning Server (independiente) de SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (independiente) - R solo](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Configurar las herramientas de desarrollo para usar los archivos binarios de Machine Learning Server. Para obtener más información acerca de Python, consulte [binarios de Python de vínculo](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obtener instrucciones sobre cómo conectar en R Studio, consulte [con diferentes versiones de R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) y elija la herramienta C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. También puede probar [R Tools para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir la primera secuencia de comandos

Escribir el script de R o Python mediante las funciones de RevoScaleR y revoscalepy con los algoritmos de aprendizaje automático.
  
  + [Explorar R y RevoScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): empiece con los comandos básicos de R y, a continuación, en curso para las funciones analíticas distribuibles de RevoScaleR que proporcionan un alto rendimiento y escalabilidad para soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

  + [Inicio rápido: Un ejemplo de clasificación binaria con el paquete de Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): crear un modelo de clasificación binaria mediante las funciones de microsoftml y el conjunto de datos de cáncer de mama conocido.

Elegir el mejor lenguaje para la tarea. R es más adecuado para cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en datos, aproveche la eficacia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Utilizar el motor de base de datos en memoria para los cálculos muy rápidos a través de las columnas.

### <a name="step-4-operationalize-your-solution"></a>Paso 4: Hacer operativo de la solución

Pueden usar servidores independientes el [operacionalización](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidad de la que no son SQL-marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Puede configurar un servidor independiente para la puesta en marcha, lo que le ofrece estas ventajas: implementar y alojar el código como servicios web, ejecute los diagnósticos, comprobar la capacidad del servicio web.

## <a name="see-also"></a>Vea también

 [SQL Server Machine Learning Services (en bases de datos)](sql-server-r-services.md)


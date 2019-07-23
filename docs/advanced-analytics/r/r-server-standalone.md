---
title: Instalación de R Server o Machine Learning Server independiente
description: Introducción a la R Server independiente y Machine Learning Server en SQL Server la instalación
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: f50049b1b93068748da84342d68ab6cb319c5d98
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344889"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (independiente) y Machine Learning Server (independiente) en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server proporciona compatibilidad de instalación para un R Server independiente o Machine Learning Server que se ejecuta independientemente de SQL Server. En función de la versión de SQL Server, un servidor independiente tiene una base de R de código abierto y posiblemente Python, superpuestas con bibliotecas de alto rendimiento de Microsoft que agregan análisis de predicción y estadísticos a escala. Las bibliotecas también permiten realizar tareas de aprendizaje automático con scripts en R o Python. 

En SQL Server 2016, esta característica se denomina **R Server (independiente)** y es de solo lectura. En SQL Server 2017, se llama **machine learning Server (independiente)** e incluye R y Python.  

> [!Note]
> Tal y como lo instala SQL Server el programa de instalación, un servidor independiente es funcionalmente equivalente a las versiones no de marca no SQL de [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), lo que admite los mismos escenarios de usuario, como la ejecución remota, la operacionalización y la web servicios y la colección completa de bibliotecas de R y Python.

## <a name="components"></a>Componentes

SQL Server 2016 es solo R. SQL Server 2017 admite R y Python. En la tabla siguiente se describen las características de cada versión.

| Componente | Descripción |
|-----------|-------------|
| Paquetes de R | [**RevoScaleR**](ref-r-revoscaler.md) es la biblioteca principal para R escalable con funciones para la manipulación, transformación, visualización y análisis de datos.  <br/>[**MicrosoftML**](ref-r-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) proporciona funciones auxiliares para colocar scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutar el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md) ofrece una implementación de servicio Web (solo en SQL Server 2017). <br/>[**olapr**](ref-r-olapr.md) es para especificar consultas MDX en R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Use siempre la versión de MRO que se incluye en el programa de instalación. |
| Herramientas de R | Las ventanas de la consola de r y los símbolos del sistema son herramientas estándar en una distribución de R. Encontrarlos en \Archivos de Programa\microsoft SQL Server\140\R_SERVER\bin\x64. |
| Ejemplos y scripts de R |  Los paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que pueda crear y ejecutar scripts con datos preinstalados. Búsquelo en \Archivos de Programa\microsoft SQL Server\140\R_SERVER\library\datasets y \library\RevoScaleR. |
| Paquetes de Python | [**revoscalepy**](../python/ref-py-revoscalepy.md) es la biblioteca principal para Python escalable con funciones para la manipulación, transformación, visualización y análisis de datos. <br/>[**microsoftml**](../python/ref-py-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones.  |
| Herramientas de Python | La herramienta de línea de comandos de Python integrada es útil para las pruebas y tareas ad hoc. Busque la herramienta en \Archivos de Programa\microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esenciales. |
| Ejemplos y scripts de Python | Al igual que con R, Python incluye scripts y conjuntos de datos integrados. Busque los datos de revoscalepy en \Archivos de Programa\microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente entrenados en R y Python | Los modelos previamente entrenados se crean para casos de uso específicos y los mantiene el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados tal cual para puntuar la opinión positiva negativa en el texto o para detectar características en las imágenes, con las nuevas entradas de datos que proporcione. Los modelos previamente entrenados se admiten y se pueden usar en un servidor independiente, pero no se pueden instalar a través de SQL Server programa de instalación. Para más información, consulte [instalación de modelos de machine learning previamente entrenados en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso de un servidor independiente

Los desarrolladores de r y Python suelen elegir un servidor independiente para moverse más allá de la memoria y las restricciones de procesamiento de R y Python de código abierto. Las bibliotecas de R y Python que se ejecutan en un servidor independiente pueden cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una sola salida consolidada. Las funciones de alto rendimiento están diseñadas para la escala y la utilidad, que ofrecen análisis predictivo, modelos estadísticos, visualizaciones de datos y algoritmos de aprendizaje automático de vanguardia en un producto de servidor comercial con ingeniería y soporte técnico de Microsoft.

Como un servidor independiente desacoplado de SQL Server, el entorno de R y Python está configurado, protegido y se tiene acceso a él mediante el sistema operativo subyacente y las herramientas estándar proporcionadas en el servidor independiente, no SQL Server. No hay compatibilidad integrada para SQL Server datos relacionales. Si desea utilizar datos de SQL Server, puede crear objetos y conexiones de origen de datos como lo haría con cualquier cliente.

Como complemento a SQL Server, un servidor independiente también es útil como un entorno de desarrollo eficaz si necesita equipos locales y remotos. Los paquetes de R y Python en un servidor independiente son los mismos que los que se proporcionan con una instalación del motor de base de datos, lo que permite la portabilidad del código y [el cambio de contexto de proceso](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Cómo empezar

Comience con el programa de instalación, adjunte los archivos binarios a su herramienta de desarrollo favorita y escriba el primer script.

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

Instale una de estas versiones:

+ [SQL Server 2017 Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (independiente)-solo R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

En un servidor independiente, es habitual trabajar localmente con un desarrollo instalado en el mismo equipo.

+ [Configuración de las herramientas de R](set-up-a-data-science-client.md)
+ [Configuración de las herramientas de Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Paso 3: Escribir el primer script

Escriba el script de R o Python con las funciones de RevoScaleR, revoscalepy y los algoritmos de aprendizaje automático.
  
  + [Explore R y RevoScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Comience con comandos de R básicos y, a continuación, avance hasta las funciones analíticas de RevoScaleR distribuible que proporcionan alto rendimiento y escalado a soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

  + [Inicio rápido: Un ejemplo de clasificación binaria con el paquete](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)de Python de microsoftml: Cree un modelo de clasificación binaria con las funciones de microsoftml y el conjunto de archivos de cáncer de mama conocido.

Elija el mejor idioma para la tarea. R es la mejor opción para los cálculos estadísticos que son difíciles de implementar con SQL. En el caso de las operaciones basadas en conjuntos en los datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , aproveche el potencial de para lograr el máximo rendimiento. Usar el motor de base de datos en memoria para cálculos muy rápidos en columnas.

### <a name="step-4-operationalize-your-solution"></a>Paso 4: Poner en funcionamiento la solución

Los servidores independientes pueden utilizar la funcionalidad de [operacionalización](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) de la [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)no marcada por SQL. Puede configurar un servidor independiente para la operacionalización, lo que le ofrece estas ventajas: implementar y hospedar el código como servicios Web, ejecutar diagnósticos, probar la capacidad del servicio Web.

### <a name="step-5-maintain-your-server"></a>Paso 5: Mantenimiento del servidor

SQL Server publica actualizaciones acumulativas periódicamente. La aplicación de las actualizaciones acumulativas agrega mejoras funcionales y de seguridad a una instalación existente. 

Puede encontrar descripciones de funcionalidad nueva o modificada en el artículo sobre [descargas de CAB](../install/sql-ml-cab-downloads.md) y en las páginas web para [las actualizaciones acumulativas de SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) y [las actualizaciones acumulativas de SQL Server 2017](https://support.microsoft.com/help/4047329). 

Para obtener más información sobre cómo aplicar las actualizaciones a una instancia existente, consulte [aplicar actualizaciones](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) en las instrucciones de instalación.

## <a name="see-also"></a>Vea también

 [Instalación de R Server (independiente) o Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)


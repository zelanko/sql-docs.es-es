---
title: ¿Qué es Machine Learning Server (independiente) o R Server?
description: Obtenga información sobre las diferencias entre R Server independiente y Machine Learning Server en la instalación de SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 67cdc278387de1faef999aa67543ec73c021bc41
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489745"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>¿Qué son Machine Learning Server (independiente) o R Server en SQL Server?
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server proporciona soporte de instalación para un servidor R Server o Machine Learning Server independiente que se ejecuta independientemente de SQL Server. En función de la versión de SQL Server, un servidor independiente tiene una base de R de código abierto y posiblemente de Python, superpuestas con bibliotecas de alto rendimiento de Microsoft que agregan análisis predictivos y estadísticos a escala. Las bibliotecas también permiten realizar tareas de aprendizaje automático con scripts en R o Python. 

En SQL Server 2016, esta característica se denomina **R Server (independiente)** y es de solo R. En SQL Server 2017 se denomina **Machine Learning Server (independiente)** e incluye R y Python.  

> [!Note]
> Tal y como se instala con el programa de instalación de SQL Server, un servidor independiente es funcionalmente equivalente a las versiones que no son de la marca SQL de [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) y admite los mismos escenarios de usuario, como la ejecución remota, la operacionalización y los servicios web, así como la colección completa de bibliotecas de R y Python.

## <a name="components"></a>Componentes

SQL Server 2016 solo admite R. SQL Server 2017 admite R y Python. En la tabla siguiente se indican las características de cada versión.

| Componente | Descripción |
|-----------|-------------|
| Paquetes de R | [**RevoScaleR**](ref-r-revoscaler.md) es la biblioteca principal para R escalable con funciones para la manipulación, transformación, visualización y análisis de datos.  <br/>[**MicrosoftML**](ref-r-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados dedicados al análisis de texto, imágenes y opiniones. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) proporciona funciones del asistente para colocar scripts de R en un procedimiento almacenado de T-SQL, registrar dicho procedimiento almacenado en una base de datos y ejecutarlo desde un entorno de desarrollo de R.<br/>[**olapr**](ref-r-olapr.md) es para especificar consultas MDX en R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Use siempre la versión de MRO que se incluye en el programa de instalación. |
| Herramientas de R | Las ventanas de la consola de R y los símbolos del sistema son herramientas estándar en una distribución de R. Podrá encontrarlos en \Archivos de programa\Microsoft SQL Server\140\ R_SERVER\bin\x64. |
| Ejemplos de R y scripts |  Los paquetes de código abierto de R y RevoScaleR incluyen conjuntos de datos integrados para que pueda crear y ejecutar scripts con datos preinstalados. Podrá buscarlos en \Archivos de programa\Microsoft SQL Server\140\ R_SERVER\library\datasets y \library\RevoScaleR. |
| Paquetes de Python | [**revoscalepy**](../python/ref-py-revoscalepy.md) es la biblioteca principal para Python escalable con funciones para la manipulación, transformación, visualización y análisis de datos. <br/>[**microsoftml**](../python/ref-py-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados dedicados al análisis de texto, imágenes y opiniones.  |
| Herramientas de Python: | La herramienta integrada de línea de comandos de Python es útil para las pruebas y tareas ad hoc. Podrá encontrar la herramienta en \Archivos de programa\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda es una distribución de código abierto de Python y paquetes esenciales. |
| Ejemplos de Python y scripts | Al igual que con R, Python incluye scripts y conjuntos de datos integrados. Podrá encontrar los datos de revoscalepy en \Archivos de programa\Microsoft SQL Server\140\PYTHON_SERVER\bib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente entrenados en R y Python | Los modelos previamente entrenados se crean para casos de uso específicos y los mantiene el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados tal cual para puntuar la opinión positiva-negativa en el texto o para detectar características en las imágenes, con las nuevas entradas de datos que proporcione. Los modelos previamente entrenados se admiten y se pueden usar en un servidor independiente, pero no se pueden instalar a través del programa de instalación de SQL Server. Para obtener más información, vea [Instalación de modelos de aprendizaje automático previamente entrenados en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso de un servidor independiente

Los desarrolladores de R y Python suelen elegir un servidor independiente para moverse más allá de la memoria y las restricciones de procesamiento de R y Python de código abierto. Las bibliotecas de R y Python que se ejecutan en un servidor independiente pueden cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una sola salida consolidada. Las funciones de alto rendimiento están diseñadas para la escala y la utilidad: ofrecen un análisis predictivo, modelos estadísticos, visualizaciones de datos y algoritmos de aprendizaje automático de vanguardia en un producto de servidor comercial con ingeniería y soporte técnico de Microsoft.

Como servidor independiente desacoplado de SQL Server, la configuración, la protección y el acceso del entorno de R y Python se realizan mediante el sistema operativo subyacente y las herramientas estándar proporcionadas en el servidor independiente, y no mediante SQL Server. No hay compatibilidad integrada para los datos relacionales de SQL Server. Si quiere utilizar datos de SQL Server, puede crear objetos y conexiones de origen de datos como lo haría con cualquier cliente.

Como complemento a SQL Server, un servidor independiente también es útil como un entorno de desarrollo eficaz si necesita equipos locales y remotos. Los paquetes de R y Python en un servidor independiente son los mismos que los que se proporcionan con una instalación del motor de base de datos, lo que permite la portabilidad del código y [el cambio de contexto de cálculo](/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Introducción

Comience con el programa de instalación, adjunte los binarios a su herramienta de desarrollo favorita y escriba el primer script.

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

Instale una de estas versiones:

+ [SQL Server 2017 Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (independiente) - solo R](../install/sql-machine-learning-standalone-windows-install.md?view=sql-server-2016&preserve-view=true)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

En un servidor independiente, es habitual trabajar localmente con un desarrollo instalado en el mismo equipo.

+ [Configuración de las herramientas de R](set-up-a-data-science-client.md)
+ [Configuración de las herramientas de Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Paso 3: escritura del primer script

Escriba el script de R o Python con las funciones de RevoScaleR, revoscalepy y los algoritmos de aprendizaje automático.
  
  + [Exploración de R y ScaleR en 25 funciones](/machine-learning-server/r/tutorial-r-to-revoscaler): Comience con comandos de R básicos y, a continuación, avance hasta las funciones analíticas de RevoScaleR distribuibles que proporcionan alto rendimiento y escalabilidad para soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos.

  + [Inicio rápido: Un ejemplo de clasificación binaria con el paquete de Python de microsoftml](/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): Cree un modelo de clasificación binaria con las funciones de microsoftml y el conocido conjunto de datos de cáncer de mama.

Elija el mejor lenguaje para la tarea. R es la mejor opción para los cálculos estadísticos que son difíciles de implementar mediante SQL. En el caso de las operaciones basadas en conjuntos sobre datos, aproveche la potencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obtener el máximo rendimiento. Use el motor de base de datos en memoria para cálculos muy rápidos en columnas.

### <a name="step-4-operationalize-your-solution"></a>Paso 4: puesta en funcionamiento de la solución

Los servidores independientes pueden usar la funcionalidad de [operacionalización](/machine-learning-server/what-is-operationalization) de [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) que no son de la marca SQL. Puede configurar un servidor independiente para la operacionalización, lo que le ofrece estas ventajas: implementar y hospedar el código como servicios web, ejecutar diagnósticos y probar la capacidad del servicio web.

### <a name="step-5-maintain-your-server"></a>Paso 5: mantenimiento del servidor

SQL Server publica actualizaciones acumulativas periódicamente. La aplicación de las actualizaciones acumulativas agrega mejoras funcionales y de seguridad a una instalación existente. 

Puede encontrar descripciones de la funcionalidad nueva o modificada en el artículo [descargas de CAB](../install/sql-ml-cab-downloads.md) y en las páginas web de las [actualizaciones acumulativas de SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) y las [actualizaciones acumulativas de SQL Server 2017](https://support.microsoft.com/help/4047329). 

Para obtener más información sobre cómo aplicar las actualizaciones a una instancia existente, vea [Aplicación de actualizaciones](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) en las instrucciones de instalación.

## <a name="see-also"></a>Consulte también

 [Instalación de R Server (independiente) o Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)

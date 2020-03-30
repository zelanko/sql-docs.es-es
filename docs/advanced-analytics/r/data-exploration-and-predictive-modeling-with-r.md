---
title: Modelado de predicción con R
description: En este artículo se describen las mejoras en el proceso de ciencia de datos que se pueden realizar a través de la integración con SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6b336404d3b69e31ffb6f1a2aa82ade04804eb9e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78172336"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>Exploración de datos y modelado de predicción con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen las mejoras en el proceso de ciencia de datos que se pueden realizar a través de la integración con SQL Server.

## <a name="the-data-science-process"></a>El proceso de ciencia de datos

Los científicos de datos suelen utilizar R para explorar datos y crear modelos de predicción. Habitualmente, esto consiste en un proceso iterativo de ensayo y error hasta que se logra un buen modelo de predicción. Como científico de datos experimentado, se podría conectar a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y capturar los datos para su estación de trabajo local mediante el paquete RODBC, explorar los datos y crear un modelo de predicción mediante paquetes R estándares.

Sin embargo, este método tiene muchas desventajas que han supuesto un obstáculo para las empresas a la hora de usar R más ampliamente. 

+ El movimiento de datos puede ser lento, ineficaz o inseguro.
+ El propio lenguaje R tiene limitaciones de rendimiento y escalado.

Estos inconvenientes resultan más evidentes cuando hay que mover y analizar grandes cantidades de datos o usar conjuntos de datos que no caben en la memoria disponible en el equipo.

Los nuevos paquetes y funciones escalables de R incluidos en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] le ayudarán a dejar atrás muchos de estos retos. 

## <a name="whats-different-about-revoscaler"></a>¿Qué diferencia hay en RevoScaleR?

El paquete **RevoScaleR** contiene implementaciones de algunas de las funciones de R más populares, que se han rediseñado para ofrecer paralelismo y escalabilidad. Para más información, vea [Computación distribuida con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).

El paquete RevoScaleR también permite cambiar el *contexto de ejecución*. Esto significa que, para una solución completa o tan solo una función, puede indicar que los cálculos se deben llevar a cabo con los recursos del equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de su estación de trabajo local. Esto conlleva varias ventajas: evita los movimientos de datos innecesarios y puede aprovechar la mayor cantidad de recursos de cálculo del equipo del servidor.

## <a name="r-environment-and-packages"></a>Paquetes y entorno de R

El entorno de R admitido en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un runtime, el lenguaje de código abierto y un motor de gráficos respaldado y ampliado por diversos paquetes. El lenguaje admite una amplia variedad de extensiones que se implementan mediante paquetes.  

### <a name="using-other-r-packages"></a>Uso de otros paquetes de R

Además de las bibliotecas de R de propiedad incluidas con Microsoft Machine Learning, se pueden usar casi todos los paquetes de R de la solución, a saber:

+ Paquetes de R de propósito general de repositorios públicos. Puede conseguir los paquetes de R de código abierto más populares en repositorios públicos, como CRAN, que hospeda más de 6000 paquetes que pueden usar los científicos de datos.
  
  Para la plataforma Windows, los paquetes de R se distribuyen como archivos .zip, que se pueden descargar e instalar bajo la licencia GPL.  
  
  Para obtener más información sobre cómo instalar paquetes de terceros para su uso con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Bibliotecas y paquetes adicionales incluidos en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     El paquete **RevoScaleR** incluye análisis de macrodatos de alto rendimiento, versiones mejoradas de funciones que admiten tareas habituales de la ciencia de datos, mecanismos de aprendizaje optimizados para Bayes naive, regresión lineal, modelos de series de tiempo y redes neuronales, así como bibliotecas de matemáticas avanzadas.  
  
     El paquete **RevoPemaR** permite desarrollar en R sus propios algoritmos de ejecución en paralelo de memoria externa.  
  
     Para más información sobre estos paquetes y cómo usarlos, vea [Qué es RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) e [Introducción a RevoPemaR](https://docs.microsoft.com/machine-learning-server/r/how-to-developer-pemar). 

+ **MicrosoftML** contiene una colección de transformaciones de datos y algoritmos de Machine Learning tremendamente optimizados procedentes del equipo de ciencia de datos de Microsoft. Muchos de esos algoritmos se usan también en Azure Machine Learning. Para obtener más información, vea [MicrosoftML en SQL Server](ref-r-microsoftml.md).

### <a name="r-development-tools"></a>Herramientas de desarrollo en R

Al desarrollar la solución de R, asegúrese de descargar Microsoft R Client. Esta descarga gratuita incluye las bibliotecas necesarias para admitir contextos de cálculo remotos y algoritmos escalables:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** una distribución del tiempo de ejecución de R y un conjunto de paquetes, como la biblioteca de matemáticas del kernel de Intel, que potencian el rendimiento de las operaciones estándar de R.  
  
+ **RevoScaleR:** un paquete de R que permite realizar cálculos de inserción en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. También incluye un conjunto de funciones de R habituales que se han rediseñado para ofrecer mejor rendimiento y escalabilidad. Puede identificar estas funciones mejoradas gracias al prefijo **rx** . También incluye proveedores de datos mejorados para una variedad de orígenes. Estas funciones tienen el prefijo **Rx**.

Se puede usar cualquier editor de código basado en Windows que admita R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o RStudio. La descarga de [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] también incluye herramientas de línea de comandos para R habituales, como RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Uso de nuevos orígenes de datos y contextos de cálculo

Cuando use el paquete RevoScaleR para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], busque estas funciones para usarlas en su código en R:

+ **RxSqlServerData** es una función incluida en el paquete RevoScaleR para facilitar una conectividad de datos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Esta función se utiliza en el código en R para definir el *origen de datos*. El objeto de origen de datos especifica el servidor y las tablas donde se encuentran los datos y se ocupa de la tarea de leer y escribir datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   El paquete **RxInSqlServer** se puede usar para especificar el *cálculo*.  Dicho de otro modo, puede indicar en qué lugar se debe ejecutar el código en R: en su estación de trabajo local o en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Para más información, vea [Funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler).
  
     Al establecer el contexto de cálculo, este solo afecta a los cálculos compatibles con el contexto de ejecución remoto (es decir, las operaciones de R proporcionadas por el paquete RevoScaleR y funciones relacionadas). Normalmente, no se pueden ejecutar soluciones de R basadas en paquetes CRAN estándar en un contexto de cálculo remoto, aunque se pueden ejecutar en el equipo de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] si las inicia T-SQL. Pero se puede usar la función `rxExec` para llamar a funciones individuales de R y ejecutarlas de forma remota en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para obtener ejemplos de cómo crear orígenes de datos y contextos de ejecución, y cómo trabajar con ellos, vea estos tutoriales:

+ [Análisis detallado de ciencia de datos](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Análisis de datos con Microsoft R](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)

## <a name="deploy-r-code-to-production"></a>Implementación de código de R en producción

Una parte importante de ciencia de datos consiste en proporcionar sus análisis a otras personas o utilizar modelos de predicción para mejorar procesos o resultados empresariales. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], resulta sencillo proceder al entorno de producción cuando su modelo o script en R está listo.

Para obtener más información sobre cómo puede trasladar el código para que se ejecute en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Por lo general, el proceso de implementación empieza por limpiar el script para eliminar los fragmentos de código que no se precisen en el entorno de producción. A medida que los cálculos se van acercando a los datos, es probable que encuentre maneras de trasladar, resumir o presentar datos de forma más eficaz que hacer todo en R. Es recomendable que el científico de datos acuda a un desarrollador de bases de datos para conocer las distintas formas de mejorar el rendimiento, especialmente si la solución realiza tareas de limpieza de datos o de ingeniería de características que pueden ser más eficaces en SQL. Es posible que se necesiten cambios en los procesos ETL para garantizar que los flujos de trabajo destinados a generar o puntuar un modelo no produzcan errores, y que los datos de entrada estén disponibles en el formato correcto.

## <a name="see-also"></a>Consulte también

[Comparación de funciones de Base R y RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)

[Biblioteca RevoScaleR en SQL Server](ref-r-revoscaler.md)

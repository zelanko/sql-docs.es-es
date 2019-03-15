---
title: Exploración de datos y modelado de predicción con R - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2e045d061df813ae004dcb13668c31e68c3b5b5a
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976419"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>Exploración de datos y modelado de predicción con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe las mejoras en el proceso de ciencia de datos que son posibles mediante la integración con SQL Server.

Se aplica a: SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="the-data-science-process"></a>El proceso de ciencia de datos

Los científicos de datos suelen utilizar R para explorar datos y crear modelos de predicción. Habitualmente, esto consiste en un proceso iterativo de ensayo y error hasta que se logra un buen modelo de predicción. Como científico de datos experimentado, se podría conectar a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y capturar los datos para su estación de trabajo local mediante el paquete RODBC, explorar los datos y crear un modelo de predicción mediante paquetes R estándares.

Sin embargo, este enfoque tiene muchas desventajas, que tengan impedirse la adopción más amplia de R en la empresa. 

+ Movimiento de datos puede ser lento, ineficaz o no segura
+ Propio R tiene limitaciones de rendimiento y escalabilidad

Estos inconvenientes resultan más evidentes cuando necesite mover y analizar grandes cantidades de datos o usar conjuntos de datos que no se ajustan a la memoria disponible en el equipo.

Los nuevos paquetes escalables y funciones de R incluidas con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] le ayudarán a superar muchas de estas dificultades. 

## <a name="whats-different-about-revoscaler"></a>¿Qué es diferente en RevoScaleR?

El paquete **RevoScaleR** contiene implementaciones de algunas de las funciones de R más populares, que se han rediseñado para ofrecer paralelismo y escalabilidad. Para obtener más información, consulte [Distributed Computing con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).

El paquete RevoScaleR también permite cambiar el *contexto de ejecución*. Esto significa que, para una solución completa o tan solo una función, puede indicar que los cálculos se deben llevar a cabo con los recursos del equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de su estación de trabajo local. Esto conlleva varias ventajas: evita los movimientos de datos innecesarios y puede aprovechar la mayor cantidad de recursos de cálculo del equipo del servidor.

## <a name="r-environment-and-packages"></a>Paquetes y entorno de R

El entorno de R admitido en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un runtime, el lenguaje de código abierto y un motor de gráficos respaldado y ampliado por diversos paquetes. El lenguaje admite una amplia variedad de extensiones que se implementan mediante paquetes.  

### <a name="using-other-r-packages"></a>Uso de otros paquetes de R

Además de las bibliotecas de R patentadas incluidas con Microsoft Machine Learning, puede usar casi todos los paquetes de R en la solución, incluidos:

+ Paquetes de R de propósito general de repositorios públicos. Puede conseguir los paquetes de R de código abierto más populares en repositorios públicos, como CRAN, que hospeda más de 6000 paquetes que pueden usar los científicos de datos.
  
  Para la plataforma Windows, los paquetes de R se distribuyen como archivos .zip, que se pueden descargar e instalar bajo la licencia GPL.  
  
  Para obtener más información sobre cómo instalar paquetes de terceros para su uso con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Bibliotecas y paquetes adicionales incluidos en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     El paquete **RevoScaleR** incluye análisis de macrodatos de alto rendimiento, versiones mejoradas de funciones que admiten tareas habituales de la ciencia de datos, mecanismos de aprendizaje optimizados para Bayes naive, regresión lineal, modelos de series de tiempo y redes neuronales, así como bibliotecas de matemáticas avanzadas.  
  
     El paquete **RevoPemaR** permite desarrollar en R sus propios algoritmos de ejecución en paralelo de memoria externa.  
  
     Para obtener más información sobre estos paquetes y cómo usarlas, vea [What ' s RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) y [Introducción a RevoPemaR](https://docs.microsoft.com/machine-learning-server/r/how-to-developer-pemar). 

+ **MicrosoftML** contiene una colección de transformaciones de datos desde el equipo de ciencia de datos de Microsoft y algoritmos de aprendizaje automático altamente optimizada. Muchos de los algoritmos también se usan en Azure Machine Learning. Para obtener más información, consulte [MicrosoftML en SQL Server](ref-r-microsoftml.md).

### <a name="r-development-tools"></a>Herramientas de desarrollo en R

Al desarrollar la solución de R, asegúrese de descargar a Microsoft R Client. Esta descarga gratuita incluye las bibliotecas necesarias para admitir contextos de cálculo remotos y alorithms escalable:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Una distribución de tiempo de ejecución de R y un conjunto de paquetes, como la biblioteca central de matemáticas de Intel, que potencian el rendimiento de las operaciones de R estándar.  
  
+ **RevoScaleR:** Un paquete de R que le permite insertar cálculos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]  También incluye un conjunto de funciones de R habituales que se han rediseñado para ofrecer mejor rendimiento y escalabilidad. Puede identificar estas funciones mejoradas gracias al prefijo **rx** . También incluye proveedores de datos mejorados para una variedad de orígenes. Estas funciones tienen el prefijo **Rx**.

Se puede usar cualquier editor de código basado en Windows que admita R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o RStudio. La descarga de [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] también incluye herramientas de línea de comandos para R habituales, como RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Use nuevos orígenes de datos y contextos de cálculo

Cuando se usa el paquete RevoScaleR para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], busque estas funciones para usar en el código de R:

+ **RxSqlServerData** es una función incluida en el paquete RevoScaleR para facilitar una conectividad de datos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Esta función se utiliza en el código en R para definir el *origen de datos*. El objeto de origen de datos especifica el servidor y las tablas donde se encuentran los datos y se ocupa de la tarea de leer y escribir datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   El paquete **RxInSqlServer** se puede usar para especificar el *cálculo*.  Dicho de otro modo, puede indicar en qué lugar se debe ejecutar el código en R: en su estación de trabajo local o en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Para obtener más información, consulte [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler).
  
     Al establecer el contexto de cálculo, este solo afecta a los cálculos compatibles con el contexto de ejecución remoto (es decir, las operaciones de R proporcionadas por el paquete RevoScaleR y funciones relacionadas). Normalmente, no se pueden ejecutar soluciones de R basadas en paquetes CRAN estándar en un contexto de cálculo remoto, aunque se pueden ejecutar en el equipo de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] si las inicia T-SQL. Pero se puede usar la función `rxExec` para llamar a funciones individuales de R y ejecutarlas de forma remota en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para obtener ejemplos de cómo crear y trabajar con orígenes de datos y contextos de ejecución, consulte estos tutoriales:

+ [Análisis detallado de ciencia de datos](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Análisis de datos con Microsoft R](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)

## <a name="deploy-r-code-to-production"></a>Implementar código R en producción

Una parte importante de ciencia de datos consiste en proporcionar sus análisis a otras personas o utilizar modelos de predicción para mejorar procesos o resultados empresariales. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], resulta sencillo proceder al entorno de producción cuando su modelo o script en R está listo.

Para obtener más información sobre cómo puede trasladar el código para que se ejecute en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Por lo general, el proceso de implementación empieza por limpiar el script para eliminar los fragmentos de código que no se precisen en el entorno de producción. Conforme se desplaza al acercar los cálculos a los datos, podría encontrar maneras de forma más eficaz mover, resumir o presentar los datos que al hacerlo todo en R.  Se recomienda que consulte a los científicos de datos con un desarrollador de la base de datos sobre las formas de mejorar el rendimiento, especialmente si la solución realiza limpieza de datos o ingeniería de características que podrían ser más eficaces en SQL. Es posible que se necesiten cambios en los procesos ETL para garantizar que los flujos de trabajo destinados a generar o puntuar un modelo no produzcan errores, y que los datos de entrada estén disponibles en el formato correcto.

## <a name="see-also"></a>Vea también

[Comparación de la Base de R y funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)

[Biblioteca de RevoScaleR en SQL Server](ref-r-revoscaler.md)

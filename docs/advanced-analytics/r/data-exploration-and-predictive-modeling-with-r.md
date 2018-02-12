---
title: "Exploración de datos y el modelado de predicción con R | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d7c5430e585d7324e94ebe64e5138246e26049c4
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>Exploración de datos y el modelado de predicción con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tema describe las mejoras en el proceso de ciencia de datos que son posibles mediante la integración con SQL Server.

Se aplica a: SQL Server 2016 R Services, servicios de SQL Server de 2017 máquinas Learnign

## <a name="the-data-science-process"></a>El proceso de ciencia de datos

Los científicos de datos suelen utilizar R para explorar datos y crear modelos de predicción. Habitualmente, esto consiste en un proceso iterativo de ensayo y error hasta que se logra un buen modelo de predicción. Como científico de datos experimentado, se podría conectar a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y capturar los datos para su estación de trabajo local mediante el paquete RODBC, explorar los datos y crear un modelo de predicción mediante paquetes R estándares.

Sin embargo, este enfoque tiene muchos de los inconvenientes, que tengan impedirse la más amplia adopción de R de la empresa. 

+ Movimiento de datos puede ser lento, ineficaz o poco
+ Propio R tiene limitaciones de rendimiento y escalabilidad

Estos inconvenientes resultan más evidentes cuando tenga que mover y analizar grandes cantidades de datos, o bien utilizar conjuntos de datos que no quepan en la memoria disponible en su equipo.

Los nuevos paquetes escalables y funciones de R incluidas con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] le ayudarán a solucionar muchos de estos desafíos. 

## <a name="whats-different-about-revoscaler"></a>¿Cuál es la diferencia RevoScaleR?

El paquete **RevoScaleR** contiene implementaciones de algunas de las funciones de R más populares, que se han rediseñado para ofrecer paralelismo y escalabilidad. Para obtener más información, consulte [informática con RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

El paquete RevoScaleR también permite cambiar el *contexto de ejecución*. Esto significa que, para una solución completa o tan solo una función, puede indicar que los cálculos se deben llevar a cabo con los recursos del equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de su estación de trabajo local. Esto conlleva varias ventajas: evita los movimientos de datos innecesarios y puede aprovechar la mayor cantidad de recursos de cálculo del equipo del servidor.

## <a name="r-environment-and-packages"></a>Paquetes y entorno de R

El entorno de R admitido en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un runtime, el lenguaje de código abierto y un motor de gráficos respaldado y ampliado por diversos paquetes. El lenguaje admite una amplia variedad de extensiones que se implementan mediante paquetes.  

### <a name="using-other-r-packages"></a>Mediante otros paquetes de R

Además de las bibliotecas de R propietarias incluidas con aprendizaje automático de Microsoft, puede utilizar casi todos los paquetes R en la solución, incluidos:

+ Paquetes de R de propósito general de repositorios públicos. Puede conseguir los paquetes de R de código abierto más populares en repositorios públicos, como CRAN, que hospeda más de 6000 paquetes que pueden usar los científicos de datos.
  
  Para la plataforma Windows, los paquetes de R se distribuyen como archivos .zip, que se pueden descargar e instalar bajo la licencia GPL.  
  
  Para obtener más información sobre cómo instalar paquetes de terceros para su uso con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Bibliotecas y paquetes adicionales incluidos en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     El paquete **RevoScaleR** incluye análisis de macrodatos de alto rendimiento, versiones mejoradas de funciones que admiten tareas habituales de la ciencia de datos, mecanismos de aprendizaje optimizados para Bayes naive, regresión lineal, modelos de series de tiempo y redes neuronales, así como bibliotecas de matemáticas avanzadas.  
  
     El paquete **RevoPemaR** permite desarrollar en R sus propios algoritmos de ejecución en paralelo de memoria externa.  
  
     Para obtener más información acerca de estos paquetes y cómo utilizarlas, vea [¿qué es RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) y [empezar a trabajar con RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started). 

+ **MicrosoftML** contiene una colección de transformaciones de datos desde el equipo de ciencia de datos de Microsoft y algoritmos de aprendizaje automático altamente optimizada. Muchos de los algoritmos también se usan en aprendizaje automático de Azure. Para obtener más información, consulte [con el paquete de MicrosoftML](../../advanced-analytics/using-the-microsoftml-package.md).

### <a name="r-development-tools"></a>Herramientas de desarrollo en R

Al desarrollar la solución R, asegúrese de descargar al cliente de Microsoft R. Esta descarga gratuita incluye las bibliotecas necesarias para admitir los contextos de proceso remoto y alorithms escalable:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** una distribución del tiempo de ejecución de R y un conjunto de paquetes, como la biblioteca de matemáticas del kernel de Intel, que potencian el rendimiento de las operaciones estándar de R.  
  
+ **RevoScaleR:** un paquete de R que permite realizar cálculos de inserción en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. También incluye un conjunto de funciones de R habituales que se han rediseñado para ofrecer mejor rendimiento y escalabilidad. Puede identificar estas funciones mejoradas gracias al prefijo **rx** . También incluye proveedores de datos mejorados para una variedad de orígenes. Estas funciones tienen el prefijo **Rx**.

Puede usar cualquier editor de código basado en Windows que admita R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o RStudio. La descarga de [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] también incluye herramientas de línea de comandos para R habituales, como RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Orígenes de datos de uso y contextos de proceso

Cuando se usa el paquete RevoScaleR para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine estas funciones que se va a usar en el código de R:

+ **RxSqlServerData** es una función incluida en el paquete RevoScaleR para facilitar una conectividad de datos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Esta función se utiliza en el código en R para definir el *origen de datos*. El objeto de origen de datos especifica el servidor y las tablas donde se encuentran los datos y se ocupa de la tarea de leer y escribir datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   El paquete **RxInSqlServer** se puede usar para especificar el *cálculo*.  Dicho de otro modo, puede indicar en qué lugar se debe ejecutar el código en R: en su estación de trabajo local o en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Para obtener más información, consulte [funciones de RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
     Al establecer el contexto de cálculo, este solo afecta a los cálculos compatibles con el contexto de ejecución remoto (es decir, las operaciones de R proporcionadas por el paquete RevoScaleR y funciones relacionadas). Normalmente, no se pueden ejecutar soluciones de R basadas en paquetes CRAN estándar en un contexto de cálculo remoto, aunque se pueden ejecutar en el equipo de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] si las inicia T-SQL. Pero se puede usar la función `rxExec` para llamar a funciones individuales de R y ejecutarlas de forma remota en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para obtener ejemplos de cómo crear y trabajar con orígenes de datos y contextos de ejecución, consulte estos tutoriales:

+ [Análisis detallado de ciencia de datos](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Análisis de datos mediante Microsoft R](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>Implementar código R en producción

Una parte importante de ciencia de datos consiste en proporcionar sus análisis a otras personas o utilizar modelos de predicción para mejorar procesos o resultados empresariales. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], resulta sencillo proceder al entorno de producción cuando su modelo o script en R está listo.

Para obtener más información sobre cómo puede trasladar el código para que se ejecute en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Por lo general, el proceso de implementación empieza por limpiar el script para eliminar los fragmentos de código que no se precisen en el entorno de producción. Conforme va moviendo cálculos más cercano a los datos, podría buscar formas de manera más eficaz mover, resumir o presentar los datos que hacerlo todo el contenido de R.  Se recomienda que consulte los científicos de datos con un desarrollador de base de datos sobre las formas de mejorar el rendimiento, especialmente si la solución de limpieza de datos o una característica de ingeniería podría ser más eficaces en SQL. Es posible que se necesiten cambios en los procesos ETL para garantizar que los flujos de trabajo destinados a generar o puntuar un modelo no produzcan errores, y que los datos de entrada estén disponibles en el formato correcto.

## <a name="see-also"></a>Vea también

[Comparación de funciones de Base R y ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[Funciones de ScaleR para trabajar con SQL Server](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)

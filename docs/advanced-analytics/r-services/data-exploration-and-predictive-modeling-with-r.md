---
title: "Exploraci&#243;n de datos y el modelado de predicci&#243;n con R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Exploraci&#243;n de datos y el modelado de predicci&#243;n con R
  Los científicos de datos suelen utilizar R para explorar datos y crear modelos de predicción. Habitualmente, esto consiste en un proceso iterativo de ensayo y error hasta que se logra un buen modelo de predicción. Como científico de datos experimentado, se podría conectar a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y capturar los datos para su estación de trabajo local mediante el paquete RODBC, explorar los datos y crear un modelo de predicción mediante paquetes R estándares.  
  
 Sin embargo, este enfoque tiene inconvenientes. El movimiento de los datos puede ser lento, ineficaz o poco seguro. Además, el propio R tiene limitaciones de rendimiento y escalabilidad. Estos inconvenientes resultan más evidentes cuando tenga que mover y analizar grandes cantidades de datos, o bien utilizar conjuntos de datos que no quepan en la memoria disponible en su equipo.  
  
 Puede superar estos desafíos mediante el uso de los nuevos paquetes escalables e incluyen funciones de R con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. El paquete **RevoScaleR** contiene implementaciones de algunas de las funciones de R más populares, que se han rediseñado para ofrecer paralelismo y escalabilidad. El paquete RevoScaleR también permite cambiar el *contexto de ejecución*. Esto significa que, para una solución completa o tan solo una función, puede indicar que los cálculos se deben llevar a cabo con los recursos del equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de su estación de trabajo local. Esto conlleva varias ventajas: evita los movimientos de datos innecesarios y puede aprovechar la mayor cantidad de recursos de cálculo del equipo del servidor.  
  
 En esta sección se proporcionan instrucciones para científicos de datos sobre cómo usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para desempeñar tareas relacionadas con el desarrollo y las pruebas de soluciones en R.  
  
##  <a name="bkmk_RDevTools"></a> Herramientas de desarrollo en R  
 R el cliente de Microsoft proporciona a científico de datos un entorno completo para desarrollar y probar modelos predictivos. R cliente incluye:  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Una distribución de tiempo de ejecución de R y un conjunto de paquetes, como la biblioteca central de matemáticas Intel, que mejoren el rendimiento de las operaciones estándar de R.  
  
-   **RevoScaleR:** un paquete de R que le permite insertar cálculos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. También incluye un conjunto de funciones comunes de R que se han rediseñado para proporcionar un mejor rendimiento y escalabilidad. Puede identificar estas funciones mejoradas gracias al prefijo **rx** . También incluye proveedores de datos mejorada para una variedad de orígenes; Estas funciones tienen el prefijo **Rx**.  
  
-   **Libertad de elección de las herramientas de desarrollo:** puede usar cualquier editor de código basado en Windows que admita R, como [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o RStudio. La descarga de [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] también incluye herramientas de línea de comandos comunes para R como RGui.exe.  
  
##  <a name="bkmk_packages"></a> Paquetes y entorno de R  
 El entorno de R admitido en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un runtime, el lenguaje de código abierto y un motor de gráficos respaldado y ampliado por diversos paquetes. El lenguaje admite una amplia variedad de extensiones que se implementan mediante paquetes.  
  
 Hay varios orígenes de paquetes de R adicionales que puede utilizar con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] :  
  
  
-   Paquetes de propósito general R desde repositorios públicos. Puede conseguir los paquetes de R de código abierto más populares en repositorios públicos, como CRAN, que hospeda más de 6000 paquetes que pueden usar los científicos de datos.  
  
     Hay otros paquetes disponibles para respaldar análisis predictivos en dominios especiales, como las finanzas, la genómica, etc.  
  
     Para la plataforma Windows, paquetes de R se proporcionan como archivos zip y pueden descargar e instalar bajo la licencia GPL.  
  
     Para obtener información acerca de cómo instalar paquetes de terceros para su uso con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte [instalar paquetes adicionales de R en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   Paquetes adicionales y bibliotecas proporcionadas por [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     El **RevoScaleR** paquete incluye el análisis de grandes volúmenes de datos de alto rendimiento, versiones mejoradas de las funciones que admiten tareas de ciencia de datos comunes, aprendices optimizados para Bayes Naive, regresión lineal, modelos de serie temporal y redes neurales y bibliotecas matemáticas avanzadas.  
  
     El paquete **RevoPemaR** permite desarrollar en R sus propios algoritmos de ejecución en paralelo de memoria externa.  
  
     Para obtener más información acerca de estos paquetes y cómo usarlos, consulte [exploración de datos y modelado predictivo & #40; Tutorial: Servicios de SQL Server R & #41;](../../advanced-analytics/r-services/sql-server-r-services.md).  
  
## Uso de orígenes de datos y contextos de cálculo  
 Cuando se usa el paquete RevoScaleR para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hay algunas nuevas funciones importantes para utilizar en el código de R:  
  
-   [RxSqlServerData](RxSqlServerData.md) es una función que se proporciona en el paquete RevoScaleR para permitir la conectividad de datos mejorada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Esta función se utiliza en el código en R para definir el *origen de datos*. El objeto de origen de datos especifica el servidor y las tablas donde se encuentran los datos y se ocupa de la tarea de leer y escribir datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El [RxInSqlServer](rxInSqlServer.md) función puede utilizarse para especificar el *calcular contexto*.  En otras palabras, puede indicar que se debe ejecutar el código R: en la estación de trabajo local o en el equipo que hospeda el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
     Cuando se establece el contexto de cálculo, afecta sólo cálculos que admiten el contexto de ejecución remota, que significa que las operaciones de R proporcionan por el paquete de RevoScaleR y funciones relacionadas. Normalmente, no se pueden ejecutar soluciones de R basadas en paquetes CRAN estándar en un contexto de proceso remoto, aunque se pueden ejecutar el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo si inicia t-SQL. Sin embargo, puede usar el `rxExec` función para llamar a funciones de R individuales y ejecutarlas de forma remota en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
 Para obtener ejemplos de cómo crear y trabajar con orígenes de datos y contextos de ejecución, vea estos tutoriales:
 
 + [Profundización de ciencia de datos](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [Introducción a RevoScaleR SQL Server](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started).  
  
## Implementación del código en R en entornos de producción  
 Una parte importante de ciencia de datos consiste en proporcionar sus análisis a otras personas o utilizar modelos de predicción para mejorar procesos o resultados empresariales. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], resulta sencillo proceder al entorno de producción cuando su modelo o script en R está listo.  
  
 Para obtener más información acerca de cómo mover el código se ejecute en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [de funcionamiento de código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
 Por lo general, el proceso de implementación empieza por limpiar el script para eliminar los fragmentos de código que no se precisen en el entorno de producción. mover cálculos más próximos a los datos, podría encontrar maneras de mover de manera más eficaz, resumir o presentar los datos que al hacerlo todo en R.  
  
 Se recomienda que consulte científico de datos con un desarrollador de bases de datos sobre las formas de mejorar el rendimiento, especialmente si la solución de limpieza de datos o una característica de ingeniería puede ser más eficaz en SQL. Cambios en los procesos ETL podrían ser necesario para asegurarse de que los flujos de trabajo para generar o un modelo de puntuación no producirán un error y que los datos de entrada están disponibles en el formato correcto.  
  
##  <a name="bkmk_SQLInR"></a> En esta sección  

[Comparación de las funciones de utilizar otros equipos y CRAN R](Summary%20of%20rx%20Functions.md)

[Funciones de utilizar otros equipos para trabajar con SQL Server](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## Vea también  

 
 [Características y tareas de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [Operationalizing Your R Code (Operacionalización del código R)](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  
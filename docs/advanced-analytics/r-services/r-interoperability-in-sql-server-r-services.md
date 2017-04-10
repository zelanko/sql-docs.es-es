---
title: "Interoperabilidad de R en servicios SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Interoperabilidad de R en servicios SQL Server R

En este tema se centra en el mecanismo para ejecutar para R en [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], y se describen las diferencias entre Microsoft R y código abierto R. Para obtener información acerca de los componentes adicionales, consulte [nuevos componentes de SQL Server](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

### Componentes de R abierto

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] incluye una distribución completa de las herramientas y los paquetes de R bases. Para obtener más información acerca de lo que se incluye con la distribución base, consulte la documentación que se instala durante la instalación en la siguiente ubicación predeterminada:
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

Como parte de la instalación de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], debe dar su consentimiento a los términos de la licencia pública GNU. Posteriormente, puede ejecutar paquetes de R estándares sin modificaciones adicionales como haría en cualquier otra distribución de código abierto de R.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no modifica el tiempo de ejecución de R de ninguna manera. El tiempo de ejecución de R se ejecuta fuera de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] procesar y puede ejecutarse independientemente de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Sin embargo, se recomienda encarecidamente que no ejecute estas herramientas mientras [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se usa R, para evitar la contención de recursos.

La distribución del paquete básico de R que está asociada a un determinado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia puede encontrarse en la carpeta asociada a la instancia. Por ejemplo, si instaló los servicios de R en la instancia predeterminada, las bibliotecas de R se encuentran en `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.

De forma similar, las herramientas de R asociadas a la instancia predeterminada se encontrarían en `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,

Para obtener más información acerca de la distribución base, consulte [paquetes instalados con Microsoft R Open](https://mran.revolutionanalytics.com/rro/installed/)

### Paquetes de R adicionales

Además de la distribución de R base, [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] incluye algunos paquetes de R propietarios, así como un marco para la ejecución paralela de R y bibliotecas que admitan la ejecución de R en contextos de proceso remoto. 

Este conjunto de características de R - la distribución base de R más las características mejoradas de R y paquetes - combinada se conoce como **Microsoft R**. Si instala el servidor de Microsoft R (independiente), obtendrá exactamente el mismo conjunto de paquetes que se instalan con SQL Server R Services (en bases de datos), pero en una carpeta diferente. 

R Microsoft incluye una distribución de la biblioteca central de matemáticas de Intel, que se utiliza siempre que sea posible para el procesamiento más rápido de matemático. Por ejemplo, la biblioteca básica lineal de álgebra (BLAS) se utiliza para muchos de los paquetes de complemento, así como para R propio. Para obtener más información, vea estos artículos:

+ [Cómo el núcleo de matemáticas Intel acelera R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [Ventajas de rendimiento de vinculación de R a bibliotecas matemáticas multiproceso](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Entre las adiciones más importantes a R de Microsoft son el **RevoScaleR** y **RevoPemaR** paquetes. Estos son los paquetes de R que se han escrito en gran medida en C o C++ para mejorar el rendimiento.

+ **RevoScaleR.** Incluye una serie de API de análisis y manipulación de datos. Las API se han optimizado para analizar los conjuntos de datos que son demasiado grandes para caber en la memoria y para realizar cálculos que se distribuye a través de varios núcleos o procesadores.

   Las APIs RevoScaleR también admiten el trabajo con subconjuntos de datos para una mayor escalabilidad. En otras palabras, la mayoría de las funciones de RevoScaleR puede operar en fragmentos de datos y utiliza algoritmos para agregar los resultados de la actualización. Por lo tanto soluciones de R basadas en las funciones de RevoScaleR pueden trabajar con grandes conjuntos de datos y no están limitadas por la memoria local.

  El paquete RevoScaleR también admite la. Formato de archivo XDF para más rápido movimiento y el almacenamiento de datos utilizados para el análisis. El formato XDF usa almacenamiento en columnas, es portátil y puede usarse para cargar y manipular datos desde diversos orígenes, incluidos texto, SPSS o una conexión ODBC. Se proporciona un ejemplo de cómo usar el formato XDF en este tutorial: [profundización de ciencia de datos](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR.** PEMA significa algoritmo paralelo de memoria externa. El **RevoPemaR** paquete proporciona API que puede usar para desarrollar sus propios algoritmos paralelos. Para obtener más información, consulte [RevoPemaR Guía de introducción a](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started).

## Vea también
[Información general sobre la arquitectura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[Los nuevos componentes de SQL Server para admitir servicios de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[Información general sobre seguridad](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

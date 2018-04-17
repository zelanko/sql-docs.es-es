---
title: Interoperabilidad de R en SQL Server R Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 59196e0569ac9cc683b3affa68fc17f068e74994
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="r-interoperability-in-sql-server"></a>Interoperabilidad de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tema se centra en el mecanismo de ejecución de R en SQL Server y se describe las diferencias entre Microsoft R y código abierto R.

Se aplica a: servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

Para obtener información acerca de los componentes adicionales, consulte [nuevos componentes de SQL Server](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md).

### <a name="open-source-r-components"></a>Componentes de R de código abierto

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] incluye una distribución completa de las herramientas y los paquetes básicos de R. Para más información sobre qué se incluye con la distribución básica, vea la documentación que se instala durante la instalación en la siguiente ubicación predeterminada: `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

Como parte de la instalación de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], debe aceptar las condiciones de la licencia pública de GNU. Cuando lo haga, podrá ejecutar paquetes de R estándar sin tener que realizar ninguna modificación más, tal y como sucede en cualquier otra distribución de código abierto de R.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no modifica el tiempo de ejecución de R de ninguna manera. El tiempo de ejecución de R se ejecuta fuera del proceso de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y se puede ejecutar independientemente de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. A pesar de ello, se recomienda encarecidamente no ejecutar estas herramientas mientras [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usa R, para evitar la contención de recursos.

La distribución de paquetes básica de R que está asociada a una determinada instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está en la carpeta asociada a la instancia. Por ejemplo, si instaló R Services en la instancia predeterminada, las bibliotecas de R se encuentran en esta carpeta de forma predeterminada:

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library

De forma similar, las herramientas de R asociadas con la instancia predeterminada se encontrarían en este carpeta predeterminada:

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin

Para obtener más información acerca de cómo Microsoft R es diferente de una distribución de base de R que puede obtener de CRAN, consulte [interoperabilidad con lenguaje R y productos de Microsoft R y características](https://docs.microsoft.com/en-us/r-server/what-is-r-server-interoperability)

### <a name="additional-r-packages-from-microsoft-r"></a>Paquetes de R adicionales de Microsoft R

Además de la distribución de R base, [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] incluye algunos paquetes de R propietarios, así como un marco para la ejecución en paralelo de R que también admite la ejecución de R en contextos de proceso remoto.

Este conjunto combinado de características de R (es decir, la distribución de R básica más las características y paquetes mejorados de R) se conoce como **Microsoft R**. Si instala Microsoft R Server (independiente), obtendrá exactamente el mismo conjunto de paquetes que se instalan con SQL Server R Services (en base de datos), pero en una carpeta diferente.

Microsoft R incluye una distribución de la biblioteca Intel Math Kernel, que se usa siempre que se puede para realizar procesamientos matemáticos más rápidos. Por ejemplo, la biblioteca de álgebra lineal básica (BLAS) se usa en muchos de los paquetes de complemento, así como en el propio R. Para más información, vea estos artículos:

+ [How the Intel Math Kernel Speeds up R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html) (Modo en que Intel Math Kernel acelera R)
+ [Performance benefits of linking R to multithreaded math libraries](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html) (Ventajas de rendimiento al vincular R a bibliotecas matemáticas multiproceso)

Dos de los aspectos más importantes que se han agregado a Microsoft R son los paquetes **RevoScaleR** y **RevoPemaR**. Son paquetes de R que se han escrito en gran medida en C o C++ para mejorar el rendimiento.

+ **RevoScaleR.** Incluye diversas API de análisis y manipulación de datos. Estas API se han optimizado para analizar los conjuntos de datos que son demasiado grandes para caber en la memoria, así como para realizar cálculos que se distribuyen a través de varios núcleos o procesadores.

   Las API de RevoScaleR también funcionan con subconjuntos de datos para una mayor escalabilidad. En otras palabras, la mayoría de las funciones de RevoScaleR puede operar en fragmentos de datos y usa algoritmos de actualización para agregar los resultados. Por lo tanto, las soluciones de R basadas en las funciones de RevoScaleR funcionan con conjuntos de datos muy voluminosos y no están limitadas por la memoria local.

  El paquete RevoScaleR también admite el formato de archivo .XDF, lo que permite mover y almacenar más rápidamente los datos usados en los análisis. El formato XDF usa el almacenamiento en columnas, es portátil y se puede usar para cargar y manipular datos procedentes de distintos orígenes, como texto, SPSS o una conexión ODBC. 

+ **RevoPemaR.** El acrónimo PEMA corresponde a "Parallel External Memory Algorithm" (algoritmo de memoria externa en paralelo). El paquete **RevoPemaR** proporciona diversas API que sirven para que pueda desarrollar sus propios algoritmos de ejecución en paralelo. Para más información, vea la [guía de introducción a RevoPemaR](https://docs.microsoft.com/r-server/r/how-to-developer-pemar).

También le recomendamos que intente [MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package), un nuevo paquete de R de Microsoft que admite la ejecución remota de código de R y escalable, procesamiento, distribuido con algoritmos de aprendizaje de automático mejorado desarrollada por Microsoft Research.

## <a name="next-steps"></a>Pasos siguientes

[Información general sobre la arquitectura](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

[Componentes de SQL Server al soporte técnico de R](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)

[Información general sobre seguridad](../../advanced-analytics/r/security-overview-sql-server-r.md)


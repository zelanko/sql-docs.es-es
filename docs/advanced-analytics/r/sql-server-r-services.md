---
title: "Servicios de aprendizaje de máquina SQL Server | Documentos de Microsoft"
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 136df79ded4c86a183d78ecc39821550ca9c24c9
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-machine-learning-services"></a>Machine Learning Services en SQL Server

Servicios de aprendizaje de SQL Server de 2017 máquina (anteriormente SQL Server 2016 R Services) proporciona una plataforma para desarrollar e implementar aplicaciones inteligentes que descubran nuevos datos relevantes. Dado que aprendizaje automático se integra con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.
  
+ En SQL Server 2016, fácilmente puede desarrollar e implementar soluciones basadas en el popular lenguaje R de ciencia de datos. 

    Las características incluyen la [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) bibliotecas, que proporcionan nueva escalabilidad y rendimiento para las soluciones de R y algoritmos de última generación en [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).
+ En SQL Server 2017, puede usar R y Python para desarrollar y comenzar a soluciones de ciencia de datos. 

    El [revoscalepy](../python/what-is-revoscalepy.md) biblioteca para Python ofrece contextos de proceso remoto y la escalabilidad comparable a las de RevoScaleR.

SQL Server admite un mejor rendimiento, seguridad y facilidad de uso para cargas de trabajo de aprendizaje de máquina a través de un conjunto completo de herramientas y tecnologías. Puede implementar soluciones mediante cómoda de R o Python, familiarizado metodología SQL y herramientas. Puede utilizar [!INCLUDE[tsql](../../includes/tsql-md.md)] para llamar a los tiempos de ejecución de R o Python desde las aplicaciones de producción, para generar modelos o recuperar los objetos visuales. Si ya ha entrenado un modelo, puede generar predicciones de él mediante sólo T-SQL, a través de [puntuación native](../sql-native-scoring.md).

## <a name="machine-learning-in-sql-server-2017"></a>Aprendizaje de SQL Server 2017 automático

+ Instalar **Machine Learning Services (In-Database)** durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para habilitar la ejecución segura de scripts de R o Python en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
    Cuando se selecciona esta característica, las extensiones se instalan en el motor de base de datos para admitir la ejecución del código escrito de R o Python. Se crea un nuevo servicio, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para administrar las comunicaciones entre los tiempos de ejecución externos y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
  
+ Instalar **aprendizaje de máquina de Microsoft Server (independiente)** en un equipo independiente si no necesita usar SQL Server como el contexto de proceso. Servidor de aprendizaje de máquina incluye los mismos componentes de aprendizaje de máquina, así como la capacidad de ejecutar trabajos de aprendizaje automático escalable y distribuida como un servicio web.
  
+ Instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) en equipos remotos para desarrollar soluciones que se pueden implementar en SQL Server o al servidor de aprendizaje de máquina en Windows, Linux o Hadoop.

## <a name="machine-learning-in-sql-server-2016"></a>Aprendizaje de SQL Server 2016 automático

+ Instalar **R Services (In-Database)** durante la instalación de SQL Server 2016 para habilitar la ejecución segura de scripts de R en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
    Cuando se selecciona esta característica, obtendrá la capacidad para ejecutar script de R mediante SQL Server como el contexto de proceso, o para ejecutar un script de R en un procedimiento almacenado.
  
+ Instalar **Microsoft R Server (independiente)** del programa de instalación de SQL Server 2016, para instalar los componentes de R en un equipo independiente que puede usar para desarrollar o implementar soluciones en R.

## <a name="how-to-get-started"></a>Cómo empezar

El programa de instalación de SQL Server proporciona dos opciones:

+ Instalación de características que es el análisis de bases de datos se integra con SQL Server, o
+ Instale la versión independiente del servidor de aprendizaje de máquina (o Microsoft R Server) que admite el aprendizaje de automático a escala sin una instancia de SQL Server.

Si tiene que ejecutar el código de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mediante procedimientos almacenados o mediante el uso de la instancia de SQL Server como el contexto de proceso, debe instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] tal y como se describe en el [Guía de instalación](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md). Esta opción proporciona seguridad de máximo de los datos y la integración con herramientas de SQL Server.

Aprendizaje de máquina de Microsoft Server (independiente) es una opción independiente diseñada para usar el [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) y [relacionados con las bibliotecas de Python](../python/what-is-revoscalepy.md) en un equipo de Windows que no se está ejecutando SQL Server. Esta opción requiere una licencia de Enterprise Edition de SQL Server.
    
Se recomienda instalar el servidor de aprendizaje de máquina (independiente) en un equipo portátil o en otro equipo remoto que se utiliza para el desarrollo y utilizar el equipo para crear y probar soluciones de aprendizaje automático que se pueden implementar fácilmente a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es decir ejecutar servicios de aprendizaje de máquina \(en bases de datos\) u otro contexto de proceso admite.
  
También puede usar el **mrsdeploy** paquete que se instala con el servidor de aprendizaje de máquina para publicar y distribuir trabajos de R y Python como un servicio web.

## <a name="additional-resources"></a>Recursos adicionales

+ [Introducción a servicios de aprendizaje de máquina de SQL Server](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Se describen escenarios comunes para los usos de R con SQL Server

+ [Configurar servicios de aprendizaje de máquina de SQL Server o R Services en bases de datos](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Instalar componentes de base de datos asociada y R como parte del programa de instalación de SQL Server
  
+ [Tutoriales de SQL Server y R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Aprenda a crear orígenes de datos de SQL Server en su código R y a usar contextos de computación remotos. Otros tutoriales dirigidos a desarrolladores de SQL muestran cómo entrenar e implementar un modelo de R en SQL Server.

---
title: "Servicios de aprendizaje de máquina SQL Server | Documentos de Microsoft"
ms.date: 11/09/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: fb770b52f2cacfc527f6bb89955acfbda243c18a
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2017
---
# <a name="sql-server-machine-learning-services"></a>Machine Learning Services en SQL Server

  Servicios de aprendizaje de SQL Server de 2017 máquina (anteriormente SQL Server 2016 R Services) proporciona una plataforma para desarrollar e implementar aplicaciones inteligentes que descubran nuevos datos relevantes. Puede usar el lenguaje R enriquecido y eficaz, así como los numerosos paquetes de la comunidad, para crear modelos y generar predicciones mediante sus datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
  Dado que aprendizaje automático se integra con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede realizar el análisis en lugar donde residen los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.
  
SQL Server admite el lenguaje de código abierto de R con un conjunto completo de herramientas y tecnologías que ofrecen un rendimiento superior, seguridad, confiabilidad y facilidad de uso. Puede implementar soluciones en R con herramientas SQL cómodos y familiares, y las aplicaciones de producción pueden llamar al runtime de R y recuperar las predicciones y objetos visuales con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También obtendrá el [Microsoft R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) bibliotecas para mejorar la escalabilidad y rendimiento de las soluciones de R, incluidos RevoScaleR, revoscalepy y MicrososftML.
  
La instalación de SQL Server le permite instalar componentes de servidor y de cliente.
  
## <a name="machine-learning-in-sql-server-2017"></a>Aprendizaje de SQL Server 2017 automático

+ Instalar **Machine Learning Services (In-Database)** durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para habilitar la ejecución segura de scripts de R o Python en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
    Cuando se selecciona esta característica, las extensiones se instalan en el motor de base de datos para admitir la ejecución del código escrito de R o Python. Se crea un nuevo servicio, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para administrar las comunicaciones entre los tiempos de ejecución externos y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
  
+ Instalar **aprendizaje de máquina de Microsoft Server (independiente)** en un equipo independiente si no necesita usar SQL Server como el contexto de proceso. Servidor de aprendizaje de máquina incluye los mismos componentes de aprendizaje de máquina, así como la capacidad de ejecutar trabajos de aprendizaje automático escalable y distribuida como un servicio web.
  
+    Instalar [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client) en equipos remotos para desarrollar soluciones que se pueden implementar en SQL Server o al servidor de aprendizaje de máquina en Windows, Linux o Hadoop.

## <a name="machine-learning-in-sql-server-2016"></a>Aprendizaje de SQL Server 2016 automático

+ Instalar **R Services (In-Database)** durante la instalación de SQL Server 2016 para habilitar la ejecución segura de scripts de R en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.
  
    Cuando se selecciona esta característica, obtendrá la capacidad para ejecutar script de R mediante SQL Server como el contexto de proceso, o para ejecutar un script de R en un procedimiento almacenado.
  
+   Instalar **Microsoft R Server (independiente)** del programa de instalación de SQL Server 2016, para instalar los componentes de R en un equipo independiente que puede usar para desarrollar o implementar soluciones en R.


## <a name="which-type-of-machine-learning-service-do-i-need"></a>¿Qué tipo de servicio de aprendizaje de máquina es necesario?

+ Si tiene que ejecutar el código de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mediante procedimientos almacenados o mediante el uso de la instancia de SQL Server como el contexto de proceso, debe instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] tal como se describe [aquí](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

+ Aprendizaje de máquina de Microsoft Server (independiente) es una opción independiente diseñada para usar el [Microsoft R](https://docs.microsoft.com/r-server/r-reference/introducing-r-server-r-package-reference) y [relacionados con las bibliotecas de Python](../python/what-is-revoscalepy.md) en un equipo de Windows que no se está ejecutando SQL Server. Sin embargo, requiere una licencia de Enterprise Edition de SQL Server.
    
    Se recomienda instalar el servidor de aprendizaje de Microsoft máquina (independiente) en un equipo portátil o en otro equipo remoto que se utiliza para el desarrollo y utilizar el equipo para crear y probar soluciones de aprendizaje de máquina que se pueden implementar fácilmente a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está ejecutando servicios de aprendizaje de máquina \(en bases de datos\) u otro contexto de proceso admite.
  
    También puede usar el **mrsdeploy** paquete que se instala con el servidor de aprendizaje de máquina para publicar y distribuir trabajos de R y Python como un servicio web.

## <a name="additional-resources"></a>Recursos adicionales

+ [Introducción a SQL Server R Services](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Se describen escenarios comunes para los usos de R con SQL Server

+ [Configurar SQL Server R Services (en bases de datos)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Instalar componentes de base de datos asociada y R como parte del programa de instalación de SQL Server
  
+ [Tutoriales de SQL Server R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Aprenda a crear orígenes de datos de SQL Server en su código R y a usar contextos de computación remotos. Otros tutoriales dirigidos a desarrolladores de SQL muestran cómo entrenar e implementar un modelo de R en SQL Server.

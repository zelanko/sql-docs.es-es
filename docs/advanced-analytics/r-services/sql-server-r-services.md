---
title: "SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] proporciona una plataforma para desarrollar e implementar aplicaciones inteligentes que descubran nuevos datos relevantes. Puede usar el lenguaje R enriquecido y eficaz, así como los numerosos paquetes de la comunidad, para crear modelos y generar predicciones mediante sus datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dado que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] integra el lenguaje R con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede realizar el análisis en lugar donde residen los datos, además de eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] admite el lenguaje de código abierto R con un conjunto completo de herramientas y tecnologías de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ofrecen un nivel superior de rendimiento, seguridad, confiabilidad y facilidad de uso. Puede implementar soluciones en R con herramientas conocidas y cómodas. Asimismo, las aplicaciones de producción pueden llamar al runtime de R y recuperar las predicciones y los efectos visuales mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. También obtendrá las bibliotecas de [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), que le permitirán mejorar la escala y el rendimiento de sus soluciones en lenguaje R.  
  
La instalación de SQL Server le permite instalar componentes de servidor y de cliente.  
  
+   **R Services (In-Database):** instale esta característica durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar la ejecución segura de scripts de R en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Cuando seleccione esta característica, las extensiones se instalarán en el motor de base de datos para poder ejecutar scripts de R. Además, se crea un nuevo servicio, [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], que administra las comunicaciones entre el tiempo de ejecución de R y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
+   **Microsoft R Server (independiente):** una distribución de R de código abierto combinada con paquetes de propiedades que admite el procesado en paralelo y otras mejoras de rendimiento. Tanto los servicios de R (en bases de datos) como Microsoft R Server (independiente) incluyen el tiempo de ejecución y los paquetes de R base, así como las bibliotecas de **ScaleR**, para proporcionar más conectividad y un mayor rendimiento. 
  
+    El [cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/index#mrc) está disponible como un instalador independiente y gratuito.  Puede usar el cliente de Microsoft R para desarrollar soluciones que se puedan implementar en servicios de R en SQL Server o en Microsoft R Server si se ejecuta Windows, Teradata o Hadoop. 
     

  > [!NOTE] Si necesita ejecutar código de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], instale [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] según estas [instrucciones](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).
  >  
  > Microsoft R Server \((independiente)\) es una opción independiente diseñada para usar las bibliotecas de ScaleR en equipos Windows que no ejecuten SQL Server. 
>   
>  Sin embargo, si dispone de Enterprise Edition, se recomienda que instale Microsoft R Server \((independiente)\) en un portátil o en otro equipo que se use para el desarrollo en R o para crear soluciones de R que se puedan implementar fácilmente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecute R Services \((en bases de datos)\).
  
## <a name="additional-resources"></a>Recursos adicionales  
  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 Describe escenarios comunes de usos de R con SQL Server.  
  
[Configurar SQL Server R Services (en bases de datos)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
Instalar R y componentes de bases de datos asociados a este como parte de la configuración de SQL Server.  
  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
Aprenda a crear orígenes de datos de SQL Server en su código R y a usar contextos de computación remotos. Otros tutoriales dirigidos a desarrolladores de SQL muestran cómo entrenar e implementar un modelo de R en SQL Server.  
  
## <a name="see-also"></a>Vea también  
  
 [Introducción a Microsoft R Server &#40;independiente&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  
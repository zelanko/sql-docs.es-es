---
title: "Escenario de Tutorial de Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# Escenario de Tutorial de Analysis Services
Este tutorial se basa en [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], una compañía ficticia. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] es una multinacional dedicada a la fabricación y distribución de bicicletas de metal y de metal compuesto en mercados de Norteamérica, Europa y Asia. Las oficinas centrales de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] se encuentran en Bothell, Washington, donde la compañía tiene 500 trabajadores. Además, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] tiene contratados a varios equipos de ventas regionales en toda su base de mercado.  
  
En los últimos años, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] compró una pequeña planta de fabricación, Importadores Neptuno, situada en México. Importadores Neptuno fabrica varios subcomponentes muy importantes para la línea de productos de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . Estos subcomponentes se envían a la sede de Bothell para el ensamblado final del producto. En el año 2005, Importadores Neptuno pasó a ser el único fabricante y distribuidor del grupo de productos de bicicletas de paseo.  
  
Tras un año fiscal con muy buenos resultados, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] desea ampliar su cuota de mercado dirigiendo sus ventas a sus mejores clientes, ampliando la disponibilidad de sus productos en un sitio web externo y reduciendo los costos de venta a través de costos de producción más bajos.  
  
## Entorno de análisis actual  
Para dar respuesta a las necesidades de análisis de datos de los equipos de ventas y de marketing, la compañía obtiene actualmente los datos transaccionales de la base de datos [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] y la información que no corresponde a las transacciones, como las cuotas de venta, la obtiene de hojas de cálculo y consolida toda esta información en el almacenamiento de datos relacionales **AdventureWorksDW2012**. No obstante, el almacenamiento de datos relacional presenta los siguientes problemas:  
  
-   Los informes son estáticos. Los usuarios no pueden explorar de forma interactiva los datos de los informes para obtener información más detallada, como podían hacer con una tabla dinámica de [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel. Aunque el conjunto existente de informes predefinidos es suficiente para muchos usuarios, los usuarios más avanzados necesitan un acceso de consulta directo a la base de datos para realizar consultas interactivas y obtener informes especializados. No obstante, debido a la complejidad de la base de datos **AdventureWorksDW2012** , se necesita demasiado tiempo para que estos usuarios puedan aprender a crear consultas eficaces.  
  
-   El rendimiento de las consultas es muy variable. Por ejemplo, algunas consultas devuelven resultados con gran rapidez, en pocos segundos, mientras que otras tardan varios minutos en devolverlos.  
  
-   Es difícil administrar las tablas agregadas. En un intento de mejorar los tiempos de respuesta de las consultas, el equipo de almacenamiento de datos de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] creó varias tablas agregadas en la base de datos **AdventureWorksDW2012** . Por ejemplo, crearon una tabla que resumía las ventas por mes. No obstante, si bien estas tablas mejoran notablemente el rendimiento de las consultas, la infraestructura creada para mantener las tablas a lo largo del tiempo es frágil y propensa a errores.  
  
-   Las definiciones de informe incluyen lógica de cálculo muy compleja que es difícil de compartir entre informes. Puesto que esta lógica empresarial se genera de forma independiente para cada informe, a veces la información de resumen es distinta entre los informes. Por consiguiente, el equipo de dirección tiene una confianza limitada en los informes del almacenamiento de datos.  
  
-   Los usuarios de distintas unidades empresariales están interesados en distintas vistas de los datos. Cada grupo se distrae y confunde con los elementos de datos que no son relevantes para él.  
  
-   La lógica de cálculo es especialmente difícil para los usuarios que necesitan informes especializados. Estos usuarios deben definir la lógica de cálculo de forma independiente para cada informe, por lo que no existe un control centralizado sobre el modo de definir la lógica de cálculo. Por ejemplo, algunos usuarios saben que deben utilizar técnicas estadísticas básicas, como medias móviles, pero no saben cómo construir estos cálculos y, por consiguiente, no utilizan dichas técnicas.  
  
-   Es difícil combinar los conjuntos de información relacionados. Resulta difícil para los usuarios de la compañía crear consultas especializadas que combinen dos conjuntos de información relacionada, como ventas y cuotas de ventas. Las consultas de este tipo han sobrecargado la base de datos, por lo que la compañía requiere que los usuarios soliciten al equipo del almacenamiento de datos conjuntos de datos comunes entre varias áreas. Como consecuencia de ello, se han definido pocos informes predefinidos que combinan datos de varias áreas temáticas. Además, debido a la complejidad de estos informes, los usuarios son reacios a intentar modificarlos.  
  
-   Los informes se basan principalmente en información de compañías de Estados Unidos. Los usuarios que se encuentran en sedes fuera de Estados Unidos no están satisfechos con este enfoque y desean poder ver los informes en distintas monedas y en distintos idiomas.  
  
-   Es difícil auditar la información. Actualmente, el departamento de finanzas usa la base de datos **AdventureWorksDW2012** solo como origen de datos en la que pueden realizarse consultas masivas. Luego descargan los datos en hojas de cálculo individuales e invierten mucho tiempo en preparar los datos y manipular dichas hojas de cálculo. Por consiguiente, el proceso de preparación, auditoría y administración de los informes financieros de la compañía es complejo.  
  
## Solución  
Recientemente, el equipo del almacenamiento de datos ha realizado una revisión del diseño del sistema de análisis actual. La revisión ha incluido un análisis de las lagunas que presentan los problemas actuales y las demandas futuras. Este equipo ha determinado que la base de datos **AdventureWorksDW2012** es una base de datos dimensional bien diseñada con dimensiones compatibles y claves suplentes. Las dimensiones compatibles permiten utilizar una dimensión en varios puestos de datos, como una dimensión de tiempo o una dimensión de producto. Las claves suplentes son claves artificiales que vinculan tablas de dimensiones y de hechos y se utilizan para garantizar la unicidad y mejorar el rendimiento. Además, el equipo de almacenamiento de datos ha determinado que actualmente no existen problemas significativos con la carga y la administración de las tablas base de la base de datos **AdventureWorksDW2012** . Por tanto, el equipo ha decidido usar [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para poder hacer lo siguiente:  
  
-   Proporcionar el acceso a datos unificados a través de una capa de metadatos común para la creación de informes y el análisis analítico.  
  
-   Simplificar la vista de datos de los usuarios, acelerando el desarrollo de consultas interactivas y predefinidas, y de informes predefinidos.  
  
-   Crear correctamente consultas que combinan datos de varias áreas temáticas.  
  
-   Administrar los agregados.  
  
-   Almacenar y reutilizar cálculos complejos.  
  
-   Presentar una versión traducida a los usuarios de la compañía que se encuentran fuera de Estados Unidos.  
  
Las lecciones del tutorial de Analysis Services proporcionan instrucciones para crear una base de datos de cubo que satisfaga todos estos objetivos. Para empezar, vaya a la primera lección: [Lesson 1: Create a New Tabular Model Project](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## Vea también  
[Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
  
  

---
title: "Introducci&#243;n a la arquitectura (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Introducci&#243;n a la arquitectura (SQL Server R Services)
Esta sección proporciona información general de la arquitectura de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], incluida la seguridad, los nuevos componentes agregados en el motor de base de datos de SQL Server a componentes de compatibilidad con R y la interoperabilidad de scripts de R abierto que se ejecutan en SQL Server.


## Objetivos


La arquitectura de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] está diseñado para admitir el lenguaje R abierto. Los usuarios actuales de R deben ser capaz de portar su código R y ejecutarlo en T-SQL con relativamente pequeñas modificaciones.

Sin embargo, SQL Server R Services también ofrece innovaciones que ofrecen un mayor rendimiento y una mayor integración de la base de datos para el lenguaje R, para habilitar el procesamiento y el rendimiento más rápido y para reducir los obstáculos para el desarrollo empresarial de soluciones de R. Estas innovaciones incluyen código abierto y propietarios componentes desarrollados por Microsoft.


Son los objetivos principales de la integración con SQL Server proporcionar rendimiento y escalabilidad mejorados para R, mientras que la administración de datos de forma segura. Hacia este objetivo, R servicios de SQL Server proporciona una infraestructura de varios proceso que admite la autenticación de Windows integrada y basada en contraseña inicios de sesión SQL. 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] Proporciona una distribución de base de R, junto con los paquetes de utilizar otros equipos y la capacidad de ejecutar tareas de R en paralelo.
+ Los nuevos componentes de SQL Server proporcionan un marco seguro y de alto rendimiento para la ejecución de scripts externos.
+ Las tareas de R se ejecutan fuera del proceso de SQL Server, para proporcionar seguridad y mayor capacidad de administración.
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] administra la seguridad de todos los procesos de R. 

Para ayudarle a optimizar el código R existente y beneficiarse de estas mejoras, los temas de esta sección describen la nueva arquitectura en detalle. Si comprende cómo se controla el procesamiento de datos y análisis [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], puede realizar decisiones adecuadas sobre cómo introducir datos, cómo realizar ingeniería de características de forma más eficaz y cómo consumir los resultados.
 

## En esta sección
+ [Interoperabilidad de R](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [Los nuevos componentes de SQL Server para los servicios de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [Información general sobre seguridad](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## Vea también
[Tutoriales de servicios de R](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)

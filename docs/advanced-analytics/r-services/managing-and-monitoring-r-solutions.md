---
title: "Administraci&#243;n y supervisi&#243;n de soluciones en R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Administraci&#243;n y supervisi&#243;n de soluciones en R
  Los administradores de bases de datos deben integrar prioridades y proyectos opuestos en un único punto de contacto: el servidor de la base de datos. Deben proporcionar acceso a los datos no solo a los científicos de datos, sino a una amplia variedad de desarrolladores de informes, analistas empresariales y consumidores de datos empresariales. Además, deben hacerlo a la vez que mantienen los almacenes de datos de informes y operativos en buen estado. En las empresas, estos profesionales desempeñan un papel esencial en la creación e implementación de una infraestructura eficaz para cultivar la ciencia de datos. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece numerosas ventajas para los administradores de bases de datos que respalden las iniciativas de ciencias de datos.  
  
-   **Securidad.** La arquitectura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege las bases de datos y aísla la ejecución de las sesiones de R del funcionamiento de la instancia de la base de datos.  
  
     Puede especificar quién tiene permiso para ejecutar los scripts de R y garantizar que los datos utilizados en las tareas de dicho lenguaje de programación se administran con los mismos roles de seguridad que los definidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Confiabilidad.** Las sesiones de R se ejecutan en un proceso independiente para garantizar que el servidor sigue ejecutándose como de costumbre, aunque surja algún problema en dichas sesiones. Cuentas de usuario físico con pocos privilegios se utilizan para contener y aislar las instancias de R.   
  
-   **Gobierno de los recursos.** Puede controlar la cantidad de recursos asignados al runtime de R y, de este modo, evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.  
  
  
## En esta sección  
 [Supervisión de los servicios de R](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [Regulador de recursos para servicios de R](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[Instalación y administración de paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[Configuración](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [Configuración y administración de Extensiones de análisis avanzados](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [Modificar el grupo de cuentas de usuario de SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [Consideraciones de seguridad para un runtime de R en SQL Server](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## Vea también  
 [Características y tareas de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  
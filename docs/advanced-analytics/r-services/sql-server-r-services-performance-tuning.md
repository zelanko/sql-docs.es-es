---
title: "Optimizaci&#243;n del rendimiento de servicios de SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Optimizaci&#243;n del rendimiento de servicios de SQL Server R
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] proporciona una plataforma para desarrollar aplicaciones inteligentes que descubran nuevos datos relevantes. Un científico de datos puede utilizar el poder del lenguaje R para entrenar y crear modelos con datos almacenados dentro de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Una vez que el modelo esté listo para producción, un científico de datos puede trabajar con los administradores de base de datos y los ingenieros SQL para implementar su solución en producción. La información de esta sección proporciona instrucciones de nivel alto acerca del ajuste de rendimiento al crear y entrenar modelos y modelos de implementación en producción.

En este documento se supone que está familiarizado con [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] conceptos y terminología. Para obtener información general sobre servicios de R, consulte [R servicios de SQL Server](../../advanced-analytics/r-services/sql-server-r-services.md).

> [!NOTE]
> Aunque gran parte de la información de esta sección es orientación general sobre la configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], alguna información es específica para las funciones analíticas RevoScaleR.

## En esta sección

* [Configuración de SQL Server](../../advanced-analytics/r-services/sql-server-configuration-r-services.md): este documento proporciona instrucciones para configurar el hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se instala en. Es muy útil para __los administradores de base de datos__.

* [R y optimización de datos](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md): este documento ofrece orientación sobre el uso de scripts de R con los servicios de R. Es muy útil para __datos científicos__.

* [Caso práctico de rendimiento](../../advanced-analytics/r-services/performance-case-study-r-services.md): este documento proporciona datos de prueba y los scripts de R que pueden utilizarse para probar el efecto de instrucciones que se proporcionan en los documentos anteriores.

## Referencias

Los siguientes son vínculos a información que se usa en el desarrollo de este documento.

* [Cómo determinar el tamaño del archivo de página adecuado para versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880)

* [Comprimir datos](../../relational-databases/data-compression/data-compression.md)

* [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Deshabilitar compresión de una tabla o un índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [Herramienta de prueba de rendimiento o generador DISKSPD almacenamiento carga](https://github.com/microsoft/diskspd)

* [Referencia de utilidad FSUtil](https://technet.microsoft.com/library/cc753059.aspx)

* [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [Opciones de optimización de rendimiento para rxDForest y rxDTree](https://support.microsoft.com/kb/3104235)

* [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [Guía del usuario de RevoScaleR](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

## Vea también

 
 [Configuración de SQL Server para los servicios de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Caso práctico de rendimiento](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R y optimización de datos](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)
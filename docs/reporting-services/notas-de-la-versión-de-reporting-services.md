---
title: "Versi&#243;n preliminar t&#233;cnica de informes de Power BI en SSRS: notas de la versi&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Notas de la versi&#243;n de Reporting Services
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  Versión preliminar técnica de informes de Power BI en SQL Server Reporting Services de enero de 2017|

En este tema se describen las limitaciones y los problemas con la versión preliminar técnica de informes de Power BI en SQL Server Reporting Services.

- Para leer sobre las novedades de esta versión, consulte [Novedades de Reporting Services](../reporting-services/novedades-de-sql-server-reporting-services-ssrs.md).

 **Pruébelo:**    
   -   [![Descarga desde el Centro de descarga de Microsoft](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351)  Descargue la versión preliminar técnica de informes de Power BI en SQL Server Reporting Services y Power BI Desktop (SQL Server Reporting Services) desde el **[Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=839351)**


## <a name="january--2017"></a>Enero de 2017

### <a name="report-server"></a>Servidor de informes

- Ahora se admite Https. Esta opción no estaba disponible en la VM de la versión preliminar que se lanzó en octubre de 2016. Para obtener más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).
   - Se requiere Https para usar el complemento de visor web de PowerPoint y exponer informes de Power BI dentro del mismo.
- Ahora se admite el escalado horizontal. Esta opción no estaba disponible en la VM de la versión preliminar que se lanzó en octubre de 2016. Para más información, consulte [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).

### <a name="power-bi-reports"></a>Informes de Power BI

- Los informes de Power BI se deben crear con Power BI Desktop (SQL Server Reporting Services) para que funcionen con SQL Server Reporting Services. Puede descargar Power BI Desktop (SQL Server Reporting Services) desde el Centro de evaluación.
- Los informes de Power BI solo son compatibles con conexiones dinámicas a Analysis Services (tabulares o multidimensionales).
- No hay compatibilidad con objetos visuales personalizados.
- No hay compatibilidad con objetos visuales de R.
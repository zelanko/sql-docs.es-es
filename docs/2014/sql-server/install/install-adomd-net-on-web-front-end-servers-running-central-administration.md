---
title: Instalación de ADOMD.NET en servidores front-end web ejecutando administración central | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f36e00a9393dcbdf1f8cbfe878b8382e6a8dac9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952152"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>Instalar ADOMD.NET en servidores front-end web ejecutando Administración central
  Si instala PowerPivot para SharePoint en una granja que tiene la topología de Administración central, sin Excel Services o PowerPivot para SharePoint, descargue e instale la biblioteca de cliente de Microsoft ADOMD.NET si desea acceso total a los informes integrados en el panel de administración de PowerPivot. Algunos informes del panel usan ADOMD.NET para tener acceso a los datos internos que proporcionan los datos de errores en el procesamiento de las consultas de PowerPivot y el estado del servidor en la granja.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010  
  
 En SharePoint 2013, el proveedor se incluye en el Feature Pack de SQL Server. Para obtener información sobre cómo descargar spPowerPivot. msi, consulte [Microsoft SQL Server Feature Pack 2014](https://www.microsoft.com/download/details.aspx?id=35577)  
  
### <a name="download-and-install-the-client-library"></a>Descargar e instalar la biblioteca de cliente  
  
1.  En la [página SQL Server Feature Pack de 2014](https://go.microsoft.com/fwlink/?LinkID=296473), busque Microsoft ADOMD.net.  
  
2.  Descargue el paquete x64 del programa de instalación de `SQL_AS_ADOMD.msi`.  
  
3.  Ejecute el archivo .msi para instalar la biblioteca.  
  
4.  Restaurar IIS una vez finalizada la instalación. Abra un símbolo del sistema administrativo y escriba **iisreset**.  
  
### <a name="verify-installation"></a>Comprobar la instalación  
  
1.  Vaya a Windows\Assembly.  
  
2.  Haga clic con el botón secundario en Microsoft. AnalysisServices. AdomdClient y seleccione **propiedades**.  
  
3.  Haga clic en **Versión**.  
  
4.  Compruebe que la versión incluye 12,00. \<número de compilación> y que la descripción es Microsoft. AnalysisService. AdomdClient.  
  
## <a name="see-also"></a>Consulte también  
 [Panel de administración de PowerPivot y datos de uso](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)  
  
  

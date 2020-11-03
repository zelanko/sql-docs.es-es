---
title: Iniciar el Generador de informes | Microsoft Docs
description: Generador de informes es un entorno de creación de informes independiente. La primera vez que lo inicie, el Centro de descarga de Microsoft le pedirá que lo descargue.
ms.date: 01/03/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 00a954a23cf9b17a58c3272a03222019400ae891
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907043"
---
# <a name="start-report-builder"></a>Iniciar el Generador de informes

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] es un entorno independiente de creación de informes. Con él, puede crear informes paginados y publicarlos en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo nativo o modo integrado de SharePoint.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  
 La primera vez que inicie [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] desde el portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el modo integrado de SharePoint, se le pedirá que lo descargue del Centro de descarga de Microsoft. 
 
![Captura de pantalla del mensaje "Estamos abriendo el Generador de informes...".](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 El usuario o un administrador también pueden [instalar el Generador de informes en el equipo desde el Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=219138). Vea "Instalación con Systems Manager Server" en [Instalar el Generador de informes](../../reporting-services/install-windows/install-report-builder.md) para obtener más detalles.
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] no se instala al instalar SQL Server Reporting Services; debe descargarlo e instalarlo por separado.  
  
 Al iniciar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] desde el portal web o un sitio de SharePoint, si una versión anterior de [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] se abre, póngase en contacto con el administrador, que puede actualizar la versión en el portal web o en un sitio de SharePoint.  
  
## <a name="to-start-ssrbnoversion-from-the-ssrsnoversion-web-portal"></a>Para iniciar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] desde el portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  En el explorador web, escriba la dirección URL del servidor de informes en la barra de direcciones. De forma predeterminada, la dirección URL es https://\<*servername*>/reports.  
  
2.  En la barra superior del portal web, seleccione **Nuevo** > **Informe paginado**.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     La primera vez, se le pedirá que [instale el Generador de informes](../../reporting-services/install-windows/install-report-builder.md). 
  
     Después de esta primera vez, se abre [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] y puede crear un informe paginado o abrir uno desde el servidor de informes.  
  
## <a name="to-start-ssrbnoversion-in-sharepoint-integrated-mode"></a>Para iniciar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] en el modo integrado de SharePoint  
  
1.  Navegue al sitio de SharePoint que contenga la biblioteca que desee.  
  
2.  Abra la biblioteca.  
  
3.  Haga clic en **Documentos**.  
  
4.  En el menú **Nuevo documento** , haga clic en **Informe del Generador de informes**.  
  
     La primera vez, se inicia el Asistente para el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] de SQL Server. Vea [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) para obtener más detalles.  
  
     Se abre [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] y puede crear un informe paginado o abrir un informe en el servidor de informes.  
  
     **Nota** Si en el menú **Nuevo documento** no aparecen las opciones **Informe del Generador de informes** , **Modelo del Generador de informes** u **Origen de datos de informe** , será necesario agregar sus tipos de contenido a la biblioteca de SharePoint. Para obtener más información, vea [Add Reporting Services Content Types to a SharePoint Library (Agregar los tipos de contenido de Reporting Services a una biblioteca de SharePoint)](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

## <a name="next-steps"></a>Pasos siguientes

[Generador de informes en SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[Establecimiento de opciones predeterminadas para el Generador de informes](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).

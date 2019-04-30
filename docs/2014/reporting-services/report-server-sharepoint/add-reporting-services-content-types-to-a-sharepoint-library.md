---
title: Agregar el elemento Web Visor de informes a una página Web (Reporting Services en modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 566ae0a91dd36d71ab6690e8910f1dd1cfe50043
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306381"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page-reporting-services-in-sharepoint-integrated-mode"></a>Agregar el elemento web Visor de informes a una página web (Reporting Services en el modo integrado de SharePoint)
  Puede usar el elemento web Visor de informes para ver informes que se ejecutan en un servidor de informes configurado para ejecutarse en el modo integrado con SharePoint. Puede usar el elemento web para mostrar archivos de definición de informe (.rdl) que haya creado en el Generador de informes o el Diseñador de informes y cargado en una biblioteca.  
  
 Puede agregar el elemento web Visor de informes a una página web si desea incrustar el informe en la página.  
  
> [!NOTE]  
>  Aunque tienen nombres idénticos, el elemento web Visor de informes instalado con el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] difiere del incluido en el archivo RSWebParts.cab. Las instrucciones de este tema son específicas para el elemento web Visor de informes que se instala con el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para agregar un elemento web a una página web, debe tener el permiso Agregar y personalizar páginas en el nivel de sitio. Si va a usar la configuración de seguridad predeterminada, este permiso se concede a los miembros del grupo **Propietarios** que tienen el nivel de permiso Control total.  
  
### <a name="to-embed-a-report-in-a-web-page"></a>Para incrustar un informe en una página web  
  
1.  Abra o cree un panel o una página de elementos web.  
  
2.  En el menú **Acciones del sitio**, haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar elemento web**.  
  
4.  En la lista de categorías de elementos web, seleccione la categoría **Varios** y, a continuación, seleccione **Visor de informes de SQL Server Reporting Services**.  
  
5.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona. Puede arrastrarlo a otra ubicación en la zona.  
  
6.  Dentro del visor, haga clic en **Haga clic aquí para abrir el panel de herramientas**.  
  
7.  Para seleccionar un informe desde cualquier biblioteca de la colección de sitios actual, haga clic en el botón Examinar (**...**). Además, puede escribir la dirección URL del informe. Para determinar la dirección URL de cualquier informe, haga clic con el botón derecho en el informe y seleccione **Propiedades**. No haga clic en la flecha hacia abajo junto al informe; la dirección URL del informe no se indica en la página Ver propiedades del elemento. Si copia y pega la dirección URL del cuadro de diálogo **Propiedades** , reemplace la codificación "%20" de la dirección URL por un espacio (por ejemplo, "Company%20Sales" debe ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada elemento web Visor de informes contiene un solo informe. La dirección URL debe ser una ruta de acceso completa a un informe que esté en el sitio de SharePoint actual o en un sitio dentro de la misma aplicación o granja de servidores web. La dirección URL debe resolverse como una biblioteca de documentos o una carpeta dentro de una biblioteca de documentos que contenga el informe. La dirección URL del informe debe incluir la extensión de archivo .rdl. Si el informe depende de un modelo o de archivos de orígenes de datos compartidos, no necesita especificar esos archivos en la dirección URL. El informe contiene referencias a los archivos que necesita.  
  
8.  Cuando el panel de herramientas está abierto, puede establecer propiedades para modificar la apariencia y el diseño predeterminados.  
  
9. Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
## <a name="see-also"></a>Vea también  
 [Elemento web Visor de informes en un sitio de SharePoint](../report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar el elemento web Visor de informes](../customize-the-report-viewer-web-part.md)   
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](../security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  

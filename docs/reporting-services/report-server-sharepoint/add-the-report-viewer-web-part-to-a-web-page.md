---
title: Agregar el elemento web Visor de informes a una página web | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d9eb107d1355a15d15c22fc3b24824cae009075
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Agregar el elemento web Visor de informes a una página web

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Puede usar el elemento web Visor de informes para ver informes que se ejecutan en un servidor de informes configurado para ejecutarse en el modo integrado de SharePoint. Puede usar el elemento web para mostrar archivos de definición de informe (.rdl) que haya creado en el Generador de informes o el Diseñador de informes y cargado en una biblioteca.

Puede agregar el elemento web Visor de informes a una página web si quiere incrustar un informe en esa página.

> [!NOTE]
> Este artículo es específico del elemento web Visor de informes incluido en el complemento Reporting Services para productos de SharePoint. La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

Para agregar un elemento web a una página web, debe tener el permiso Agregar y personalizar páginas en el nivel de sitio. Si va a usar la configuración de seguridad predeterminada, este permiso se concede a los miembros del grupo **Propietarios** que tienen el nivel de permiso Control total.

## <a name="to-embed-a-report-in-a-web-page"></a>Para incrustar un informe en una página web

1.  Abra o cree el panel o la página de elementos web.  
  
2.  En el menú **Acciones del sitio**, haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar elemento web**.  
  
4.  En la lista de categorías de elementos web, seleccione la categoría **Varios** y, a continuación, seleccione **Visor de informes de SQL Server Reporting Services**.  
  
5.  Haga clic en **Agregar**. El elemento web se agrega a la parte superior de la zona. Puede arrastrarlo a otra ubicación en la zona.  
  
6.  Dentro del visor, haga clic en **Haga clic aquí para abrir el panel de herramientas**.  
  
7.  Para seleccionar un informe desde cualquier biblioteca de la colección de sitios actual, haga clic en el botón Examinar (**...**). Además, puede escribir la dirección URL del informe. Para determinar la dirección URL de cualquier informe, haga clic con el botón derecho en el informe y seleccione **Propiedades**. No haga clic en la flecha hacia abajo junto al informe; la dirección URL del informe no se indica en la página Ver propiedades del elemento. Si copia y pega la dirección URL del cuadro de diálogo **Propiedades** , reemplace la codificación "%20" de la dirección URL por un espacio (por ejemplo, "Company%20Sales" debe ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada elemento web Visor de informes contiene un solo informe. La dirección URL debe ser una ruta de acceso completa a un informe que esté en el sitio de SharePoint actual o en un sitio dentro de la misma aplicación o granja de servidores web. La dirección URL debe resolverse como una biblioteca de documentos o una carpeta dentro de una biblioteca de documentos que contenga el informe. La dirección URL del informe debe incluir la extensión de archivo .rdl. Si el informe depende de un modelo o de archivos de orígenes de datos compartidos, no necesita especificar esos archivos en la dirección URL. El informe contiene referencias a los archivos que necesita.  
  
8.  Cuando el panel de herramientas está abierto, puede establecer propiedades para modificar la apariencia y el diseño predeterminados.  
  
9. Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
## <a name="see-also"></a>Vea también

 [Elemento web Visor de informes en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar el elemento web Visor de informes](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

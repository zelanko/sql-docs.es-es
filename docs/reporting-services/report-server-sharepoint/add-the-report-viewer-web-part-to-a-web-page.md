---
title: "Agregar el elemento web Visor de informes a una página web | Documentos de Microsoft"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 26080938c9849d6021f30d970ab2262f405df00c
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Agregar el elemento web Visor de informes a una página web

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Puede usar el elemento web Visor de informes para ver los informes que ejecutan servidor de informes que está configurado para ejecutarse en SharePoint el modo integrado. Puede usar el elemento web para mostrar los archivos de definición (.rdl) de informe que ha creado en el generador de informes o el Diseñador de informes y cargado en una biblioteca.

Puede agregar el elemento web Visor de informes a una página web si desea incrustar un informe en la página.

> [!NOTE]
> Este artículo es específico para el elemento web Visor de informes que se incluye con el complemento de Reporting Services para productos de SharePoint. Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

Para agregar un elemento web a una página web, debe tener el permiso Agregar y personalizar páginas en el nivel de sitio. Si va a usar la configuración de seguridad predeterminada, este permiso se concede a los miembros del grupo **Propietarios** que tienen el nivel de permiso Control total.

## <a name="to-embed-a-report-in-a-web-page"></a>Para incrustar un informe en una página web

1.  Abra o cree un panel o página de elementos web.  
  
2.  En el menú **Acciones del sitio**, haga clic en **Editar página**.  
  
3.  Haga clic en **agregar un elemento web**.  
  
4.  En la lista de categorías de elementos web, seleccione la categoría **Varios** y, a continuación, seleccione **Visor de informes de SQL Server Reporting Services**.  
  
5.  Haga clic en **Agregar**. El elemento web se agrega en la parte superior de la zona. Puede arrastrarlo a otra ubicación en la zona.  
  
6.  Dentro del visor, haga clic en **Haga clic aquí para abrir el panel de herramientas**.  
  
7.  Para seleccionar un informe desde cualquier biblioteca de la colección de sitios actual, haga clic en el botón Examinar (**...**). Además, puede escribir la dirección URL del informe. Para determinar la dirección URL de cualquier informe, haga clic con el botón derecho en el informe y seleccione **Propiedades**. No haga clic en la flecha hacia abajo junto al informe; la dirección URL del informe no se indica en la página Ver propiedades del elemento. Si copia y pega la dirección URL del cuadro de diálogo **Propiedades** , reemplace la codificación "%20" de la dirección URL por un espacio (por ejemplo, "Company%20Sales" debe ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada elemento web Visor de informes contiene un único informe. La dirección URL debe ser una ruta de acceso completa a un informe que esté en el sitio de SharePoint actual o en un sitio dentro de la misma aplicación o granja de servidores web. La dirección URL debe resolverse como una biblioteca de documentos o una carpeta dentro de una biblioteca de documentos que contenga el informe. La dirección URL del informe debe incluir la extensión de archivo .rdl. Si el informe depende de un modelo o de archivos de orígenes de datos compartidos, no necesita especificar esos archivos en la dirección URL. El informe contiene referencias a los archivos que necesita.  
  
8.  Cuando el panel de herramientas está abierto, puede establecer propiedades para modificar la apariencia y el diseño predeterminados.  
  
9. Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
## <a name="see-also"></a>Vea también

 [Elemento web Visor de informes en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar el elemento web Visor de informes](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

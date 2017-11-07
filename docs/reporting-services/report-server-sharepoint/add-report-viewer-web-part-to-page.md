---
title: "Agregar elemento web de Visor de informes de SQL Server Reporting Services a una página de SharePoint | Documentos de Microsoft"
ms.custom: Display a report, from SQL Server Reporting Services or Power BI Report Server, by adding a Report Viewer web part to a SharePoint page.
ms.date: 09/26/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: fbc68b6ff9f1edf5cf6ee13f6e93a3d2d1a8f834
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---

# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>Agregar elemento web de Visor de informes de SQL Server Reporting Services a una página de SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Mostrar un informe de SQL Server Reporting Services o el servidor de informes de Power BI, mediante la adición de un elemento web Visor de informes a una página de SharePoint.

![Elemento web Visor de informes en una página de SharePoint](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>Requisitos previos

* Para que los informes cargar correctamente, las notificaciones del servicio de Token de Windows (C2WTS) debe estar configurada para Kerberos delegación restringida. Para obtener más información sobre cómo configurar C2WTS, vea [notificaciones del servicio de Token de Windows (C2WTS) y Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md).

* El elemento web Visor de informes se debe implementar en la granja de servidores de SharePoint. Para obtener información sobre cómo implementar el proyecto de solución de elementos de web de Visor de informes, consulte [implementar el elemento web Visor de informes en un sitio de SharePoint](deploy-report-viewer-web-part.md).

* Para agregar un elemento web a una página web, debe tener el permiso Agregar y personalizar páginas en el nivel de sitio. Si va a usar la configuración de seguridad predeterminada, este permiso se concede a los miembros del grupo **Propietarios** que tienen el nivel de permiso Control total.

## <a name="add-web-part"></a>Agregar elemento web

1. En el sitio de SharePoint, seleccione la **engranaje** icono en la parte superior izquierda y seleccione **agregar una página**.

    ![Agregar una página a un sitio de sharepoint desde el icono de engranaje.](media/sharepoint-add-a-page.png)

2. Asigne un nombre y seleccione a la página **crear**.

3. En el Diseñador de la página, seleccione la **insertar** ficha en la cinta de opciones. A continuación, seleccione **elemento web** dentro de la **elementos** sección.

    ![Insertar un elemento web de la cinta de opciones de office.](media/sharepoint-insert-web-part.png)

4. En **categorías**, seleccione **SQL Server Reporting Services (modo nativo). En **elementos**, seleccione **Visor de informes**. A continuación, seleccione **agregar**.

    ![Agregar elemento web Visor de informes.](media/sharepoint-report-viewer-web-part.png)

    Inicialmente, esto puede aparecer un error. El error es porque la URL del servidor de informes de forma predeterminada está establecida en *http://localhost* y puede no estar disponible en esa ubicación.

## <a name="configure-the-report-viewer-web-part"></a>Configurar el elemento web Visor de informes

Para configurar el elemento web para que señale a un informe específico, haga lo siguiente.

1. Al editar la página de SharePoint, seleccione la flecha hacia abajo en la esquina superior derecha del elemento web y seleccione **Editar elemento web**.

    ![Modificar una página web de web parte desplegable.](media/sharepoint-edit-web-part.png)

2. Escriba el **dirección URL del servidor de informes** para el servidor de informes que hospeda el informe. Esto debe ser similar a *http://myrsserver/reportserver*.

3. Escriba la ruta de acceso y el nombre del informe que desea mostrar en el elemento web. Esto tendrá un aspecto similar a *AdventureWorks Sample Reports/Company Sales*. En este ejemplo, el informe *Company Sales* está en una carpeta denominada *AdventureWorks Sample Reports*.

4. Si el informe requiere parámetros, una vez que ha proporcionado la URL del servidor de informes y el nombre del informe, seleccione **cargar parámetros** dentro de la **parámetros** sección.

5. Seleccione **Aceptar** para guardar los cambios en la configuración del elemento web.

6. Seleccione **guardar**, dentro de la cinta de opciones de Office, para guardar los cambios en la página de SharePoint.

![Elemento web Visor de informes en una página de SharePoint](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>Consideraciones y limitaciones

* No se puede usar el elemento web Visor de informes en páginas modernas dentro de SharePoint.
* Informes de Power BI no se puede usar con el elemento web Visor de informes.
* Si no ve el elemento web Visor de informes, agregar a la página, asegúrese de que tiene [implementa el elemento web Visor de informes](deploy-report-viewer-web-part.md).

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).


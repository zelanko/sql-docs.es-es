---
title: Ver informes de Reporting Services en dispositivos de Microsoft Surface y Apple iOS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a3937f227d025da054a28f73fffde4a57dc365c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098662"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>Ver informes de Reporting Services en dispositivos de Microsoft Surface y de Apple iOS
  En este artículo se describen las características y los flujos de trabajo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admitidos para dispositivos de Microsoft Surface, y para dispositivos con Apple iOS 6 y Apple Safari como el iPad.  
  
## <a name="view-and-interact-with-reports"></a>Ver e interactuar con informes  
 A partir de [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite la visualización e interactividad básica con informes en dispositivos de Microsoft Surface, y en dispositivos con Apple iOS 6 y con el explorador Apple Safari como el iPad. También puede publicar informes mediante dispositivos de Microsoft Surface.  
  
 ![Escritorio del IPad](media/videothumbnail.jpg "escritorio del IPad")  
Vea una demostración de cómo ver informes en un iPad.  
  
 También puede ver informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en un dispositivo de Windows Phone 8.  
  
 Para usar las características descritas en este tema, instale uno de los elementos siguientes:  
  
-   Si se trata de un servidor de informes en modo nativo, instale [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] o posterior.  
  
     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] está disponible para su descarga desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=35575).  
  
-   Si es un servidor de informes en modo de SharePoint, instale la versión [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] o posterior del complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para productos de SharePoint.  
  
 **Para ver e interactuar con un informe en un dispositivo iPad o dispositivo Microsoft Surface**  
  
1.  Asegúrese de que puede conectarse al servidor de informes o al sitio de SharePoint donde reside el informe.  
  
2.  Abra el informe realizando una de las acciones siguientes.  
  
    -   **Iniciar desde correo electrónico:** Desde un correo electrónico creado por un [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suscripción, puntee en la dirección URL del informe. El informe se abrirá en el explorador.  
  
    -   **Iniciar desde el servidor de informes:** Busque el directorio en el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] servidor de informes y, a continuación, puntee en el nombre del informe para abrir el informe.  
  
    -   **Iniciar desde una biblioteca de documentos de SharePoint:** Vaya a una biblioteca de documentos de SharePoint que contiene [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes y, a continuación, puntee en el nombre del informe. Puede ver e interactuar con el informe.  
  
        > [!IMPORTANT]  
        >  Para el iPad, asegúrese de que la propiedad **Exploración privada** de Safari esté desactivada.  
  
    -   **Elemento web de SharePoint:** Si se ha agregado el elemento web a una página de SharePoint, puede ver [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes.  
  
3.  También puede abrir el informe en el dispositivo de Microsoft Surface utilizando el Administrador de informes. Busque el directorio en el Administrador de informes [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y, a continuación, puntee en el nombre del informe para abrirlo.  
  
    > [!IMPORTANT]  
    >  No se admite ver informes del Administrador de informes en un iPad.  
  
4.  Desplácese y haga zoom haciendo lo siguiente.  
  
    -   Para desplazar el informe, arrastre el dedo por la pantalla (hacia arriba, hacia abajo, a la izquierda o a la derecha). Este es el gesto de deslizar rápidamente.  
  
    -   Para acercar, coloque dos dedos sobre la pantalla y sepárelos. Para alejar, coloque dos dedos sobre la pantalla y acérquelos. Este es el gesto de alejar.  
  
5.  Navegue e interactúe con el informe haciendo lo siguiente.  
  
    -   Contraiga y expanda elementos de informe, y filas y columnas asociadas a grupos, punteando en el signo más (+) para contraer y en el signo menos (-) para expandir.  
  
    -   Alterne entre orden ascendente y descendente para las filas de una tabla o para las filas y columnas de una matriz punteando en el botón de ordenación. El botón de ordenación se encuentra normalmente en el encabezado de columna.  
  
    -   Expanda y contraiga el panel de parámetros punteando en el botón de flecha situado cerca de la parte superior del informe.  
  
    -   Seleccione un valor de parámetro punteando en el cuadro o el control situado junto al parámetro. Puntee en **Ver informe** para aplicar el valor del parámetro al informe.  
  
    -   Busque en el contenido del informe punteando en el cuadro situado junto a **Buscar**, escribiendo un término de búsqueda y, a continuación, punteando en **Buscar**.  
  
    -   Navegue por las páginas del informe punteando en los botones de navegación o punteando en el cuadro de texto situado junto a los botones y escribiendo el número de página.  
  
    -   Navegue a direcciones URL punteando en los hipervínculos que se han agregado a elementos de informe como cuadros de texto, imágenes, gráficos y medidores.  
  
    -   Exporte el informe punteando en el icono del **menú desplegable Exportar** y punteando después en un formato de archivo.  
  
        -   Si está viendo el informe en un dispositivo Microsoft Surface, puede exportar el informe a uno de los siguientes formatos.  
  
            -   Archivo XML con datos de informe  
  
            -   CSV (delimitado por comas)  
  
            -   PDF  
  
            -   MHTML (archivo web)  
  
            -   Excel  
  
            -   TIFF  
  
            -   Word  
  
        -   Si está viendo el informe en un iPad, puede exportar el informe como un archivo TIFF o PDF.  
  
## <a name="authentication"></a>Autenticación  
 La autenticación RSWindowsNTLM y la autenticación RSWindowsBasic funcionan con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo nativo y el iPad.  
  
 En general, se recomienda no utilizar RSWindowsBasic en entornos sin conexión https, porque este tipo de autenticación no proporciona confidencialidad para las credenciales transmitidas.  
  
 Para obtener más información sobre las autenticaciones RSWindowsNTLM y RSWindowsBasic, vea [Authentication with the Report Server](security/authentication-with-the-report-server.md).  
  
## <a name="uploading-reports"></a>Cargar informes  
 Puede publicar informes desde un dispositivo de Microsoft Surface mediante uno de los métodos siguientes si dispone de los permisos adecuados.  
  
> [!IMPORTANT]  
>  Estos métodos no se admiten en el iPad.  
  
-   Cargar un archivo de definición de informe (.rdl) en una biblioteca de documentos de SharePoint abriendo la biblioteca y punteando en **Cargar documento**.  
  
-   Cargar un archivo de definición de informe en la base de datos del servidor de informes abriendo el Administrador de informes y punteando en **Cargar archivo**.  
  
## <a name="additional-information"></a>Información adicional  
 Para obtener más información acerca de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y los exploradores admitidos, vea:  
  
-   [Planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
 Para obtener más información acerca de Microsoft Business Intelligence y los dispositivos móviles, vea lo siguiente:  
  
-   [Información general de dispositivos móviles y SharePoint 2013](https://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161351(v=office.15).aspx).  
  
-   [Admite los exploradores de dispositivos móviles en SharePoint 2013](https://technet.microsoft.com/library/fp161353\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161353(v=office.15).aspx).  
  
-   [Ver informes y cuadros de mandos en dispositivos iPad de Apple (SharePoint Server 2010)](https://technet.microsoft.com/library/hh697482.aspx) (https://technet.microsoft.com/library/hh697482.aspx).  
  
-   [Ver informes de Reporting Services en un iPad (vídeo)](https://technet.microsoft.com/sqlserver/jj873792.aspx) (https://technet.microsoft.com/sqlserver/jj873792.aspx).  
  
-   [Visualización de informes de Reporting Services en un dispositivo de RT de Microsoft Surface (vídeo)](https://technet.microsoft.com/sqlserver/dn146017)  
  
  

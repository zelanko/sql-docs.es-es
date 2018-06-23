---
title: Ver informes de Reporting Services en dispositivos de Microsoft Surface y Apple iOS | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2766644db67f3f677060c90a2addd2123276f1e0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200297"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>Ver informes de Reporting Services en dispositivos de Microsoft Surface y de Apple iOS
  En este artículo se describen las características y los flujos de trabajo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admitidos para dispositivos de Microsoft Surface, y para dispositivos con Apple iOS 6 y Apple Safari como el iPad.  
  
## <a name="view-and-interact-with-reports"></a>Ver e interactuar con informes  
 A partir de [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite la visualización e interactividad básica con informes en dispositivos de Microsoft Surface y con Apple iOS 6 y el explorador Apple Safari como el iPad. También puede publicar informes mediante dispositivos de Microsoft Surface.  
  
 ![Escritorio del IPad](media/videothumbnail.jpg "escritorio del IPad")  
Vea una demostración de cómo ver informes en un iPad.  
  
 También puede ver informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en un dispositivo de Windows Phone 8.  
  
 Para usar las características descritas en este tema, instale uno de los elementos siguientes:  
  
-   Si se trata de un servidor de informes en modo nativo, instale [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] o posterior.  
  
     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] está disponible para su descarga desde el [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35575).  
  
-   Para un servidor de informes de modo de SharePoint, instale [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] o una versión posterior de la [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint.  
  
 **Para ver e interactuar con un informe en un dispositivo iPad o un dispositivo Microsoft Surface**  
  
1.  Asegúrese de que puede conectarse al servidor de informes o al sitio de SharePoint donde reside el informe.  
  
2.  Abra el informe realizando una de las acciones siguientes.  
  
    -   **Iniciar desde correo electrónico:** desde un correo electrónico creado por un [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suscripción, puntee en la dirección URL del informe. El informe se abrirá en el explorador.  
  
    -   **Iniciar desde el servidor de informes:** busque el directorio en el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] servidor de informes y, a continuación, puntee en el nombre del informe para abrir el informe.  
  
    -   **Iniciar desde una biblioteca de documentos de SharePoint:** vaya a una biblioteca de documentos de SharePoint que contiene [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes y, a continuación, puntee en el nombre del informe. Puede ver e interactuar con el informe.  
  
        > [!IMPORTANT]  
        >  Para el iPad, asegúrese de que la propiedad **Exploración privada** de Safari esté desactivada.  
  
    -   **Elemento web de SharePoint:** si se ha agregado el elemento web a una página de SharePoint, puede ver [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes.  
  
3.  También puede abrir el informe en el dispositivo de Microsoft Surface utilizando el Administrador de informes. Busque el directorio en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Administrador de informes y, a continuación, puntee en el nombre del informe para abrir el informe.  
  
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
  
        -   Si está viendo el informe en un dispositivo de Microsoft Surface, puede exportar el informe a uno de los formatos siguientes.  
  
            -   Archivo XML con datos de informe  
  
            -   CSV (delimitado por comas)  
  
            -   PDF  
  
            -   MHTML (archivo web)  
  
            -   Excel  
  
            -   TIFF  
  
            -   Word  
  
        -   Si está viendo el informe en un iPad, puede exportar el informe como un archivo TIFF o PDF.  
  
## <a name="authentication"></a>Autenticación  
 Autenticación RSWindowsNTLM y la autenticación RSWindowsBasic funcionan con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo nativo y el iPad.  
  
 En general, se recomienda no utilizar RSWindowsBasic en entornos sin conexión https, porque este tipo de autenticación no proporciona confidencialidad para las credenciales transmitidas.  
  
 Para obtener más información acerca de la autenticación RSWindowsNTLM y RSWindowsBasic, vea [la autenticación con el servidor de informes](security/authentication-with-the-report-server.md).  
  
## <a name="uploading-reports"></a>Cargar informes  
 Puede publicar informes desde un dispositivo de Microsoft Surface mediante uno de los métodos siguientes si dispone de los permisos adecuados.  
  
> [!IMPORTANT]  
>  Estos métodos no se admiten en el iPad.  
  
-   Cargar un archivo de definición de informe (.rdl) en una biblioteca de documentos de SharePoint abriendo la biblioteca y punteando en **Cargar documento**.  
  
-   Cargar un archivo de definición de informe en la base de datos del servidor de informes abriendo el Administrador de informes y punteando en **Cargar archivo**.  
  
## <a name="additional-information"></a>Información adicional  
 Para obtener más información sobre [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y exploradores admitidos, vea:  
  
-   [Planeación de Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
 Para obtener más información acerca de Microsoft Business Intelligence y los dispositivos móviles, vea lo siguiente:  
  
-   [Información general de dispositivos móviles y SharePoint 2013](http://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) (http://technet.microsoft.com/library/fp161351(v=office.15).aspx).  
  
-   [Exploradores de dispositivos móviles admitidos en SharePoint 2013](http://technet.microsoft.com/library/fp161353\(v=office.15\).aspx) (http://technet.microsoft.com/library/fp161353(v=office.15).aspx).  
  
-   [Ver informes y cuadros de mandos en dispositivos iPad de Apple (SharePoint Server 2010)](http://technet.microsoft.com/library/hh697482.aspx) (http://technet.microsoft.com/library/hh697482.aspx).  
  
-   [Ver informes de Reporting Services en un iPad (vídeo)](http://technet.microsoft.com/sqlserver/jj873792.aspx) (http://technet.microsoft.com/sqlserver/jj873792.aspx).  
  
-   [Ver informes de Reporting Services en un dispositivo de RT de Microsoft Surface (vídeo)](http://technet.microsoft.com/sqlserver/dn146017)  
  
  
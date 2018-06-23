---
title: Implementar una extensión de representación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
caps.latest.revision: 43
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1cd6fb05217c0bde25dcc00e5f520dfd126385ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197899"
---
# <a name="deploying-a-rendering-extension"></a>Implementar una extensión de representación
  Después de haber escrito y compilado la extensión de representación de informes de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en una biblioteca de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], es necesario hacer que el servidor de informes y el Diseñador de informes la puedan reconocer. Para ello, copie la extensión en el directorio adecuado y agregue las entradas a los archivos de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adecuados.  
  
## <a name="configuration-file-rendering-extension-element"></a>Elemento Extension de representación de archivos de configuración  
 Una vez compilada una extensión de representación en una .DLL, agregue una entrada al archivo rsreportserver.config. De forma predeterminada, la ubicación es %Archivos de programa%\Microsoft SQL Server\MSRS10_50.\<nombreDeInstancia>\Reporting Services\ReportServer. El elemento primario es \<Render>. Bajo el elemento Render hay un elemento Extension para cada extensión de representación. El `Extension` elemento contiene dos atributos, Name y Type.  
  
 En la tabla siguiente se describe los atributos para el `Extension` (elemento) para las extensiones de representación:  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|**Nombre**|Nombre único de la extensión. La longitud máxima para el atributo **Name** es de 255 caracteres. El nombre debe ser único entre todas las entradas dentro del elemento **Extensions** del archivo de configuración. Si hay un nombre duplicado, el servidor de informes devuelve un error.|  
|**Tipo**|Lista separada por comas que incluye el espacio de nombres completo junto con el nombre del ensamblado.|  
|**Visible**|El valor `false` indica que la extensión de representación no debería estar visible en las interfaces de usuario. Si el atributo no está incluido, el valor predeterminado es `true`.|  
|**LogAllExecutionRequests**|Un valor `false` indica que una entrada solo se registra para la primera ejecución de un informe en una sesión. Si el atributo no está incluido, el valor predeterminado es `true`.<br /><br /> Por ejemplo, este valor de configuración determina si se ha de registrar una entrada solo para la primera página representada en un informe (en el caso de `false`) o una entrada para cada página representada en el informe (en el caso de `true`).|  
  
 Para más información, consulte [RSReportServer Configuration File](../../report-server/rsreportserver-config-configuration-file.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implementar la extensión para el servidor de informes  
 El servidor de informes utiliza las extensiones de representación para exportar los informes a otros formatos. Debería implementar su ensamblado de extensión de representación para el servidor de informes como un ensamblado privado. También tiene que realizar una entrada en el archivo de configuración del servidor de informes, rsreportserver.config.  
  
### <a name="to-deploy-the-assembly"></a>Para implementar el ensamblado  
  
1.  Copie el ensamblado de la ubicación provisional al directorio bin del servidor de informes en el que desea utilizar la extensión de representación. La ubicación predeterminada del directorio Bin del servidor de informes es %Archivos de programa%\Microsoft SQL Server\MSRS10_50.\<nombreDeInstancia>\Reporting Services\ReportServer\Bin.  
  
2.  Una vez copiado el archivo de ensamblado, abra el archivo rsreportserver.config. El archivo rsreportserver.config también se encuentra en el directorio bin del servidor de informes. Tiene que realizar una entrada en el archivo de configuración para el archivo de ensamblado de extensión. Puede abrir el archivo con [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o con un simple editor de texto.  
  
     Para más información, consulte [RSReportServer Configuration File](../../report-server/rsreportserver-config-configuration-file.md).  
  
3.  Busque el elemento **Render** en el archivo Rsreportserver.config. En la ubicación siguiente se debería realizar una extensión creada recientemente:  
  
    ```  
    <Extensions>  
       <Render>  
          <extension configuration>  
       </Render>  
    </Extensions>  
    ```  
  
4.  Agregue una entrada para la extensión de representación. La entrada debería incluir un elemento que tenga valores para **Name** y **Type**, y podría parecerse a la siguiente:  
  
    ```  
    <Extension Name="My Rendering Extension Name" Type="CompanyName.ExtensionName.MyRenderingProvider, AssemblyName" />  
    ```  
  
     El valor de **Name** es el nombre único de la extensión de representación. El valor de **Type** es una lista separada por comas que incluye una entrada para el espacio de nombres completo de la implementación de <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension>, seguida del nombre del ensamblado (sin incluir la extensión de archivo .dll). De forma predeterminada, las extensiones de representación están visibles. Para ocultar una extensión de las interfaces de usuario, por ejemplo, el Administrador de informes, agregue un **Visible** atribuir a la `Extension` elemento y establézcalo en `false`.  
  
## <a name="verifying-the-deployment"></a>Comprobación de la implementación  
 Puede abrir también el Administrador de informes y comprobar que la extensión está incluida en la lista de tipos de exportación disponibles para un informe.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de representación](implementing-a-rendering-extension.md)   
 [Información general de las extensiones de representación](rendering-extensions-overview.md)   
 [Implementar la interfaz IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Consideraciones de seguridad para las extensiones](../security-considerations-for-extensions.md)  
  
  
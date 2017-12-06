---
title: "Implementar una extensión de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b708125e0e6a15c22e7baee4ef4aba0f2c193624
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="deploying-a-delivery-extension"></a>Implementar una extensión de entrega
  Las extensiones de entrega proporcionan su información de configuración en forma de archivo de configuración XML. El archivo XML cumple el esquema XML definido para las extensiones de entrega. Las extensiones de entrega proporcionan la infraestructura para establecer y modificar el archivo de configuración.  
  
 Si una extensión de entrega se reemplaza o actualiza, todas las suscripciones que hacen referencia a la misma siguen siendo válidas.  
  
 Una vez escrita y compilada la extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en una biblioteca de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], debe copiar la extensión en el directorio adecuado y agregar una entrada al archivo de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] correcto de modo que el servidor de informes pueda localizarla.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extension de archivos de configuración  
 Las extensiones de entrega que se implementan en el servidor de informes tienen que especificarse como elementos **Extension** en el archivo de configuración. El archivo de configuración para el servidor de informes es RSReportServer.config.  
  
 En la tabla siguiente se describen los atributos del elemento **Extension** para las extensiones de entrega.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**Nombre**|Un nombre único para la extensión (por ejemplo, "Correo electrónico del servidor de informes", para la extensión de entrega por correo electrónico, o "Recurso compartido de archivos del servidor de informes", para la extensión de entrega en recursos compartidos de archivos). La longitud máxima para el atributo **Name** es de 255 caracteres. El nombre debe ser único entre todas las entradas en el elemento **Extension** del archivo de configuración. Si hay un nombre duplicado, el servidor de informes devuelve un error.|  
|**Tipo**|Lista separada por comas que incluye el espacio de nombres completo junto con el nombre del ensamblado.|  
|**Visible**|El valor **false** indica que la extensión de entrega no debe ser visible en las interfaces de usuario. Si el atributo no está incluido, el valor predeterminado es **true**.|  
  
 Para más información sobre el archivo RSReportServer.config, vea [Archivos de configuración de Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implementar la extensión para el servidor de informes  
 El servidor de informes utiliza las extensiones de entrega para procesar y entregar notificaciones o informes. Debería implementar el ensamblado de extensión de entrega para el servidor de informes como un ensamblado privado. También tiene que realizar una entrada en el archivo de configuración del servidor de informes, RSReportServer.config.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>Para implementar un ensamblado de extensión de entrega en un servidor de informes  
  
1.  Copie el ensamblado desde la ubicación provisional al directorio bin del servidor de informes en el que desea utilizar la extensión de entrega. La ubicación predeterminada del directorio Bin del servidor de informes es %Archivos de programa%\Microsoft SQL Server\MSRS13.\<nombreDeInstancia>\Reporting Services\ReportServer\bin.  
  
    > [!IMPORTANT]  
    >  Si está intentando sobrescribir un ensamblado de extensión de entrega existente, primero debe detener el servicio del servidor de informes antes de copiar el ensamblado actualizado. Reinicie el servicio después de que el ensamblado termine la copia.  
  
2.  Una vez copiado el archivo de ensamblado, abra el archivo RSReportServer.config. El archivo RSReportServer.config se encuentra en el directorio %Archivos de programa%\Microsoft SQL Server\MSRS13.\<nombreDeInstancia>\Reporting Services\ReportServer. Tiene que realizar una entrada en el archivo de configuración para el archivo de ensamblado de extensión de entrega. Puede abrir el archivo de configuración con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o con un simple editor de texto, como el Bloc de notas.  
  
3.  Busque el elemento **Delivery** en el archivo RSReportServer.config. En la ubicación siguiente se debería realizar una extensión de entrega creada recientemente:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Agregue una entrada para la extensión de entrega. La entrada debe incluir un elemento **Extension** con valores para **Name** y **Type**, y podría parecerse a la siguiente:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     El valor de **Name** es el nombre único de la extensión de entrega. El valor de **Type** es una lista separada por comas que incluye una entrada para el espacio de nombres completo de la clase que implementa la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>, seguida del nombre del ensamblado (sin incluir la extensión de archivo .dll). De forma predeterminada, las extensiones de entrega están visibles. Para ocultar una extensión de las interfaces de usuario, por ejemplo del portal web, agregue un atributo **Visible** al elemento **Extension** y establézcalo en **false**.  
  
5.  Por último, agregue un grupo de código para el ensamblado personalizado que conceda el permiso **FullTrust** a la extensión de entrega. Para ello, agregue el grupo de código al archivo rssrvpolicy.config que se encuentra, de forma predeterminada, en %Archivos de programa %\Microsoft SQL Server\MSRS13.\<nombreDeInstancia>\Reporting Services\ReportServer. El grupo de código podría tener la apariencia siguiente:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     La pertenencia de dirección URL es solo una de las muchas condiciones de pertenencia que podría elegir para la extensión de entrega. Para más información sobre la seguridad de acceso del código de [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], vea [Desarrollo seguro &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
   
## <a name="verifying-the-deployment"></a>Comprobación de la implementación  
 Puede comprobar si la extensión de entrega se implementó correctamente en el servidor de informes utilizando el método <xref:ReportService2010.ReportingService2010.ListExtensions%2A> del servicio web. También puede abrir el portal web y comprobar que la extensión está incluida en la lista de extensiones de entrega disponibles para una suscripción. Para más información sobre el portal web y las suscripciones, vea [Suscripciones y entrega &#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

---
title: "Implementar una extensión de entrega | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d072577828375a08c133bb1a68d93e652e5cf168
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="deploying-a-delivery-extension"></a>Implementar una extensión de entrega
  Las extensiones de entrega proporcionan su información de configuración en forma de archivo de configuración XML. El archivo XML cumple el esquema XML definido para las extensiones de entrega. Las extensiones de entrega proporcionan la infraestructura para establecer y modificar el archivo de configuración.  
  
 Si una extensión de entrega se reemplaza o actualiza, todas las suscripciones que hacen referencia a la misma siguen siendo válidas.  
  
 Después de haber escrito y compilado la [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de entrega en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] biblioteca, debe copiar la extensión en el directorio adecuado y agregar una entrada a la correspondiente [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] archivo de configuración para el servidor de informes puede encontrarlo.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extension de archivos de configuración  
 Las extensiones de entrega que se implementación en el servidor de informes tienen que escribirse como **extensión** elementos en el archivo de configuración. El archivo de configuración para el servidor de informes es RSReportServer.config.  
  
 En la tabla siguiente se describe los atributos para el **extensión** (elemento) para las extensiones de entrega.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**Nombre**|Un nombre único para la extensión (por ejemplo, "Correo electrónico del servidor de informes", para la extensión de entrega por correo electrónico, o "Recurso compartido de archivos del servidor de informes", para la extensión de entrega en recursos compartidos de archivos). La longitud máxima para el atributo **Name** es de 255 caracteres. El nombre debe ser único entre todas las entradas en el elemento **Extension** del archivo de configuración. Si hay un nombre duplicado, el servidor de informes devuelve un error.|  
|**Tipo**|Lista separada por comas que incluye el espacio de nombres completo junto con el nombre del ensamblado.|  
|**Visible**|Un valor de **false** indica que la extensión de entrega no debería estar visible en las interfaces de usuario. Si el atributo no está incluido, el valor predeterminado es **true**.|  
  
 Para obtener más información sobre el archivo RSReportServer.config, vea [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implementar la extensión para el servidor de informes  
 El servidor de informes utiliza las extensiones de entrega para procesar y entregar notificaciones o informes. Debería implementar el ensamblado de extensión de entrega para el servidor de informes como un ensamblado privado. También tiene que realizar una entrada en el archivo de configuración del servidor de informes, RSReportServer.config.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>Para implementar un ensamblado de extensión de entrega en un servidor de informes  
  
1.  Copie el ensamblado desde la ubicación provisional al directorio bin del servidor de informes en el que desea utilizar la extensión de entrega. La ubicación predeterminada del directorio de bin del servidor de informes es %ProgramFiles%\Microsoft SQL Server\MSRS13. \<NombreDeInstancia > \Reporting.  
  
    > [!IMPORTANT]  
    >  Si está intentando sobrescribir un ensamblado de extensión de entrega existente, primero debe detener el servicio del servidor de informes antes de copiar el ensamblado actualizado. Reinicie el servicio después de que el ensamblado termine la copia.  
  
2.  Una vez copiado el archivo de ensamblado, abra el archivo RSReportServer.config. El archivo RSReportServer.config se encuentra en el %ProgramFiles%\Microsoft SQL Server\MSRS13. \<NombreDeInstancia > \Reporting directorio. Tiene que realizar una entrada en el archivo de configuración para el archivo de ensamblado de extensión de entrega. Puede abrir el archivo de configuración con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o un editor de texto simple, como el Bloc de notas.  
  
3.  Busque la **entrega** elemento en el archivo RSReportServer.config. En la ubicación siguiente se debería realizar una extensión de entrega creada recientemente:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Agregue una entrada para la extensión de entrega. La entrada debería incluir una **extensión** elemento con los valores para **nombre** y **tipo**y podría ser similar al siguiente:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     El valor de **nombre** es el nombre único de la extensión de entrega. El valor de **tipo** es una lista separada por comas que incluye una entrada para el espacio de nombres completo de la clase que implementa el <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> interfaz, seguido del nombre del ensamblado (sin incluir la extensión de archivo .dll). De forma predeterminada, las extensiones de entrega están visibles. Para ocultar una extensión de interfaces de usuario, como el portal web, agregue un **Visible** atribuir a la **extensión** elemento y establézcalo en **false**.  
  
5.  Por último, agregue un grupo de código para el ensamblado personalizado que conceda **FullTrust** permiso para la extensión de entrega. Para ello, agregue el grupo de código al archivo rssrvpolicy.config que se encuentra en %ProgramFiles%\Microsoft SQL Server\MSRS13 de forma predeterminada. \<NombreDeInstancia > \Reporting. El grupo de código podría tener la apariencia siguiente:  
  
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
  
     La pertenencia de dirección URL es solo una de las muchas condiciones de pertenencia que podría elegir para la extensión de entrega. Para obtener más información acerca de la seguridad de acceso del código en [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], consulte.[ Proteger desarrollo &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>Comprobación de la implementación  
 Puede comprobar si la extensión de entrega se implementó correctamente en el servidor de informes utilizando el método <xref:ReportService2010.ReportingService2010.ListExtensions%2A> del servicio web. También puede abrir el portal web y compruebe que la extensión está incluida en la lista de extensiones de entrega disponibles para una suscripción. Para obtener más información sobre el portal web y las suscripciones, vea [suscripciones y entrega &#40; Reporting Services &#41; ](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  


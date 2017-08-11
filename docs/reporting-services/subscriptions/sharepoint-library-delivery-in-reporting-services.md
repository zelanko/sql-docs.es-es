---
title: Entrega de la biblioteca de SharePoint en Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 18312b5d8222cc79b07eb3a33eaf3fb60454b861
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Entrega de la biblioteca de SharePoint en Reporting Services
  Un servidor de informes que se configura para la integración de SharePoint incluye una extensión de entrega que usted puede utilizar para enviar un informe a una biblioteca de SharePoint.  
  
 Para usar la extensión de entrega de SharePoint, debe crear una suscripción a partir de una página de aplicación de un sitio de SharePoint y, a continuación, seleccionar **Biblioteca de documentos de SharePoint** como el tipo de entrega. No puede usar la extensión de entrega de SharePoint para suscripciones creadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o el Administrador de informes.  
  
> [!NOTE]  
>  La extensión de entrega no admite la entrega de informes a un sitio de SharePoint si el servidor de informes se ejecuta en modo nativo. Si intenta llamar a la extensión de entrega mediante programación para un servidor de informes en modo nativo, el servidor devuelve el error **rsDeliveryExtensionNotFound** y registra el error **rsOperationNotSupportedSharePointMode** en los archivos de registro del servidor de informes.  
  
## <a name="requirements"></a>Requisitos  
 Requisitos para entregar informes representados a una biblioteca:  
  
-   El servidor de informes debe estar configurado para el modo integrado de SharePoint.  
  
-   El servidor de informes debe tener la extensión de entrega de SharePoint instalada y configurada.  
  
-   El informe debe ser un archivo de definición de informe (.rdl). No puede entregar otros tipos de contenido del servidor de informes, como modelos o recursos, mediante una suscripción. No puede suscribirse a informes ad hoc que usen modelos como origen de datos.  
  
-   El informe debe usar credenciales almacenadas. Es un requisito previo para crear suscripciones en un informe con independencia del tipo de entrega.  
  
-   El destino debe ser una biblioteca de SharePoint. Al elegir una biblioteca de destino, debe elegir la que se encuentra en el mismo sitio de SharePoint. No puede entregar un informe a una biblioteca que se encuentre en otro servidor o en otro sitio dentro de la misma colección de sitios.  
  
 Las propiedades y los metadatos no forman parte de la entrega de informes. La primera vez que se entrega el informe, hereda la configuración de seguridad de la carpeta o la lista que lo contiene. Si modifica posteriormente la configuración de seguridad o establece propiedades de informe, se conserva dicha configuración. La suscripción tan solo actualiza el informe almacenado en la ubicación especificada.  
  
## <a name="sharepoint-permissions"></a>Permisos de SharePoint  
 Para crear una suscripción, debe tener el permiso Ver elementos en el informe. Para entregar el informe, debe tener el permiso Agregar elementos en la biblioteca a la que se entrega el informe.  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>Cómo crear, modificar y eliminar suscripciones  
  
1.  Vaya al sitio de SharePoint desde el que se obtiene acceso al informe.  
  
2.  Seleccione el informe, haga clic en la flecha hacia abajo junto al informe y seleccione **Administrar suscripciones**.  
  
3.  Haga clic en **Crear**, **Editar**o **Eliminar**.  
  
 Un mensaje de estado en la lista Administrar suscripciones muestra la información actual acerca de la suscripción, donde se especifica si se ha realizado correctamente, así como la fecha y hora de la última vez que se ejecutó la suscripción.  
  
## <a name="setting-delivery-options"></a>Establecer opciones de entrega  
 Puede establecer las siguientes opciones de entrega en una suscripción que entrega un informe a una biblioteca de SharePoint.  
  
 Formato de salida de representación  
 Especifique el formato de aplicación en que desea entregar el informe. El informe se representa en este formato antes de la entrega. El formato de salida seleccionado determina la extensión de archivo predeterminada.  
  
 La lista de formatos de salida en la que puede realizar la selección es el conjunto de extensiones de representación instaladas en el servidor de informes.  
  
 Tenga en cuenta que no puede especificar formatos de salida solo para uso interno o no admitidos para los servidores de informes que se ejecutan en el modo integrado de SharePoint. Estos formatos son Null, RGDI y HTMLOWC.  
  
 Nombre y extensión de archivo  
 Especifique el nombre y la extensión de archivo del informe como desea que aparezca en la biblioteca de destino. Si no especifica ninguna extensión de archivo, el servidor de informes crea una basada en el formato de salida del informe. Este valor es necesario. El nombre de archivo no debe incluir los siguientes caracteres: : \ / * ? " < > | # { } %  
  
 Title  
 Especifica una propiedad **Title** opcional para el informe en la biblioteca de destino. Es una propiedad estándar para todos los elementos almacenados en una biblioteca. Los usuarios pueden especificar si se va a mostrar u ocultar esta propiedad al ver el contenido de la biblioteca en un sitio de SharePoint.  
  
 Ruta de acceso  
 Especifica una dirección URL completa a la biblioteca de SharePoint, incluidos la aplicación web y el sitio de SharePoint. Por ejemplo: `http://mySharePointWeb/MySite/MyDocLib`; donde `http://mySharePointWeb` indica la aplicación Web, "Misitio" es el sitio de SharePoint y "Mibibliotecadedocumentos" es la biblioteca de SharePoint donde se entregará el informe.  
  
 No puede especificar una página, un sitio o una lista. El contenedor de destino debe ser una biblioteca en el mismo sitio o conjunto de servidores.  
  
 Opciones de sobrescritura  
 Especifica si un archivo con el mismo nombre y extensión se sustituye por una versión más reciente al procesarse la suscripción. Elija **Sobrescribir** si desea reemplazar un archivo existente por una versión nueva. Elija **Ninguno** si no desea que la suscripción reemplace el archivo. En este caso, no se realiza ninguna entrega si existe un archivo con el nombre y la extensión de destino. Elija **Incremento automático** si desea agregar versiones sucesivas del mismo archivo anexando un número al final del nombre de archivo.  
  
 Copia automática  
 Si va a usar la característica de copia automática para copiar automáticamente la versión más reciente de un archivo en varias ubicaciones, el archivo se copiará al habilitarse **Sobrescribir** . Si usa **Incremento automático** o **Ninguno**, la entrega no se realiza y se genera el error **rsDeliveryError** .  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar suscripciones para servidores de informes en modo de SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Las suscripciones y entrega &#40; Reporting Services &#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Especificar credenciales y la información de conexión para orígenes de datos de informe](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  


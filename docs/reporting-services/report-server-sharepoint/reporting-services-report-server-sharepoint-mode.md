---
title: Informe servidor de Reporting Services (modo de SharePoint) | Documentos de Microsoft
ms.custom: 
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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a8cd1bd00ec92535fff73c5eaa4ff9bbe9274ef2
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Servidor de informes de Reporting Services (modo de SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Un servidor de informes de Reporting Services configurado para **el modo de SharePoint** puede ejecutarse en una implementación de un producto de SharePoint. Un servidor de informes en el modo de SharePoint puede usar las características de colaboración y administración de SharePoint para los informes y otros tipos de contenido de [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] . Modo de SharePoint requiere instalar la versión adecuada del complemento de Reporting Services para productos de SharePoint en el SharePoint front-end Web.  
  
> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

 Para obtener información sobre la instalación y la configuración, vea lo siguiente:  
  
-   [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Agregar un servidor de informes adicional a una granja de servidores](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
## <a name="feature-summary"></a>Resumen de características

 Configurar un servidor de informes para que se ejecute en el modo integrado de SharePoint proporciona la siguiente funcionalidad adicional, que solo está disponible al implementar un servidor de informes en este modo:  
  
-   Uso de las características de administración de documentos y colaboración de SharePoint, incluidas las alertas. Un sitio de SharePoint proporciona un portal unificado para obtener acceso y administrar todos los elementos de informe en un único lugar.  
  
-   Uso de proveedores de autenticación y permisos de SharePoint para controlar el acceso a informes, modelos y otros elementos.  
  
-   Uso de topologías de implementación de SharePoint para distribuir informes a través de una conexión a Internet desde fuera del firewall. Un servidor de informes proporciona servicios de procesamiento de datos e informes en el contexto de una implementación de SharePoint de mayor tamaño configurada para el acceso a Internet.  
  
-   Administración de informes, modelos, orígenes de datos, programaciones e historial de informes en páginas de aplicación personalizadas en un sitio de SharePoint. Puede establecer propiedades, definir programaciones y suscripciones, y crear y administrar el historial de informes en un sitio de SharePoint del mismo modo que los crearía y administraría desde otras herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Publicación o carga de informes, modelos de informes, recursos y archivos de orígenes de datos compartidos en una biblioteca de SharePoint, incluido el Centro de informes de Office SharePoint Server.  
  
     Uso del Diseñador de informes, el Diseñador de modelos y el Generador de informes para crear informes y orígenes de datos que se van a publicar directamente en una biblioteca de SharePoint. También puede utilizar la acción Cargar de un sitio de SharePoint para agregar cualquier definición de informe y modelos de informe a una biblioteca de SharePoint.  
  
     Como el servidor de informes procesa las definiciones de informe de la misma forma, independientemente del modo de servidor que se utilice, los datos y el diseño de informe no se ven afectados por el modo de servidor. Cualquier informe que pueda ejecutarse en un servidor de informes en modo nativo podrá ejecutarse en un servidor de informes configurado para el modo integrado de SharePoint.  
  
-   Suscripción y entrega de informes a una biblioteca de SharePoint mediante el uso de una nueva extensión de entrega de SharePoint. También puede entregar informes a través de correo electrónico o en una carpeta compartida. Las extensiones de entrega del servidor de informes se utilizan para entregar informes. Puede crear suscripciones controladas por datos para la distribución de informes a gran escala utilizando datos del suscriptor consultados en tiempo de ejecución.  
  
-   Un elemento web Visor de informes puede agregar a las páginas de SharePoint para ver un informe dentro de una aplicación web de SharePoint. El elemento web incluye la navegación en páginas, buscar, imprimir y exportar funciones.  
  
-   Programación con un nuevo extremo SOAP para crear aplicaciones personalizadas que se integren con un sitio de SharePoint. También puede utilizar el proveedor de Instrumental de administración de Windows (WMI) actualizado para configurar mediante programación una instancia de servidor de informes que se ejecute en el modo integrado de SharePoint.  
  
-   Creación de informes de servicio de Microsoft Access en modo conectado.  
  
-   Zonas de AAM, implementaciones con conexión a Internet y tokens de usuario de SharePoint para listas de SharePoint.  
  
## <a name="connected-mode-and-local-mode"></a>Modo conectado y modo local

 La versión SQL Server 2008 R2 presentó un nuevo *modo local* para ver informes desde un servidor de SharePoint 2010 que tenga instalado el complemento Reporting Services de Microsoft SQL Server 2008 R2 o posterior para productos de SharePoint 2010.  
  
-   *Modo local*: modo Local permite que los informes se representen localmente desde la biblioteca de documentos de SharePoint, sin integración con un servidor de informes de Reporting Services. El complemento de Reporting Services para productos de SharePoint es necesario, pero no es un servidor de informes de Reporting Services. El complemento se puede instalar de varias formas diferentes, incluida la herramienta de preparación de productos de SharePoint 2010. Para obtener más información sobre el modo local, vea [modo Local frente a los informes en modo conectado en el Visor de informes](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) y [dónde encontrar el complemento de Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modo conectado*: modo conectado se obtiene integrando un servidor de informes de Reporting Services en la granja de SharePoint mediante Administración Central de SharePoint. La integración con un servidor de informes habilita la creación de informes completos; proporciona las características de colaboración de SharePoint 2010 y las características basadas en servidor de un servidor de informes: suscripciones, instantáneas y procesamiento basado en servidor.  
  
## <a name="unsupported-sharepoint-features"></a>Características de sharePoint no admitidas

 No todas las características de SharePoint se encuentran disponibles para las operaciones integradas. La siguiente es una lista de las características de SharePoint, que Reporting Services no se integra directamente:  
  
-   Servicio de almacenamiento seguro.  
  
-   No puede utilizar la integración del Calendario de Outlook de SharePoint ni la programación de SharePoint para los archivos de servicios de informes en una biblioteca de documentos.  
  
-   Catálogo de datos profesionales de SharePoint.  
  
-   Personalización de SharePoint no se admite también en las páginas de Reporting Services. La integración del servidor de informes no se admite si la aplicación web de SharePoint está habilitada para el acceso anónimo.  
  
-   SQL Server Reporting Services **no** admite el control de versiones de la biblioteca de documentos de SharePoint. Si guarda los elementos de informe en una biblioteca de documentos configurada con el “Historial de versiones del documento” habilitado, las características de Reporting Services no funcionarán correctamente y generarán errores en el registro de ULS. A continuación se presenta un ejemplo de un error en el registro de ULS:  
  
    -   “…Se ha deshabilitado un origen de datos asociado al informe”.  
  
     El historial de versiones de la biblioteca de documentos se configura en la página “Configuración de versiones” de “Configuración de biblioteca”.  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>Combinaciones admitidas del servidor de SharePoint y el complemento informes

 No todas las características se admiten en todas las combinaciones de servidor de informes, complemento de Reporting Services para SharePoint y productos de SharePoint. Para obtener más información, vea [combinaciones admitidas de SharePoint y servidor de Reporting Services y complemento](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  Se debe utilizar la versión correcta del complemento Reporting Services con la versión correspondiente de Productos de SharePoint.  
  
## <a name="components-that-provide-integration"></a>Componentes que proporcionan integración

 Para combinar los servidores en una sola implementación, integrar una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services con una instancia de productos de SharePoint  
  
 Integración se proporciona a través de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el complemento de Reporting Services para productos de SharePoint. El complemento de Reporting Services es un componente de distribución gratuita que puede descargar e instalar a continuación, en un servidor que ejecuta la versión adecuada de SharePoint.  
  
> [!TIP]  
>  No todas las características se admiten en todas las combinaciones de servidor de informes, complemento de Reporting Services para SharePoint y productos de SharePoint. Para obtener más información, vea [combinaciones admitidas de SharePoint y servidor de Reporting Services y complemento](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   En SharePoint, el complemento de Reporting Services proporciona el punto de conexión de proxy ReportServer, un elemento web Visor de informes y páginas de aplicación para que se puede ver, almacenar y administrar el contenido de servidor de informes en un sitio de SharePoint o una granja de servidores.  
  
-   En Reporting Services proporciona archivos de programa actualizados, un extremo SOAP y las extensiones personalizadas de seguridad y la entrega. El servidor de informes debe configurarse para que se ejecute en el modo integrado de SharePoint, dedicado en exclusiva a admitir el acceso a informes y la entrega a través del sitio de SharePoint.  
  
 Después de instalar el complemento de Reporting Services en SharePoint y configurados los dos servidores para la integración, puede cargar o publicar los tipos de contenido de servidor de informes en una biblioteca de SharePoint y, a continuación, ver y administrar esos documentos desde un sitio de SharePoint. Cargar o publicar el contenido del servidor de informes es un primer paso importante; el elemento web y las páginas están disponibles al seleccionar las definiciones de informe (.rdl), modelos de informe (.smdl) y compartido (.rsds) de orígenes de datos en un sitio de SharePoint.  
  
##  <a name="language-considerations"></a>Consideraciones de idioma

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] y [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] están disponibles en muchos más idiomas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Cuando configure un servidor de informes para que se ejecute en una implementación de un producto de SharePoint, es probable que vea una combinación de idiomas. La interfaz de usuario, la documentación y los mensajes se mostrarán en los siguientes idiomas:  
  
-   Todas las páginas de aplicación, herramientas, errores, advertencias y mensajes que se originan en Reporting Services aparecerá en el idioma usado por la instancia de Reporting Services en uno de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] idiomas.  
  
-   Páginas de aplicación que se abren en un sitio de SharePoint, el elemento web Visor de informes y el generador de informes aparecerán en uno de los idiomas admitidos para el complemento de Reporting Services. Para ver la lista de los idiomas admitidos, vaya a [descargas de SQL Server](http://msdn.microsoft.com/sql/downloads/) y busque la página de descarga para el SQL Server 2016 Reporting Services Add-de.  
  
-   Los sitios de SharePoint, la Administración central de SharePoint, la Ayuda en pantalla y los mensajes están disponibles en los idiomas compatibles con los productos Office Server.  
  
 Si el idioma de su producto de SharePoint o la tecnología es diferente del idioma del servidor de informes, Reporting Services intentará utilizar el idioma de la misma familia de idiomas que proporciona a la coincidencia más cercana. Si no hay ningún idioma sustituto que se aproxime, el servidor de informes utilizará el inglés.  
  
## <a name="related-tasks"></a>Tareas relacionadas

 En la tabla siguiente se resume las tareas relacionadas con un servidor de informes de modo de SharePoint de Reporting Services:  
  
|**Tarea**|**Vínculo**|  
|--------------|--------------|  
|Pasos detallados para instalar y configurar Reporting Services en modo de SharePoint.|[Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c) y [agregar un servidor de informes adicional a una granja de servidores](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Escalado horizontal la implementación de SharePoint de Reporting Services mediante la adición de servidores de informes adicionales.|[Agregar un servidor de informes adicional a una granja de servidores](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) y [topologías de implementación para las características de BI de SQL Server en SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).|  
|Agregar adicionales SharePoint front-end web que tienen los componentes de Reporting Services instalados para ver e imprimir elementos.|[Agregar un front-end de web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configurar el correo electrónico para el servidor de informes en SharePoint.|[Configurar el correo electrónico para una aplicación de servicio de Reporting Services](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|Información reciente sobre esta versión, incluida en TechNet Wiki.|[SQL Server 2012 Reporting Services consejos, trucos y solución de problemas de](http://go.microsoft.com/fwlink/?LinkId=221297).|  

## <a name="next-steps"></a>Pasos siguientes

[Instalar o desinstalar Reporting Services en sdd para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[Notificar el elemento web Visor de en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[Cuestionario: Configurar SSRS 2012 para la integración de SharePoint](http://go.microsoft.com/fwlink/?LinkId=306443)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).


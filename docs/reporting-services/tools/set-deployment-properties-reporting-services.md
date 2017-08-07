---
title: "Establecer propiedades de implementación (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], deploying
- publishing reports [Reporting Services]
- properties [Reporting Services], deployment
- deploying reports [Reporting Services]
ms.assetid: 18201ca0-bf4a-484f-b3a2-95d1046a6a9b
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 30d542287f81032aa1bc2540d461a8f8c163b2f9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="set-deployment-properties-reporting-services"></a>Establecer propiedades de implementación (Reporting Services)
  En[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], debe especificar el servidor de informes y, si lo desea, las carpetas de los informes y orígenes de datos compartidos para poder publicar los elementos de un proyecto de Servidor de informes en un servidor de informes. Las propiedades y valores que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] necesita para generar los informes, obtener una vista previa de los mismos e implementarlos están almacenados en las configuraciones de proyecto correspondiente al proyecto del servidor de informes. Puede crear varios conjuntos con nombre para estas propiedades de proyecto; de esta forma, podrá cambiar de un conjunto de propiedades a otro según sea necesario. Cada conjunto de propiedades es una configuración. Por ejemplo, puede tener una configuración para publicar los informes en un servidor de pruebas y otra configuración diferente para publicar los informes en un servidor de producción.  
  
 Use el Administrador de configuración para crear y administrar conjuntos de propiedades de proyecto en las configuraciones de proyecto. El Administrador de configuración es una característica admitida en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], en el que está basado [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] .  
  
> [!NOTE]  
>  No confunda esta característica con el Administrador de configuración de Reporting Services, que se usa para configurar Reporting Services después de la instalación. Para obtener más información, vea [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md).  
  
> [!NOTE]  
>  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], la acción de publicar informes desde un proyecto o una solución de servidor de informes se denomina *implementación de informes*.  
  
### <a name="to-set-deployment-properties"></a>Establecer las propiedades de implementación  
  
1.  Haga clic con el botón derecho en el proyecto de informe y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Páginas de propiedades** del proyecto, en la lista **Configuración** , seleccione la configuración que desea modificar. Las configuraciones habituales son **DebugLocal**, **Debug**y **Release**.  
  
    > [!NOTE]  
    >  Puede utilizar varias configuraciones para cambiar rápidamente entre diferentes servidores de informes y opciones.  
  
3.  En el cuadro de texto **OutputPath**  , escriba o pegue la ruta de acceso en el sistema de archivos local para almacenar la definición de informe que se usa en la comprobación de la compilación, la implementación y la vista previa de informes. La ruta de acceso debe ser diferente de la que se utiliza para el proyecto y una ruta de acceso relativa que sea una carpeta secundaria bajo la ruta de acceso del proyecto.  
  
4.  En el cuadro de texto **ErrorLevel**  , escriba la gravedad de los problemas de compilación que se notifican como errores. Los problemas que se producen al compilar informes, orígenes de datos u otros recursos de proyecto con un nivel de gravedad menor o igual que el valor de **ErrorLevel**  se notifican como errores; los demás se notifican como advertencias. Cualquier error hará que la tarea de compilación dé un error. Los niveles de gravedad válidos abarcan de 0 a 4, ambos incluidos. El valor predeterminado es 2.  
  
     **ErrorLevel** se puede utilizar para aumentar o disminuir la sensibilidad de la compilación. Por ejemplo, cuando se crea un informe con un mapa durante la implementación en un servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , de forma predeterminada se muestra un error y la compilación del informe genera un error. Si reduce el **ErrorLevel** , el mapa se quita del informe, se muestra una advertencia y la compilación del informe continúa.  
  
5.  En la lista **StartItem**  , seleccione un informe para que se muestre en la ventana de vista previa o en una ventana del explorador cuando se ejecute el proyecto de informe.  
  
6.  En la lista **OverwriteDataSources** , seleccione **True** para sobrescribir el origen de datos compartido en el servidor cada vez que se publican orígenes de datos compartidos, o seleccione **False** para mantener el origen de datos en el servidor.  
  
7.  En la lista **TargetServerVersion** , seleccione la versión de SQL Server 2016 de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o seleccione **Detectar versión** para determinar automáticamente la versión instalada en el servidor identificado por la propiedad **TargetServer URL** . El valor predeterminado es **SQL Server 2016 o posterior**.  
  
     Utilice **TargetServerVersion** para personalizar los informes compilados, colocados en la ruta de acceso especificada en OutputPath, para la versión del servidor de informes especificada en **TargetServer URL**.  
  
8.  En el cuadro de texto **TargetDataSourceFolder** , escriba la carpeta del servidor de informes donde desea colocar los orígenes de datos compartidos publicados. El valor predeterminado para **TargetDataSourceFolder** es Data Sources. Si deja esta valor en blanco, los orígenes de datos se publicarán en la ubicación especificada en **TargetReportFolder**.  
  
9. En el cuadro de texto **TargetReportFolder** , escriba la carpeta del servidor de informes donde desea colocar los informes publicados. El valor predeterminado de **TargetReportFolder**  es el nombre del proyecto de informe.  
  
    > [!NOTE]  
    >  Para un servidor de informes que se ejecuta en modo nativo, debe disponer de permisos de **publicación** en la carpeta de destino para poder publicar informes en dicha carpeta. Los permisos de publicación se proporcionan mediante una asignación de roles que asigne la cuenta de usuario a un rol que disponga de operaciones de publicación. Para obtener más información, vea [Crear y administrar asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md). Para un servidor de informes que se ejecuta en el modo integrado de SharePoint, debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint. Para obtener más información, vea [Referencia de permisos de sitio y lista de SharePoint para los elementos del servidor de informes](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
10. En el cuadro de texto **TargetServerURL** , escriba la dirección URL del servidor de informes de destino. Antes de publicar un informe, establezca esta propiedad en la dirección URL de un servidor de informes válido. Al publicar en un servidor de informes que se ejecute en modo nativo, use la dirección URL del directorio virtual del servidor de informes (por ejemplo, http:*//servidor/servidorDeInformes* o https:*//servidor/servidorDeInformes)*. Se trata del directorio virtual del servidor de informes, y no del Administrador de informes.  
  
     Al publicar en un servidor de informes que se ejecute en el modo integrado de SharePoint, use una dirección URL a un sitio de nivel superior o un subsitio de SharePoint. Si no especifica ningún sitio, se usa el sitio de nivel superior predeterminado (por ejemplo, http://*nombreDeServidor*, http://*nombreDeServidor*/*sitio* o http://*nombreDeServidor*/*sitio*/*subsitio*).  
  
### <a name="to-set-configuration-manager-properties"></a>Para establecer las propiedades del Administrador de configuración  
  
1.  Haga clic con el botón derecho en el proyecto de informe y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Páginas de propiedades** del proyecto, haga clic en **Administrador de configuración**.  
  
3.  En el cuadro de diálogo **Administrador de configuración** , seleccione la configuración que desea modificar. La configuración activa se muestra como **Active(***\<configuración>***)**.  
  
4.  En **Contextos del proyecto**, para cada proyecto de la solución, active o desactive **Generar** o **Implementar**.  
  
    > [!NOTE]  
    >  Si ha seleccionado **Generar** , el Diseñador de informes genera el proyecto del informe y comprueba si existen errores antes de mostrar una vista previa o publicarlo en un servidor de informes. Si ha seleccionado **Implementar** , el Diseñador de informes publica los informes en el servidor de informes de acuerdo con las propiedades de implementación establecidas. Si no ha seleccionado **Implementar** , el Diseñador de informes muestra el informe especificado en la propiedad **StartItem** en una ventana de vista previa local.  
  
## <a name="see-also"></a>Vea también  
 [Publicar orígenes de datos e informes](../../reporting-services/reports/publishing-data-sources-and-reports.md)   
 [Obtener la vista previa de informes](../../reporting-services/reports/previewing-reports.md)   
 [Diseñador de informes (Ayuda F1)](../../reporting-services/tools/report-designer-f1-help.md)   
 [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Publicar informes en un servidor de informes](../../reporting-services/reports/publishing-reports-to-a-report-server.md)  
  
  

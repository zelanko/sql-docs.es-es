---
title: Crear configuraciones de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e4d13fb24ad337ed6395e8529f4067d8acd2a1c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140645"
---
# <a name="create-package-configurations"></a>Crear configuraciones de paquetes
  Puede crear configuraciones de paquetes con el cuadro de diálogo **Organizador de configuraciones de paquetes** y el Asistente para la configuración de paquetes. Para tener acceso a estas herramientas, haga clic en **Configuraciones de paquetes** en el menú **SSI** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  También puede acceder al **Organizador de configuraciones de paquetes**haciendo clic en el botón de puntos suspensivos junto a la propiedad **Configuración** . La propiedad Configuración aparece en la ventana de propiedades del paquete.  
  
> [!NOTE]  
>  Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 En el cuadro de diálogo **Organizador de configuraciones de paquetes** , puede habilitar paquetes para usar configuraciones, agregar y eliminar configuraciones, y establecer el orden preferido en que se deben cargar las configuraciones.  
  
> [!NOTE]  
>  Cuando las configuraciones de paquetes se cargan en el orden preferido, se cargan de arriba a abajo, según la lista que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Sin embargo, en tiempo de ejecución, las configuraciones de paquetes podrían no cargarse en el orden preferido. Concretamente, las configuraciones de paquetes principales se cargan después de las configuraciones de otros tipos.  
  
> [!NOTE]  
>  Si varias configuraciones establecen la misma propiedad de objeto, el último valor cargado se utiliza en tiempo de ejecución.  
  
 En el cuadro de diálogo **Organizador de configuraciones de paquetes** , puede ejecutar el Asistente para la configuración de paquetes, que guía al usuario para crear una configuración. Para ejecutar el Asistente para la configuración de paquetes, agregue una nueva configuración en el cuadro de diálogo **Organizador de configuraciones de paquetes** o modifique una existente. En las páginas del asistente, puede elegir el tipo de configuración, seleccionar si desea tener acceso directo a la configuración o utilizar variables de entorno, así como seleccionar las propiedades que desee guardar en la configuración.  
  
 En el ejemplo siguiente se muestran las propiedades de destino de una variable y un paquete tal como aparecen en la página de finalización del Asistente para la configuración de paquetes:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 En este ejemplo, la configuración actualiza estas propiedades:  
  
-   La propiedad RaiseChangedEvent de una variable definida por el usuario, `TodaysDate`.  
  
-   Las propiedades MaximumErrorCount, LoggingMode y LocaleID del paquete.  
  
-   La propiedad Value de una variable definida por el usuario, `varTableName`, en el ámbito de la tarea, My SQL Task.  
  
 "\Package" representa la raíz y los puntos (.) separan los objetos que definen la ruta de acceso a la propiedad que actualiza la configuración Los nombres de variables y propiedades se ponen entre corchetes. El término Package se usa siempre en configuración, independientemente del nombre del paquete; sin embargo, los demás objetos de la ruta utilizan sus nombres definidos por el usuario.  
  
 Cuando finaliza el asistente, la nueva configuración se agrega a la lista de configuraciones del cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
> [!NOTE]  
>  La última página del Asistente para la configuración de paquetes, la página Finalización del asistente, enumera las propiedades de destino de la configuración. Si quiere actualizar propiedades cuando ejecuta paquetes mediante la utilidad del símbolo del sistema **dtexec**, puede generar las cadenas que representan las rutas de acceso a las propiedades con el Asistente para configuración de paquetes, y, después, copiarlas y pegarlas en la ventana del símbolo del sistema para usarlas con la opción establecida de **dtexec**.  
  
 En la tabla siguiente se describen las columnas de la lista de configuraciones del cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
|columna|Descripción|  
|------------|-----------------|  
|**Nombre de la configuración**|Nombre de la configuración.|  
|**Tipo de configuración**|Tipo de configuración.|  
|**Cadena de configuración**|Ubicación de la configuración. La ubicación puede ser una ruta de acceso, una variable de entorno, una clave del Registro, un nombre de variable de paquete primario o una tabla de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Objeto de destino**|Nombre del objeto que tiene una propiedad con una configuración. Si la configuración es un archivo de configuración XML, la columna aparece en blanco, ya que la configuración puede actualizar varios objetos.|  
|**Propiedad de destino**|El nombre de la propiedad. Si la configuración escribe en un archivo de configuración XML o una tabla de SQL Server, la columna aparece en blanco, ya que la configuración puede actualizar varios objetos.|  
  
### <a name="to-create-a-package-configuration"></a>Para crear una configuración de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en las pestañas **Flujo de control**, **Flujo de datos**, **Controlador de eventos**o **Explorador de paquetes** .  
  
4.  En el menú **SSIS** , haga clic en **Configuraciones de paquetes**.  
  
5.  En el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Habilitar configuraciones de paquetes**y haga clic en **Agregar**.  
  
6.  En la página de bienvenida del Asistente para la configuración de paquetes, haga clic en **Siguiente**.  
  
7.  En la página Seleccionar tipo de configuración, especifique el tipo de configuración y establezca las propiedades relevantes para el tipo de configuración. Para más información, vea [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md).  
  
8.  En la página Seleccionar propiedades para la exportación, seleccione las propiedades de los objetos de paquete que desee incluir en la configuración. Si el tipo de configuración admite solamente una propiedad, el título de esta página del asistente es Seleccionar propiedad de destino. Para más información, vea [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md).  
  
    > [!NOTE]  
    >  Los tipos de configuración **Archivo de configuración XML** y **SQL Server** son los únicos que admiten varias propiedades en una configuración.  
  
9. En la página Finalización del asistente, escriba el nombre de la configuración y haga clic en **Finalizar**.  
  
10. Vea la configuración en el cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
11. Haga clic en **Cerrar**.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artículo técnico con una [introducción a las configuraciones de paquetes de Integration Services](http://go.microsoft.com/fwlink/?LinkId=165643), en msdn.microsoft.com  
  
-   Entrada de blog, [Crear paquetes en código: configuraciones de paquetes](http://go.microsoft.com/fwlink/?LinkId=217663), en www.sqlis.com.  
  
-   Entrada de blog, [API de ejemplo: agregar mediante programación un archivo de configuración a un paquete](http://go.microsoft.com/fwlink/?LinkId=217664), en blogs.msdn.com.  
  
## <a name="see-also"></a>Vea también  
 [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md)   
 [Implementación del paquete &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Trabajar con variables mediante programación](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  

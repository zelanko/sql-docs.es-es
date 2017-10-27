---
title: "Implementación de paquetes heredada (SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 15c21ac27069d582a7006c38993f48dc3f4ed0be
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="legacy-package-deployment-ssis"></a>Implementación de paquetes heredada (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye herramientas y asistentes para facilitar la implementación de paquetes del equipo de desarrollo en el servidor de producción o en otros equipos.  
  
 El proceso de implementación de paquetes consta de cuatro pasos:  
  
1.  El primer paso es opcional e implica crear configuraciones de paquetes que actualizan las propiedades de los elementos de los paquetes en tiempo de ejecución. Las configuraciones se incluyen automáticamente al implementar los paquetes.  
  
2.  El segundo paso es generar el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para crear una utilidad de implementación de paquetes. La utilidad de implementación del proyecto contiene los paquetes que desea implementar.  
  
3.  El tercer paso es copiar la carpeta de implementación que se creó al generar el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el equipo de destino.  
  
4.  El cuarto paso es ejecutar en el equipo de destino el Asistente para la instalación de paquetes con el fin de instalar los paquetes en el sistema de archivos o en una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="package-configurations"></a>Configuraciones de paquetes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona configuraciones de paquetes que se pueden usar para actualizar los valores de las propiedades en tiempo de ejecución.  
  
> **NOTA:** Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
 Una configuración es una par propiedad/valor que se agrega a un paquete completo. Normalmente, se crean las propiedades establecidas de un paquete para los objetos del paquete durante el desarrollo y, después, se agrega la configuración al paquete. Cuando se ejecuta el paquete, éste recibe de la configuración los nuevos valores de la propiedad. Por ejemplo, al utilizar una configuración, se puede modificar la cadena de conexión de un administrador de conexiones o actualizar el valor de una variable.  
  
 Las configuraciones de paquetes ofrecen las siguientes ventajas:  
  
-   Permiten mover más fácilmente los paquetes de un entorno de desarrollo a un entorno de producción. Por ejemplo, una configuración puede actualizar la ruta de acceso de un archivo de origen, o bien cambiar el nombre de una base de datos o servidor.  
  
-   Son útiles para implementar paquetes en varios servidores distintos. Por ejemplo, una variable en la configuración de cada paquete implementado puede contener un valor de espacio de disco distinto, y si el espacio de disco disponible es menor que dicho valor, el paquete no se ejecuta.  
  
-   Aumentan la flexibilidad de los paquetes. Por ejemplo, una configuración puede actualizar el valor de una variable que se utiliza en una expresión de propiedad.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite varios métodos distintos para almacenar configuraciones de paquetes, como archivos XML, tablas de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y variables de entorno y de paquete.  
  
 Cada configuración es una pareja propiedad/valor. El archivo de configuración XML y los tipos de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden incluir varias configuraciones.  
  
 Las configuraciones se incluyen al crear una utilidad de implementación de paquetes para instalar paquetes. Al instalar los paquetes, las configuraciones se pueden actualizar como un paso en la instalación del paquete.  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>Cómo se aplican las configuraciones de paquetes en tiempo de ejecución  
 Cuando usa la utilidad de símbolo del sistema **dtexec** (dtexec.exe) para ejecutar un paquete implementado, la utilidad aplica las configuraciones de paquetes dos veces. antes y después de aplicar las opciones que se especificaron en la línea de comandos.  
  
 A medida que la utilidad carga y ejecuta el paquete, los eventos se producen en el orden siguiente:  
  
1.  La utilidad **dtexec** carga el paquete.  
  
2.  La utilidad aplica las configuraciones que se especificaron en el paquete en tiempo de diseño, en el orden indicado en el paquete. (Las configuraciones de las variables de paquetes primarios son la excepción. La utilidad solo aplica estas configuraciones una vez y al final en el proceso).  
  
3.  A continuación, la utilidad aplica cualquier opción que especificara en la línea de comandos.  
  
4.  La utilidad vuelve a cargar entonces las configuraciones que se especificaron en el paquete en tiempo de diseño, en el orden indicado en el paquete. (De nuevo, la excepción a esta regla son las configuraciones de variables de paquetes primarios). La utilidad utiliza las opciones de la línea de comandos que se especificaran para volver a cargar las configuraciones. Por consiguiente, se podrían volver a cargar valores diferentes desde una ubicación diferente.  
  
5.  La utilidad aplica las configuraciones de variables de paquetes primarios.  
  
6.  La utilidad ejecuta el paquete.  
  
 La manera en la que la utilidad **dtexec** aplica las configuraciones afecta a estas opciones de la línea de comandos:  
  
-   Puede usar la opción **/Connection** o **/Set** en tiempo de ejecución para cargar configuraciones de paquete desde una ubicación distinta de la que ha especificado en tiempo de diseño.  
  
-   Puede usar la opción **/ConfigFile** para cargar configuraciones adicionales que no ha especificado en tiempo de diseño.  
  
 Sin embargo, estas opciones de la línea de comandos tienen algunas restricciones:  
  
-   No puede usar la opción **/Set** o **/Connection** para invalidar valores únicos que también se establezcan en una configuración.  
  
-   No puede usar la opción **/ConfigFile** para cargar configuraciones que reemplacen las configuraciones que ha especificado en tiempo de diseño.  
  
 Para más información sobre estas opciones y cómo difiere el comportamiento de estas opciones entre [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] y las versiones anteriores, vea [Cambios del comportamiento en las características de Integration Services en SQL Server 2016](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
### <a name="package-configuration-types"></a>Tipos de configuraciones de paquetes  
 En la tabla siguiente se describen los tipos de configuraciones de paquetes.  
  
|Tipo|Description|  
|----------|-----------------|  
|Archivo de configuración XML|Un archivo XML contiene las configuraciones. El archivo XML puede incluir varias configuraciones.|  
|Variable de entorno|Una variable de entorno contiene la configuración.|  
|Entrada del Registro|Una entrada del Registro contiene la configuración.|  
|Variable de paquete primario|Una variable del paquete contiene la configuración. Este tipo de configuración se utiliza habitualmente para actualizar las propiedades de los paquetes secundarios.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table|Una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene la configuración. La tabla puede incluir varias configuraciones.|  
  
#### <a name="xml-configuration-files"></a>Archivos de configuración XML  
 Si selecciona el tipo de configuración **Archivo de configuración XML** , puede crear un archivo de configuración, reutilizar un archivo existente y agregarle configuraciones nuevas, o bien reutilizar un archivo existente sobrescribiendo el contenido actual.  
  
 Un archivo de configuración XML tiene dos secciones:  
  
-   Un encabezado que contiene información acerca del archivo de configuración. Este elemento incluye atributos como por ejemplo, cuándo se creó el archivo y el nombre de la persona que lo generó.  
  
-   Elementos de configuración que contienen información acerca de cada configuración. Este elemento incluye atributos como la ruta de acceso de la propiedad y el valor configurado de una propiedad.  
  
 El siguiente código XML muestra la sintaxis de un archivo de configuración XML. En este ejemplo se muestra una configuración para la propiedad Value de una variable entera llamada `MyVar`.  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>Entrada del Registro  
 Si desea usar una entrada del Registro para guardar la configuración, puede usar una clave existente o crear otra en HKEY_CURRENT_USER. La clave del Registro que utilice debe tener un valor denominado **Value**. El valor puede ser un valor de tipo DWORD o una cadena.  
  
 Si selecciona el tipo de configuración **Entrada del Registro** , debe escribir el nombre de la clave del Registro en el cuadro de texto del Registro. El formato es \<clave del registro >. Si desea usar una clave del registro que no está en la raíz de HKEY_CURRENT_USER, use el formato \<key\registry clave\\... > para identificar la clave. Por ejemplo, para usar la clave MyPackage de SSISPackages, escriba **SSISPackages\MyPackage**.  
  
#### <a name="sql-server"></a>SQL Server  
 Si selecciona el tipo de configuración **SQL Server** , debe especificar la conexión a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que desee almacenar las configuraciones. Puede guardar las configuraciones en una tabla existente o crear una tabla nueva en la base de datos especificada.  
  
 La siguiente instrucción SQL muestra la instrucción CREATE TABLE predeterminada que proporciona el Asistente para la configuración de paquetes.  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 El nombre que asigna a la configuración es el valor que se almacena en la columna **ConfigurationFilter** .  
  
### <a name="direct-and-indirect-configurations"></a>Configuraciones directas e indirectas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona configuraciones directas e indirectas. Si especifica las configuraciones directamente, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un vínculo directo entre el elemento de configuración y la propiedad del objeto de paquete. Las configuraciones directas son una opción mejor cuando la ubicación del origen no cambia. Por ejemplo, si está seguro de que todas las implementaciones del paquete utilizarán la misma ruta de acceso al archivo, puede especificar un archivo de configuración XML.  
  
 Las configuraciones indirectas utilizan variables de entorno. En lugar de especificar el entorno de configuración directamente, la configuración apunta a una variable de entorno, que a su vez contiene el valor de configuración. Las configuraciones indirectas son una opción mejor cuando la ubicación de la configuración puede cambiar en cada implementación de un paquete.  

## <a name="create-package-configurations"></a>Crear configuraciones de paquetes
  Cree configuraciones de paquetes con el cuadro de diálogo **Organizador de configuraciones de paquetes** y el Asistente para la configuración de paquetes. Para tener acceso a estas herramientas, haga clic en **Configuraciones de paquetes** en el menú **SSI** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **COMENTARIOS:**
>También puede acceder al **Organizador de configuraciones de paquetes** haciendo clic en el botón de puntos suspensivos junto a la propiedad **Configuración** . La propiedad Configuración aparece en la ventana de propiedades del paquete.  
  
>Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
  
>En el cuadro de diálogo **Organizador de configuraciones de paquetes** , puede habilitar paquetes para usar configuraciones, agregar y eliminar configuraciones, y establecer el orden preferido en que se deben cargar las configuraciones. 
 
>Cuando las configuraciones de paquetes se cargan en el orden preferido, se cargan de arriba a abajo, según la lista que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Sin embargo, en tiempo de ejecución, las configuraciones de paquetes podrían no cargarse en el orden preferido. Concretamente, las configuraciones de paquetes principales se cargan después de las configuraciones de otros tipos.  
  
>Si varias configuraciones establecen la misma propiedad de objeto, el último valor cargado se utiliza en tiempo de ejecución.  
  
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
  
> **NOTA:** La última página del Asistente para la configuración de paquetes, la página Finalización del asistente, enumera las propiedades de destino de la configuración. Si quiere actualizar propiedades cuando ejecuta paquetes mediante la utilidad del símbolo del sistema **dtexec** , puede generar las cadenas que representan las rutas de acceso a las propiedades con el Asistente para configuración de paquetes, y, después, copiarlas y pegarlas en la ventana del símbolo del sistema para usarlas con la opción establecida de **dtexec**.  
  
 En la tabla siguiente se describen las columnas de la lista de configuraciones del cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
|Columna|Description|  
|------------|-----------------|  
|**Nombre de la configuración**|Nombre de la configuración.|  
|**Tipo de configuración**|Tipo de configuración.|  
|**Cadena de configuración**|Ubicación de la configuración. La ubicación puede ser una ruta de acceso, una variable de entorno, una clave del Registro, un nombre de variable de paquete primario o una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Objeto de destino**|Nombre del objeto que tiene una propiedad con una configuración. Si la configuración es un archivo de configuración XML, la columna aparece en blanco, ya que la configuración puede actualizar varios objetos.|  
|**Propiedad de destino**|El nombre de la propiedad. Si la configuración escribe en un archivo de configuración XML o una tabla de SQL Server, la columna aparece en blanco, ya que la configuración puede actualizar varios objetos.|  
  
### <a name="to-create-a-package-configuration"></a>Para crear una configuración de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en las pestañas **Flujo de control**, **Flujo de datos**, **Controlador de eventos**o **Explorador de paquetes** .  
  
4.  En el menú **SSIS** , haga clic en **Configuraciones de paquetes**.  
  
5.  En el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Habilitar configuraciones de paquetes**y haga clic en **Agregar**.  
  
6.  En la página de bienvenida del Asistente para la configuración de paquetes, haga clic en **Siguiente**.  
  
7.  En la página Seleccionar tipo de configuración, especifique el tipo de configuración y establezca las propiedades relevantes para el tipo de configuración. Para más información, vea [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  En la página Seleccionar propiedades para la exportación, seleccione las propiedades de los objetos de paquete que desee incluir en la configuración. Si el tipo de configuración admite solamente una propiedad, el título de esta página del asistente es Seleccionar propiedad de destino. Para más información, vea [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **NOTA:** Los tipos de configuración **Archivo de configuración XML** y **SQL Server** son los únicos que admiten varias propiedades en una configuración.  
  
9. En la página Finalización del asistente, escriba el nombre de la configuración y haga clic en **Finalizar**.  
  
10. Vea la configuración en el cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
11. Haga clic en **Cerrar**.  

## <a name="package-configurations-organizer"></a>Organizador de configuraciones de paquetes
  Utilice el cuadro de diálogo **Organizador de configuraciones de paquetes** para habilitar las configuraciones de paquetes, ver una lista de configuraciones para el paquete actual y especificar el orden de preferencia en el que se deben cargar las configuraciones.  
  
> **NOTA:** Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
  
 Si varias configuraciones actualizan la misma propiedad, los valores de las configuraciones que aparezcan más abajo en la lista reemplazarán los valores de aquéllas que ocupen un lugar superior en la lista. El último valor cargado en la propiedad es el valor que se usa cuando se ejecuta el paquete. Asimismo, si el paquete utiliza una combinación de configuración directa, como un archivo de configuración XML, y configuración indirecta, como una variable de entorno, la configuración indirecta que señala a la ubicación de la configuración directa debe ocupar un lugar superior en la lista.  
  
> **NOTA:** Cuando las configuraciones de paquetes se cargan en el orden preferido, se cargan de arriba a abajo, según la lista que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Sin embargo, en tiempo de ejecución, las configuraciones de paquetes podrían no cargarse en el orden preferido. Concretamente, las configuraciones de paquetes principales se cargan después de las configuraciones de otros tipos.  
  
 Las configuraciones de paquetes actualizan los valores de las propiedades de los objetos de paquete en tiempo de ejecución. Cuando se carga un paquete, los valores de las configuraciones reemplazan los valores establecidos cuando se desarrolló el paquete. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite distintos tipos de configuración. Por ejemplo, se puede utilizar un archivo XML que contenga múltiples configuraciones o una variable de entorno que contenga una única configuración. Para más información, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### <a name="options"></a>Opciones  
 **Habilitar configuraciones de paquetes**  
 Seleccione esta opción para utilizar las configuraciones incluidas con el paquete.  
  
 **Nombre de la configuración**  
 Presenta el nombre de la configuración.  
  
 **Tipo de configuración**  
 Presenta el tipo de la ubicación donde se almacenan las configuraciones.  
  
 **Cadena de configuración**  
 Presenta la ubicación donde se almacenan los valores de configuración. La ubicación puede ser la ruta de acceso a un archivo, el nombre de una variable de entorno, el nombre de una variable de paquete principal, una clave del Registro o el nombre de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Objeto de destino**  
 Muestra el nombre del objeto que la configuración actualiza. Si la configuración se encuentra en un archivo de configuración XML o una tabla de SQL Server, la columna aparece en blanco, ya que la configuración puede incluir varios objetos.  
  
 **Propiedad de destino**  
 Presenta el nombre de la propiedad modificada por la configuración. La columna está en blanco si el tipo de configuración admite varias configuraciones.  
  
 **Agregar**  
 Agrega una configuración empleando el Asistente para la configuración de paquetes.  
  
 **Editar**  
 Edita una configuración existente volviendo a ejecutar el Asistente para la configuración de paquetes.  
  
 **Quitar**  
 Seleccione una configuración y haga clic en **Quitar**.  
  
 **Flechas**  
 Seleccione una configuración y utilice las flechas arriba y abajo para subirla o bajarla de la lista. Las configuraciones se cargan en la secuencia en la que aparecen en la lista.  

## <a name="package-configuration-wizard-ui-reference"></a>Referencia de la interfaz de usuario del Asistente para la configuración de paquetes
  Use el **Asistente para la configuración de paquetes** para crear configuraciones que actualizan las propiedades de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y sus objetos en tiempo de ejecución. Este asistente se ejecuta al agregar una nueva configuración o modificar una existente en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Para abrir el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Configuraciones de paquetes** en el menú **SSIS** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para más información, vea [Crear configuraciones de paquetes](../../integration-services/packages/create-package-configurations.md).  
  
> **NOTA:** Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 En las siguientes secciones se describen las páginas del asistente.  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>Asistente para la configuración de paquetes (página principal)  
 Use el **Asistente para la configuración de SSIS** para crear configuraciones que actualizan las propiedades de un paquete y sus objetos en tiempo de ejecución.  
  
#### <a name="options"></a>Opciones  
 **No volver a mostrar esta página**  
 Omite la página de bienvenida la próxima vez que abre el asistente.  
  
 **Siguiente**  
 Avanza a la página siguiente del asistente.  
  
### <a name="select-configuration-type-page"></a>Página Seleccionar tipo de configuración  
 Use la página **Seleccionar tipo de configuración** para especificar el tipo de configuración que se creará.  
  
 Si necesita obtener información adicional para determinar el tipo de configuración que debe utilizar, vea [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
#### <a name="static-options"></a>Opciones estáticas  
 **Tipo de configuración**  
 Seleccione el tipo de origen en el que se almacenará la configuración, utilizando las siguientes opciones:  
  
|Value|Description|  
|-----------|-----------------|  
|**Archivo de configuración XML**|Almacenar la configuración como un archivo XML. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Variable de entorno**|Almacenar la configuración en una de las variables de entorno. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Entrada del Registro**|Almacenar la configuración en el Registro. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Variable de paquete primario**|Almacenar la configuración como una variable en el paquete que contiene la tarea.  Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**SQL Server**|Almacenar la configuración en una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
  
 **Siguiente**  
 Muestra la siguiente página en la secuencia del asistente.  
  
#### <a name="dynamic-options"></a>Opciones dinámicas  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>Opción de tipo de configuración = Archivo de configuración XML  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Description|  
|-----------|-----------------|  
|**Nombre del archivo de configuración**|Escriba la ruta de acceso del archivo de configuración que genera el asistente.|  
|**Examinar**|Use el cuadro de diálogo **Seleccionar ubicación del archivo de configuración** para especificar la ruta de acceso del archivo de configuración que genera el asistente. Si el archivo no existe, el asistente lo crea.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se usa para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Description|  
|-----------|-----------------|  
|**Variable de entorno**|Seleccione una variable de entorno de la lista.|  
  
##### <a name="configuration-type-option--environment-variable"></a>Opción de tipo de configuración = Variable de entorno  
 **Variable de entorno**  
 Seleccione la variable de entorno que contiene la información de configuración.  
  
##### <a name="configuration-type-option--registry-entry"></a>Opción de tipo de configuración = Entrada del Registro  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada del Registro**|Escriba la clave del Registro que contiene la información de configuración. El formato es \<clave del registro >.<br /><br /> La clave del Registro ya debe existir en HKEY_CURRENT_USER y tener un valor con el nombre Value. El valor puede ser un valor de tipo DWORD o una cadena.<br /><br /> Si desea usar un registro de clave no está registrado en la raíz de HKEY_CURRENT_USER, use el formato \<key\registry clave\\... > para identificar la clave.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se utiliza para especificar la variable de entorno donde debe almacenarse la configuración.  
  
|Value|Description|  
|-----------|-----------------|  
|**Variable de entorno**|Seleccione una variable de entorno de la lista.|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>Opción de tipo de configuración = Variable de paquete primario  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Description|  
|-----------|-----------------|  
|**Variable primaria**|Especifique la variable del paquete primario que contiene la información de configuración.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se usa para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Description|  
|-----------|-----------------|  
|**Variable de entorno**|Seleccione una variable de entorno de la lista.|  
  
##### <a name="configuration-type-options--sql-server"></a>Opción de tipo de configuración = SQL Server  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexión**|Seleccione una conexión de la lista o haga clic en **Nueva** para crear una nueva conexión.|  
|**Tabla de configuración**|Seleccione una tabla existente o haga clic en **Nueva** para escribir una instrucción SQL que cree la nueva tabla.|  
|**Filtro de la configuración**|Seleccione un nombre de configuración existente o escriba uno nuevo.<br /><br /> Muchas de las configuraciones de SQL Server se pueden almacenar en la misma tabla, y cada configuración puede incluir varios elementos de configuración.<br /><br /> Este valor definido por el usuario se almacena en la tabla para identificar los elementos de configuración de una configuración determinada.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se utiliza para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Description|  
|-----------|-----------------|  
|**Variable de entorno**|Seleccione una variable de entorno de la lista.|  
  
### <a name="select-objects-to-export-page"></a>Página Seleccionar objetos para la exportación  
 Use la página **Seleccionar propiedad de destino o Seleccionar propiedades para la exportación** para especificar las propiedades de objetos contenidas en la configuración. La posibilidad de seleccionar varias propiedades solo está disponible si se selecciona el tipo de configuración XML.  
  
#### <a name="options"></a>Opciones  
 **Objetos**  
 Expanda la jerarquía de paquetes y seleccione las propiedades que desea exportar.  
  
 **Atributos de propiedad**  
 Permite ver los atributos de una propiedad.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
### <a name="completing-the-wizard-page"></a>Página Finalización del asistente  
 Utilice la página **Finalización del asistente** para asignar un nombre a la configuración y ver los valores utilizados por el asistente para crear la configuración. Una vez que finaliza el asistente, se muestra el **Organizador de configuraciones de paquetes** , que enumera todas las configuraciones para el paquete.  
  
#### <a name="options"></a>Opciones  
 **Nombre de la configuración**  
 Escriba el nombre de la configuración.  
  
 **Vista previa**  
 Muestra los valores utilizados por el asistente para crear la configuración.  
  
 **Finalizar**  
 Crea la configuración y sale del **Asistente para configuración de paquetes**.  

## <a name="child"></a>Use los valores de Variables y parámetros de un paquete secundario
  Este procedimiento describe cómo crear una configuración de paquete que utiliza el tipo de configuración de variables primarias. Este tipo de configuración habilita un paquete secundario que se ejecuta desde un paquete primario para tener acceso a una variable del elemento primario.  
  
> [!NOTE]  
>  También puede pasar valores a un paquete secundario configurando la Tarea Ejecutar paquete para asignar variables o parámetros del paquete primario, o parámetros del proyecto, a parámetros del paquete secundario. Para más información, consulte [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
 No es necesario crear la variable en el paquete primario antes de crear la configuración de paquete en el paquete secundario. Puede agregar la variable al paquete primario en cualquier momento, pero debe utilizar el nombre exacto de la variable primaria en la configuración del paquete. Sin embargo, antes de que pueda crear una configuración de variable primaria, debe existir una variable en el paquete secundario que la configuración pueda actualizar. Para obtener más información sobre cómo agregar y configurar variables, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
 El ámbito de la variable del paquete primario que se utiliza en una configuración de variable primaria se puede establecer en la tarea Ejecutar paquete, el contenedor que contiene la tarea o el paquete. Si se definen varias variables con el mismo nombre en un paquete, se utiliza la variable que está más próxima en ámbito de la tarea Ejecutar paquete. El ámbito más cercano a la tarea Ejecutar paquete es la tarea propiamente dicha.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Para agregar una variable a un paquete primario  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete al que desea agregar una variable para pasar a un paquete secundario.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , siga uno de estos procedimientos para definir el ámbito de la variable:  
  
    -   Para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
    -   Para establecer el ámbito en un contenedor primario de la tarea Ejecutar paquete, haga clic en el contenedor.  
  
    -   Para establecer el ámbito a la tarea Ejecutar paquete, haga clic en ella.  
  
4.  Agregue y configure una variable.  
  
    > [!NOTE]  
    >  Seleccione un tipo de datos que sea compatible con los datos que almacenará la variable.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Para agregar una variable a un paquete secundario  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete al que desea agregar una configuración de variable primaria.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
4.  Agregue y configure una variable.  
  
    > [!NOTE]  
    >  Seleccione un tipo de datos que sea compatible con los datos que almacenará la variable.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  

## <a name="create-a-deployment-utility"></a>Crear una utilidad de implementación
  El primer paso para implementar paquetes es crear una utilidad de implementación para un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La utilidad de implementación es una carpeta que contiene los archivos necesarios para implementar los paquetes de un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un servidor distinto. La utilidad de implementación se crea en el equipo en el que se almacena el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Puede crear una utilidad de implementación de paquetes para un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] configurando primero el proceso de generación de una utilidad de implementación y después, generando el proyecto. Al generar el proyecto, todos los paquetes y configuraciones de paquetes del proyecto se incluyen automáticamente. Para implementar archivos adicionales con el proyecto, como un archivo Léame, coloque los archivos en la carpeta **Miscellaneous** del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Al generar el proyecto, estos archivos también se incluirán automáticamente.  
  
 Puede configurar de manera distinta la implementación de cada proyecto. Antes de generar el proyecto y de crear la utilidad de implementación de paquetes, puede establecer sus propiedades para personalizar la forma en que se implementarán los paquetes en el proyecto. Por ejemplo, puede especificar si desea que las configuraciones de paquetes se actualicen al implementar el proyecto. Para tener acceso a las propiedades de un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , haga clic con el botón derecho en el proyecto y, después, haga clic en **Propiedades**.  
  
 En la tabla siguiente se muestran las propiedades de la utilidad de implementación.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|Valor que especifica si se actualizarán las configuraciones durante la implementación.|  
|CreateDeploymentUtility|Valor que especifica si se creará una utilidad de implementación de paquetes al generar el proyecto. Esta propiedad debe estar establecida en **True** para crear una utilidad de implementación.|  
|DeploymentOutputPath|Ubicación, respecto al proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , de la utilidad de implementación.|  
  
 Cuando se crea un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proyecto, un archivo de manifiesto \<nombre del proyecto >. SSISDeploymentManifest.xml, se crea y agrega, junto con las copias de los paquetes del proyecto y las dependencias del paquete, en la carpeta bin\Deployment en el proyecto o en la ubicación especificada en la propiedad DeploymentOutputPath. El archivo de manifiesto muestra los paquetes, las configuraciones de paquetes y todos los demás archivos del proyecto.  
  
 El contenido de la carpeta de implementación se actualiza cada vez que genera el proyecto. Esto significa que se eliminará cualquier archivo guardado en esta carpeta que no se copie nuevamente en el proceso de generación. Por ejemplo, se eliminarán archivos de configuración de paquetes guardados en las carpetas de implementación.  
  
### <a name="to-create-a-package-deployment-utility"></a>Para crear una utilidad de implementación de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra la solución que contiene el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para el que desee crear una utilidad de implementación de paquetes.  
  
2.  Haga clic con el botón derecho en el proyecto y haga clic en **Propiedades**.  
  
3.  En el  **\<nombre del proyecto > páginas de propiedades** cuadro de diálogo, haga clic en **utilidad de implementación**.  
  
4.  Para actualizar las configuraciones de paquetes al implementar los paquetes, establezca **AllowConfigurationChanges** en **True**.  
  
5.  Establezca **CreateDeploymentUtility** en **True**.  
  
6.  Opcionalmente, actualice la ubicación de la utilidad de implementación modificando la propiedad **DeploymentOutputPath** .  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y, después, haga clic en **Generar**.  
  
9. Vea el progreso y los errores de la generación en la ventana **Salida** .  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>Implementar los paquetes mediante la utilidad de implementación
  Después de generar una utilidad de implementación para instalar paquetes de un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo distinto del que se utilizó para generar la utilidad, debe copiar la carpeta de implementación en el equipo de destino.  
  
 La ruta de acceso a la carpeta de implementación se especifica en la propiedad DeploymentOutputPath del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para el que ha creado la utilidad de implementación. La ruta predeterminada es bin\Deployment, relativa al proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para más información, consulte [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Para instalar los paquetes, puede utilizar el Asistente para la instalación de paquetes. Para iniciar el asistente, haga doble clic en el archivo de la utilidad de implementación una vez copiada la carpeta de implementación en el servidor. Este archivo se denomina \<nombre del proyecto >. SSISDeploymentManifest y puede encontrarse en la carpeta de implementación en el equipo de destino.  
  
> [!NOTE]  
>  Dependiendo de la versión del paquete que esté implementando, puede encontrar un error si tiene varias versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en paralelo. Este error puede producirse porque la extensión de nombre de archivo .SSISDeploymentManifest es la misma para todas las versiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Al hacer doble clic en el archivo, se llama al instalador (dtsinstall.exe) para la versión instalada más recientemente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que podría no ser la misma versión que la del archivo de la utilidad de implementación. Para evitar este problema, ejecute la versión correcta de dtsinstall.exe desde la línea de comandos y proporcione la ruta de acceso al archivo de la utilidad de implementación.  
  
 El Asistente para la instalación de paquetes le guía paso a paso durante la instalación de paquetes en el sistema de archivos o en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede configurar la instalación de las maneras siguientes:  
  
-   Eligiendo el tipo de ubicación y la ubicación para instalar los paquetes.  
  
-   Eligiendo la ubicación para instalar las dependencias de paquete.  
  
-   Validando los paquetes una vez instalados en el servidor de destino.  
  
 Las dependencias basadas en archivos de los paquetes se instalan siempre en el sistema de archivos. Si instala un paquete en el sistema de archivos, las dependencias se instalarán en la misma carpeta que especificó para el paquete. Si instala un paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar la carpeta en la que desee almacenar las dependencias basadas en archivo.  
  
 Si el paquete incluye configuraciones que desea modificar para utilizarlas en el equipo de destino, puede utilizar el asistente para actualizar los valores de las propiedades.  
  
 Además de instalar paquetes con el Asistente para instalar paquetes, puede copiar y mover paquetes con la utilidad **dtutil** del símbolo del sistema. Para más información, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>Para implementar paquetes en una instancia de SQL Server  
  
1.  Abra la carpeta de implementación en el equipo de destino.  
  
2.  Haga doble clic en el archivo de manifiesto, \<nombre del proyecto >. SSISDeploymentManifest, para iniciar al Asistente para la instalación de paquetes.  
  
3.  En la página **Implementar paquetes SSIS** , seleccione la opción **Implementación en SQL Server** .  
  
4.  Opcionalmente, puede seleccionar **Validar los paquetes después de la instalación** para validar los paquetes una vez instalados en el servidor de destino.  
  
5.  En la página **Especificar el servidor SQL Server de destino** , especifique la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que desee instalar los paquetes y seleccione un modo de autenticación. Si selecciona la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , deberá proporcionar un nombre de usuario y una contraseña.  
  
6.  En la página **Seleccionar la carpeta de instalación** , especifique la carpeta del sistema de archivos para las dependencias de paquete que se instalarán.  
  
7.  Si el paquete incluye configuraciones, puede modificarlas actualizando los valores de la lista **Valor** de la página Configurar paquetes.  
  
8.  Si elige validar los paquetes después de la instalación, vea los resultados de la validación de los paquetes implementados.  

## <a name="redeployment-of-packages"></a>Volver a implementar paquetes
  Después de implementar un proyecto, es posible que necesite actualizar o ampliar las funciones del paquete y después, volver a implementar el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene los paquetes actualizados. Como parte del proceso de volver a implementar paquetes, debe revisar las propiedades de configuración incluidas en la utilidad de implementación. Por ejemplo, es posible que no desee permitir cambios en la configuración después de volver a implementar el paquete.  
  
### <a name="process-for-redeployment"></a>Proceso para volver a implementar  
 Cuando termine de actualizar los paquetes, vuelva a generar el proyecto, copiar la carpeta de implementación al equipo de destino y ejecutar el Asistente para la instalación de paquetes.  
  
 Si solo actualiza unos cuantos paquetes del proyecto, es posible que no desee volver a implementar todo el proyecto. Para implementar solamente algunos paquetes, puede crear un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , agregarle los paquetes actualizados y después, generar e implementar el proyecto. Las configuraciones de paquetes se copian automáticamente junto con el paquete al agregarlo a otro proyecto.  

## <a name="package-installation-wizard-ui-reference"></a>Referencia de la interfaz de usuario del Asistente para la instalación de paquetes
  Use el **Asistente para la instalación de paquetes** para implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , incluidos los paquetes y los distintos archivos que contienen, así como las dependencias del paquete.  
  
 Antes de implementar paquetes, puede crear configuraciones y después implementarlas con los paquetes. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utiliza configuraciones para actualizar dinámicamente las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. Por ejemplo, la cadena de conexión de una conexión OLE DB puede establecerse dinámicamente en tiempo de ejecución proporcionando una configuración que asigne un valor a la propiedad que contiene la cadena de conexión.  
  
 No se puede ejecutar el Asistente para la instalación de paquetes hasta que se genere un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y se cree una utilidad de implementación. Para más información, consulte [Deploy Packages by Using the Deployment Utility](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 En las siguientes secciones se describen las páginas del asistente.  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>Asistente para la instalación de paquetes (página principal)  
 Use el **Asistente para la instalación de paquetes** para implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para el que ha creado una utilidad de implementación de paquetes.  
  
 **No volver a mostrar esta página**  
 Seleccione para omitir la página de inicio al volver a ejecutar el asistente.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
### <a name="configure-packages-page"></a>Página Configurar paquetes  
 Utilice la página **Configurar paquetes** para modificar la configuración de los paquetes.  
  
#### <a name="options"></a>Opciones  
 **Archivo de configuración**  
 Para modificar el contenido de un archivo de configuración, seleccione el archivo en la lista.  
  
 **Related Topics:** [Create Package Configurations](../../integration-services/packages/create-package-configurations.md)  
  
 **Ruta de acceso**  
 Muestra la ruta de acceso de la propiedad que debe configurarse.  
  
 **Tipo**  
 Muestra el tipo de datos de la propiedad.  
  
 **Value**  
 Especifique el valor de la configuración.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
### <a name="confirm-installation-page"></a>Página Confirmar la instalación  
 Use la página **Confirmar la instalación** para iniciar la instalación de paquetes, ver el estado y ver la información que utilizará el asistente para instalar los archivos del proyecto especificado.  
  
 **Siguiente**  
 Instale los paquetes y sus dependencias y vaya a la siguiente página del asistente una vez completada la instalación.  
  
 **Estado**  
 Muestra el progreso de la instalación del paquete.  
  
 **Finalizar**  
 Vaya a la página Salir del Asistente para la instalación de paquetes. Utilice esta opción si ha comprobado las páginas del asistente para revisar sus elecciones y ha especificado todas las opciones necesarias.  
  
### <a name="deploy-ssis-packages-page"></a>Página Implementar paquetes SSIS  
 Use la página **Implementar paquetes SSIS** para especificar dónde instalar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y sus dependencias.  
  
#### <a name="options"></a>Opciones  
 **Implementación en el sistema de archivos**  
 Implementa paquetes y dependencias en una carpeta determinada del sistema de archivos.  
  
 **Implementación en SQL Server**  
 Implementa paquetes y dependencias en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta opción si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comparte paquetes entre servidores. Las dependencias de paquetes se instalan en la carpeta especificada del sistema de archivos.  
  
 **Validar los paquetes después de la instalación**  
 Indica si se van a validar los paquetes después de la instalación.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
### <a name="packages-validation-page"></a>Página Validación de paquetes  
 Use la página **Validación de paquetes** para ver el progreso y los resultados de la validación del paquete.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
### <a name="select-installation-folder-page"></a>Página Seleccionar la carpeta de instalación  
 Use la página **Seleccionar la carpeta de instalación** para especificar la carpeta del sistema de archivos en la que desea instalar los paquetes y sus dependencias.  
  
#### <a name="options"></a>Opciones  
 **Carpeta**  
 Permite especificar la ruta y la carpeta en la que se desea copiar el paquete y sus dependencias.  
  
 **Examinar**  
 Permite ir a la carpeta de destino mediante el cuadro de diálogo **Buscar carpeta** .  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
### <a name="specify-target-sql-server-page"></a>Página Especificar el SQL Server de destino  
 Use la página **Especificar el SQL Server de destino** para especificar las opciones de implementación del paquete en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="options"></a>Opciones  
 **Nombre del servidor**  
 Especifique el nombre del servidor en el que se implementarán los paquetes.  
  
 **Utilizar autenticación de Windows**  
 Permite especificar si se usará la autenticación de Windows al iniciar una sesión en el servidor. Para obtener una mayor seguridad, es recomendable utilizar la autenticación de Windows.  
  
 **Utilizar autenticación de SQL Server**  
 Permite especificar si el paquete debe usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al iniciar una sesión en el servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario.  
  
 **Contraseña**  
 Especifique una contraseña.  
  
 **Ruta de acceso del paquete**  
 Especifique el nombre de la carpeta lógica o escribe "/" para la carpeta predeterminada.  
  
 Para seleccionar la carpeta en el cuadro de diálogo **Paquete SSIS** , haga clic en el botón para examinar (…). Sin embargo, el cuadro de diálogo no proporciona medios para seleccionar la carpeta predeterminada. Si desea utilizar la carpeta predeterminada, tiene que escribir "/" en el cuadro de texto.  
  
> [!NOTE]  
>  Si no escribe una ruta de acceso del paquete válida, aparece el mensaje de error siguiente: "Uno o más argumentos no son válidos."  
  
 **Basar el cifrado en el almacenamiento del servidor**  
 Seleccione estas características de seguridad del [!INCLUDE[ssDE](../../includes/ssde-md.md)] para contribuir a proteger los paquetes.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
### <a name="finish-the-package-installation-page"></a>Página Salir del Asistente para la instalación de paquetes  
 Use la página **Salir del Asistente para la instalación de paquetes** para ver un resumen de los resultados de la instalación del paquete. Esta página muestra información, como el nombre del proyecto implementado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , los paquetes instalados, los archivos de configuración y la ubicación de la instalación.  
  
 **Finalizar**  
 Para salir del asistente, haga clic en **Finalizar**.  



---
title: Configuraciones de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package configuration syntax [Integration Services]
- SQL Server Integration Services packages, configurations
- SSIS packages, configurations
- XML [Integration Services]
- Integration Services packages, configurations
- configuration syntax [Integration Services]
- indirect configurations [Integration Services]
- configurations [Integration Services]
- direct configurations [Integration Services]
- packages [Integration Services], configurations
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c220fc87f726d8ba3d8e8cc92904ce42e3baeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056891"
---
# <a name="package-configurations"></a>Configuraciones de paquetes
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona configuraciones de paquetes que se pueden usar para actualizar los valores de las propiedades en tiempo de ejecución.  
  
> [!NOTE]  
>  Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Una configuración es una par propiedad/valor que se agrega a un paquete completo. Normalmente, se crean las propiedades establecidas de un paquete para los objetos del paquete durante el desarrollo y, después, se agrega la configuración al paquete. Cuando se ejecuta el paquete, éste recibe de la configuración los nuevos valores de la propiedad. Por ejemplo, al utilizar una configuración, se puede modificar la cadena de conexión de un administrador de conexiones o actualizar el valor de una variable.  
  
 Las configuraciones de paquetes ofrecen las siguientes ventajas:  
  
-   Permiten mover más fácilmente los paquetes de un entorno de desarrollo a un entorno de producción. Por ejemplo, una configuración puede actualizar la ruta de acceso de un archivo de origen, o bien cambiar el nombre de una base de datos o servidor.  
  
-   Son útiles para implementar paquetes en varios servidores distintos. Por ejemplo, una variable en la configuración de cada paquete implementado puede contener un valor de espacio de disco distinto, y si el espacio de disco disponible es menor que dicho valor, el paquete no se ejecuta.  
  
-   Aumentan la flexibilidad de los paquetes. Por ejemplo, una configuración puede actualizar el valor de una variable que se utiliza en una expresión de propiedad.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] admite varios métodos distintos para almacenar configuraciones de paquetes, como archivos XML, tablas de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y variables de entorno y de paquete.  
  
 Cada configuración es una pareja propiedad/valor. El archivo de configuración XML y los tipos de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pueden incluir varias configuraciones.  
  
 Las configuraciones se incluyen al crear una utilidad de implementación de paquetes para instalar paquetes. Al instalar los paquetes, las configuraciones se pueden actualizar como un paso en la instalación del paquete.  
  
## <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>Cómo se aplican las configuraciones de paquetes en tiempo de ejecución  
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
  
 Para obtener más información sobre estas opciones y cómo difiere el comportamiento de estas opciones entre [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] y versiones anteriores, vea [cambios de comportamiento en las características de Integration Services en SQL Server 2014](../../2014/integration-services/behavior-changes-to-integration-services-features-in-sql-server-2014.md).  
  
## <a name="package-configuration-types"></a>Tipos de configuraciones de paquetes  
 En la tabla siguiente se describen los tipos de configuraciones de paquetes.  
  
|Tipo|Descripción|  
|----------|-----------------|  
|Archivo de configuración XML|Un archivo XML contiene las configuraciones. El archivo XML puede incluir varias configuraciones.|  
|Variable de entorno|Una variable de entorno contiene la configuración.|  
|Entrada del Registro|Una entrada del Registro contiene la configuración.|  
|Variable de paquete primario|Una variable del paquete contiene la configuración. Este tipo de configuración se utiliza habitualmente para actualizar las propiedades de los paquetes secundarios.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] table|Una tabla de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contiene la configuración. La tabla puede incluir varias configuraciones.|  
  
### <a name="xml-configuration-files"></a>Archivos de configuración XML  
 Si selecciona el tipo de configuración **Archivo de configuración XML** , puede crear un archivo de configuración, reutilizar un archivo existente y agregarle configuraciones nuevas, o bien reutilizar un archivo existente sobrescribiendo el contenido actual.  
  
 Un archivo de configuración XML tiene dos secciones:  
  
-   Un encabezado que contiene información acerca del archivo de configuración. Este elemento incluye atributos como por ejemplo, cuándo se creó el archivo y el nombre de la persona que lo generó.  
  
-   Elementos de configuración que contienen información acerca de cada configuración. Este elemento incluye atributos como la ruta de acceso de la propiedad y el valor configurado de una propiedad.  
  
 El siguiente código XML muestra la sintaxis de un archivo de configuración XML. En este ejemplo se muestra una configuración para la propiedad Value de una variable entera llamada `MyVar`.  
  
```  
<?xml version="1.0"?>  
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
  
### <a name="registry-entry"></a>Entrada del Registro  
 Si desea usar una entrada del Registro para guardar la configuración, puede usar una clave existente o crear otra en HKEY_CURRENT_USER. La clave del Registro que utilice debe tener un valor denominado `Value`. El valor puede ser un valor de tipo DWORD o una cadena.  
  
 Si selecciona el tipo de configuración **Entrada del Registro** , debe escribir el nombre de la clave del Registro en el cuadro de texto del Registro. El formato es \<clave del Registro>. Si quiere usar una clave del Registro que no está en la raíz de HKEY_CURRENT_USER, use el formato \<clave del Registro\clave del Registro\\...> para identificarla. Por ejemplo, para usar la clave MyPackage de SSISPackages, escriba `SSISPackages\MyPackage`.  
  
### <a name="sql-server"></a>SQL Server  
 Si selecciona el tipo de configuración **SQL Server** , debe especificar la conexión a la base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que desee almacenar las configuraciones. Puede guardar las configuraciones en una tabla existente o crear una tabla nueva en la base de datos especificada.  
  
 La siguiente instrucción SQL muestra la instrucción CREATE TABLE predeterminada que proporciona el Asistente para la configuración de paquetes.  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 El nombre que asigna a la configuración es el valor que se almacena en la columna **ConfigurationFilter** .  
  
## <a name="direct-and-indirect-configurations"></a>Configuraciones directas e indirectas  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona configuraciones directas e indirectas. Si especifica las configuraciones directamente, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] crea un vínculo directo entre el elemento de configuración y la propiedad del objeto de paquete. Las configuraciones directas son una opción mejor cuando la ubicación del origen no cambia. Por ejemplo, si está seguro de que todas las implementaciones del paquete utilizarán la misma ruta de acceso al archivo, puede especificar un archivo de configuración XML.  
  
 Las configuraciones indirectas utilizan variables de entorno. En lugar de especificar el entorno de configuración directamente, la configuración apunta a una variable de entorno, que a su vez contiene el valor de configuración. Las configuraciones indirectas son una opción mejor cuando la ubicación de la configuración puede cambiar en cada implementación de un paquete.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico con una [introducción a las configuraciones de paquetes de Integration Services](https://go.microsoft.com/fwlink/?LinkId=165643), en msdn.microsoft.com  
  
-   Entrada de blog, [crear paquetes de código: configuraciones de paquetes](https://go.microsoft.com/fwlink/?LinkId=217663), en www.sqlis.com.  
  
-   Entrada de blog, [ejemplo de API: agregar mediante programación un archivo de configuración a un paquete](https://go.microsoft.com/fwlink/?LinkId=217664), en blogs.msdn.com.  
  
  

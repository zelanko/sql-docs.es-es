---
title: Referencia de la interfaz de usuario del Asistente para configuración de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.configwizard.selectobjects.f1
- sql12.dts.configwizard.selecconfigtype.f1
- sql12.dts.configwizard.finishdtsconfiguration.f1
- sql12.dts.configwizard.welcome.f1
ms.assetid: adca6938-6d5a-40ec-950e-dceb79d044fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70576676604340a3239d4903d895f1dd385882d6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424052"
---
# <a name="package-configuration-wizard-ui-reference"></a>Referencia de la interfaz de usuario del Asistente para la configuración de paquetes
  Use el **Asistente para la configuración de paquetes** para crear configuraciones que actualizan las propiedades de un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y sus objetos en tiempo de ejecución. Este asistente se ejecuta al agregar una nueva configuración o modificar una existente en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Para abrir el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Configuraciones de paquetes** en el menú **SSIS** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md).  
  
> [!NOTE]  
>  Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 En las siguientes secciones se describen las páginas del asistente.  
  
## <a name="welcome-to-the-package-configuration-wizard-page"></a>Asistente para la configuración de paquetes (página principal)  
 Use el **Asistente para la configuración de SSIS** para crear configuraciones que actualizan las propiedades de un paquete y sus objetos en tiempo de ejecución.  
  
### <a name="options"></a>Opciones  
 **No volver a mostrar esta página**  
 Omite la página de bienvenida la próxima vez que abre el asistente.  
  
 **Siguiente**  
 Avanza a la página siguiente del asistente.  
  
## <a name="select-configuration-type-page"></a>Página Seleccionar tipo de configuración  
 Use la página **Seleccionar tipo de configuración** para especificar el tipo de configuración que se creará.  
  
 Si necesita obtener información adicional para determinar el tipo de configuración que debe utilizar, vea [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Tipo de configuración**  
 Seleccione el tipo de origen en el que se almacenará la configuración, utilizando las siguientes opciones:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Archivo de configuración XML**|Almacenar la configuración como un archivo XML. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Variable del entorno**|Almacenar la configuración en una de las variables de entorno. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Entrada del registro**|Almacenar la configuración en el Registro. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**Variable de paquete primario**|Almacenar la configuración como una variable en el paquete que contiene la tarea.  Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
|**SQL Server**|Almacenar la configuración en una tabla en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Al seleccionar este valor se muestran las opciones dinámicas de la sección **Tipo de configuración**.|  
  
 **Siguiente**  
 Muestra la siguiente página en la secuencia del asistente.  
  
### <a name="dynamic-options"></a>Opciones dinámicas  
  
#### <a name="configuration-type-option--xml-configuration-file"></a>Opción de tipo de configuración = Archivo de configuración XML  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Nombre del archivo de configuración**|Escriba la ruta de acceso del archivo de configuración que genera el asistente.|  
|**Examinar**|Use el cuadro de diálogo **Seleccionar ubicación del archivo de configuración** para especificar la ruta de acceso del archivo de configuración que genera el asistente. Si el archivo no existe, el asistente lo crea.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se usa para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable del entorno**|Seleccione una variable de entorno de la lista.|  
  
#### <a name="configuration-type-option--environment-variable"></a>Opción de tipo de configuración = Variable de entorno  
 **Variable del entorno**  
 Seleccione la variable de entorno que contiene la información de configuración.  
  
#### <a name="configuration-type-option--registry-entry"></a>Opción de tipo de configuración = Entrada del Registro  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada del registro**|Escriba la clave del Registro que contiene la información de configuración. El formato es \<registry key>.<br /><br /> La clave del Registro ya debe existir en HKEY_CURRENT_USER y tener un valor con el nombre Value. El valor puede ser un valor de tipo DWORD o una cadena.<br /><br /> Si desea usar una clave del registro que no está en la raíz de HKEY_CURRENT_USER, use el formato \<Registry key\registry key\\...> para identificar la clave.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se utiliza para especificar la variable de entorno donde debe almacenarse la configuración.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable del entorno**|Seleccione una variable de entorno de la lista.|  
  
#### <a name="configuration-type-option--parent-package-variable"></a>Opción de tipo de configuración = Variable de paquete primario  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable primaria**|Especifique la variable del paquete primario que contiene la información de configuración.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se usa para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable del entorno**|Seleccione una variable de entorno de la lista.|  
  
#### <a name="configuration-type-options--sql-server"></a>Opción de tipo de configuración = SQL Server  
 **Especificar valores de configuración directamente**  
 Se utiliza para especificar la configuración directamente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Connection**|Seleccione una conexión de la lista o haga clic en **Nueva** para crear una nueva conexión.|  
|**Tabla de configuración**|Seleccione una tabla existente o haga clic en **Nueva** para escribir una instrucción SQL que cree la nueva tabla.|  
|**Filtro de la configuración**|Seleccione un nombre de configuración existente o escriba uno nuevo.<br /><br /> Muchas de las configuraciones de SQL Server se pueden almacenar en la misma tabla, y cada configuración puede incluir varios elementos de configuración.<br /><br /> Este valor definido por el usuario se almacena en la tabla para identificar los elementos de configuración de una configuración determinada.|  
  
 **La ubicación de configuración se almacena en una variable de entorno**  
 Se utiliza para especificar la variable de entorno donde se almacena la configuración.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable del entorno**|Seleccione una variable de entorno de la lista.|  
  
## <a name="select-objects-to-export-page"></a>Página Seleccionar objetos para la exportación  
 Use la página **Seleccionar propiedad de destino o Seleccionar propiedades para la exportación** para especificar las propiedades de objetos contenidas en la configuración. La posibilidad de seleccionar varias propiedades solo está disponible si se selecciona el tipo de configuración XML.  
  
### <a name="options"></a>Opciones  
 **Objects**  
 Expanda la jerarquía de paquetes y seleccione las propiedades que desea exportar.  
  
 **Atributos de propiedad**  
 Permite ver los atributos de una propiedad.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
## <a name="completing-the-wizard-page"></a>Página Finalización del asistente  
 Utilice la página **Finalización del asistente** para asignar un nombre a la configuración y ver los valores utilizados por el asistente para crear la configuración. Una vez que finaliza el asistente, se muestra el **Organizador de configuraciones de paquetes** , que enumera todas las configuraciones para el paquete.  
  
### <a name="options"></a>Opciones  
 **Nombre de la configuración**  
 Escriba el nombre de la configuración.  
  
 **Versión preliminar**  
 Muestra los valores utilizados por el asistente para crear la configuración.  
  
 **Finalizar**  
 Crea la configuración y sale del **Asistente para configuración de paquetes**.  
  
## <a name="see-also"></a>Consulte también  
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)  
  
  

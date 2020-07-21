---
title: Parámetros de paquete y proyecto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.parameterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c773ae8db0b9942e23e40fb5f72b989b97ccfcc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "77903862"
---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Paquete de Integration Services (SSIS) y parámetros del proyecto

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Los parámetros de[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) permiten asignar valores a las propiedades de los paquetes en el momento de la ejecución de los mismos. Puede crear *parámetros de proyecto* en el nivel de proyecto y *parámetros de paquete* en el nivel de paquete. Los parámetros de proyecto se usan para proporcionar cualquier entrada externa que el proyecto recibe a uno o más paquetes del proyecto. Los parámetros de paquete permiten modificar la ejecución del paquete sin tener que modificarlo ni volver a implementarlo.  
  
 En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] puede crear, modificar o eliminar parámetros del proyecto en la ventana **Project.params** . Para crear, modificar y eliminar los parámetros de paquetes, use la pestaña **Parámetros** en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Puede asociar un parámetro nuevo o existente a una propiedad de tarea con el cuadro de diálogo **Parametrizar** . Para obtener más información sobre cómo usar la ventana **Project.params** y las pestaña **Parámetros** , vea [Create Parameters](https://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99). Para obtener más información acerca del cuadro de diálogo **Parametrizar** , vea [Parameterize Dialog Box](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  
  
## <a name="parameters-and-package-deployment-model"></a>Parámetros y modelo de implementación de paquetes  
 En general, si implementa un paquete con el modelo de implementación de paquetes, debe utilizar configuraciones en lugar de parámetros.  
  
 Al implementar un paquete que contenga parámetros utilizando el modelo de implementación de paquetes y después ejecutar el paquete, los parámetros no se llaman durante la ejecución. Si el paquete contiene parámetros de paquetes y las expresiones dentro del paquete utilizan los parámetros, los valores resultantes se aplican en tiempo de ejecución. Si el paquete contiene parámetros de proyecto, la ejecución del paquete puede producir un error.  
  
## <a name="parameters-and-project-deployment-model"></a>Modelo de implementación de proyectos y paquetes  
 Al implementar un proyecto en el servidor de Integration Services (SSIS), use las vistas, los procedimientos almacenados y la interfaz de usuario de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrar los parámetros de proyectos y paquetes. Para obtener más información, vea los siguientes temas.  
  
-   [Views &#40;Integration Services Catalog&#41;](../integration-services/system-views/views-integration-services-catalog.md) (Vistas [catálogo de Integration Services])  
  
-   [Stored Procedures &#40;Integration Services Catalog&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md) (Procedimientos almacenados [catálogo de Integration Services])  
  
-   [Cuadro de diálogo Configurar](../integration-services/service/configure-dialog-box.md)  
  
-   [Ejecutar paquete (cuadro de diálogo)](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>Valores de parámetros  
 Puede asignar hasta tres tipos de valores para un parámetro. Cuando se inicia la ejecución del paquete, se utiliza un único valor para el parámetro y el parámetro se resuelve en un valor literal final.  
  
 La tabla siguiente enumera los tipos de valores.  
  
|Nombre del valor|Descripción|Tipo del valor|  
|----------------|-----------------|-------------------|  
|Valor de ejecución|El valor asignado a una instancia específica de la ejecución del paquete. Esta asignación invalida todos los demás valores, pero solo se aplica a una única instancia de ejecución del paquete.|Literal|  
|Valor de servidor|El valor asignado al parámetro dentro del ámbito del proyecto, una vez que el proyecto se implementa en el servidor de Integration Services. Este valor invalida el valor predeterminado de diseño.|Literal o referencia de variable de entorno|  
|Valor de diseño|El valor asignado al parámetro cuando el proyecto se crea o modifica en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Este valor se mantiene con el proyecto.|Literal|  
  
 Puede utilizar un único parámetro para asignar un valor a varias propiedades del paquete. A una propiedad del paquete se le puede asignar un valor solo de un único parámetro.  
  
###  <a name="executions-and-parameter-values"></a><a name="executions"></a> Ejecuciones y valores de parámetros  
 La *ejecución* es un objeto que representa una sola instancia de ejecución del paquete. Cuando se crea una ejecución, debe especificar todos los detalles para ejecutar un paquete como los valores de los parámetros de ejecución. También puede modificar los valores de parámetros para las ejecuciones existentes.  
  
 Cuando se establece explícitamente un valor de parámetro de ejecución, el valor solo es aplicable a esa instancia de ejecución concreta. El valor de ejecución se utiliza en lugar de un valor de servidor o de un valor de diseño. Si no establece explícitamente un valor de ejecución y se ha especificado un valor de servidor, se utiliza el valor del servidor.  
  
 Si un parámetro se marca como sea necesario, se debe especificar el valor de servidor o el valor de ejecución para ese parámetro. De lo contrario, el paquete correspondiente no se ejecuta. Aunque el parámetro tenga un valor predeterminado en tiempo de diseño, nunca se usará una vez que se implemente el proyecto.  
  
#### <a name="environment-variables"></a>Variables de entorno  
 Si un parámetro hace referencia a una variable de entorno, el valor literal de esa variable se resuelve mediante la referencia de entorno especificada y se aplica al parámetro. El valor del parámetro literal final que se utiliza para la ejecución del paquete se conoce como valor de parámetro de ejecución. Especifica la referencia de entorno para una ejecución mediante el cuadro de diálogo **Ejecutar**  
  
 Si un parámetro de proyecto hace referencia a una variable de entorno y el valor literal de la variable no puede resolverse en la ejecución, se utiliza el valor de diseño. El valor del servidor no se utiliza.  
  
 Para ver las variables de entorno que se asignan a los valores de parámetro, consulte la vista catalog.object_parameters. Para más información, vea [catalog.object_parameters &#40;SSISDB Database&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (catalog.object_parameters [base de datos de SSISDB]).  
  
#### <a name="determining-execution-parameter-values"></a>Determinar los valores de parámetros de ejecución  
 Pueden utilizarse las vistas y el procedimiento almacenado siguientes de Transact-SQL para mostrar y establecer los valores de parámetro.  
  
 [catalog.execution_parameter_values &#40;SSISDB Database&#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) (catalog.execution_parameter_values [base de datos de SSISDB]) (vista)  
 Muestra los valores de parámetros reales que serán utilizados por una ejecución concreta  
  
 [catalog.get_parameter_values &#40;SSISDB Database&#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (catalog.get_parameter_values [base de datos de SSISDB]) (procedimiento almacenado)  
 Resuelve y muestra los valores reales del paquete y la referencia de entorno especificados  
  
 [catalog.object_parameters &#40;SSISDB Database&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (catalog.object_parameters [base de datos de SSISDB]) (vista)  
 Muestra los parámetros y las propiedades de todos los paquetes y proyectos en el catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , incluidos los valores predeterminados de servidor y de diseño.  
  
 [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) (catalog.set_execution_parameter_value [base de datos de SSISDB];)  
 Establece el valor de un parámetro para una instancia de ejecución en el catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 También puede utilizar el cuadro de diálogo **Ejecutar paquete** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para modificar el valor de parámetro. Para obtener más información, vea [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog).  
  
 También puede utilizar la opción de **/Parameter** dtexec para modificar un valor de parámetro. Para obtener más información, consulte [utilidad dtexec](../integration-services/packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Validación de parámetros  
 Si los valores de parámetros no se pueden resolver, la ejecución del paquete correspondiente generará un error. Para ayudar a evitar errores, puede validar los proyectos y los paquetes mediante el cuadro de diálogo **Validar** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. La validación permite confirmar que todos los parámetros tienen los valores necesarios o pueden resolver los valores necesarios con referencias de entorno específicas. La validación comprueba también otros problemas comunes del paquete.  
  
 Para obtener más información, vea [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Ejemplo de parámetro  
 En este ejemplo se describe un parámetro denominado **pkgOptions** que se utiliza para especificar opciones para el paquete en que reside.  
  
 En tiempo de diseño, cuando el parámetro se creó en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], se asignó al parámetro el valor predeterminado 1. Este valor predeterminado se conoce como valor predeterminado de diseño. Si el proyecto se implementó en el catálogo de SSISDB y no se asignaron otros valores a este parámetro, se asignará a la propiedad del paquete correspondiente al parámetro **pkgOptions** el valor 1 durante la ejecución del paquete. El valor predeterminado de diseño se mantiene con el proyecto en su ciclo de vida.  
  
 En la preparación de una instancia específica de la ejecución del paquete, se asigna el valor 5 al parámetro **pkgOptions** . Este valor se conoce como valor de ejecución porque se aplica al parámetro solo para esa instancia concreta de ejecución. Cuando se inicia la ejecución, se asigna el valor 5 a la propiedad del paquete correspondiente al parámetro **pkgOptions** .  
  
## <a name="create-parameters"></a>Creación de parámetros
Puede usar [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear parámetros de proyecto y parámetros de paquete. Los procedimientos siguientes proporcionan instrucciones paso a paso para crear parámetros de paquete o proyecto.  
  
> **NOTA:** Si va a convertir un proyecto que creó con una versión anterior de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al modelo de implementación de proyectos, puede usar el **Asistente para conversión de proyectos de Integration Services** con el fin de crear parámetros de acuerdo con las configuraciones. Para obtener más información, consulte [Deploy Integration Services (SSIS) Projects and Packages](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md) (Implementación de proyectos y paquetes de Integration Services [SSIS]).  
  
### <a name="create-package-parameters"></a>Creación de parámetros del paquete  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]y después haga clic en la pestaña **Parámetros** del Diseñador SSIS.  
  
     ![Pestaña Parámetros de paquete](../integration-services/media/denali-package-parameters.gif "Pestaña Parámetros de paquete")  
  
2.  Haga clic en el botón **Agregar parámetro** de la barra de herramientas.  
  
     ![Agregar botón de la barra de herramientas](../integration-services/media/denali-parameter-add.gif "Agregar botón de la barra de herramientas")  
  
3.  Escriba valores para las propiedades **Nombre**, **Tipo de datos**, **Valor**, **Con distinción**y **Obligatorio** en la propia lista o en la ventana **Propiedades** . Estas propiedades se describen en la tabla siguiente.  
  
    |Propiedad|Descripción|  
    |--------------|-----------------|  
    |Nombre|El nombre del parámetro.|  
    |Tipo de datos|El tipo de datos del parámetro.|  
    |Valor predeterminado|Valor predeterminado para el parámetro asignado en tiempo de diseño. También se conoce como valor predeterminado de diseño.|  
    |Sensible|Los valores de parámetros con distinción se cifran en el catálogo y aparecen como valor NULL cuando se ven con Transact-SQL o SQL Server Management Studio.|  
    |Obligatorio|Requiere que un valor, distinto del valor predeterminado de diseño, se especifique antes de que el paquete se ejecute.|  
    |Descripción|Descripción del parámetro en cuanto a capacidad de mantenimiento. En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], establezca la descripción del parámetro en la ventana Propiedades de Visual Studio cuando el parámetro esté seleccionado en la ventana de parámetros aplicable.|  
  
    > **NOTA:** Cuando se implementa un proyecto en el catálogo, algunas propiedades más se asocian al proyecto. Para ver todas las propiedades de todos los parámetros del catálogo, use la vista [catalog.object_parameters &#40;base de datos de SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
4.  Guarde el proyecto para guardar los cambios realizados en los parámetros. Los valores de parámetro se almacenan en el archivo de proyecto.  
  
    > **¡ADVERTENCIA!** Puede realizar modificaciones en contexto en la lista o utilizar la ventana **Propiedades** para modificar los valores de las propiedades de parámetro. Puede eliminar un parámetro con el botón de la barra de herramientas **Eliminar (x)** . Con el último botón de la barra de herramientas, puede especificar un valor para un parámetro que se utilice solo cuando se ejecute el paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
    > **NOTA:** Si abre de nuevo el archivo del paquete sin abrir el proyecto en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], la pestaña **Parámetros** estará vacía y deshabilitada.  
  
### <a name="create-project-parameters"></a>Creación de los parámetros del proyecto  
  
1.  Abra el proyecto en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en **Project.params** y, a continuación, haga clic en **Abrir** , o haga doble clic en **Project.params** para abrirlo.  
  
     ![Ventana Parámetros del proyecto](../integration-services/media/denali-project-parameters.gif "Ventana Parámetros del proyecto")  
  
3.  Haga clic en el botón **Agregar parámetro** de la barra de herramientas.  
  
     ![Agregar botón de la barra de herramientas](../integration-services/media/denali-parameter-add.gif "Agregar botón de la barra de herramientas")  
  
4.  Escriba valores para las propiedades **Nombre**, **Tipo de datos**, **Valor**, **Con distinción**y **Obligatorio** .  
  
    |Propiedad|Descripción|  
    |--------------|-----------------|  
    |Nombre|El nombre del parámetro.|  
    |Tipo de datos|El tipo de datos del parámetro.|  
    |Valor predeterminado|Valor predeterminado para el parámetro asignado en tiempo de diseño. También se conoce como valor predeterminado de diseño.|  
    |Sensible|Los valores de parámetros con distinción se cifran en el catálogo y aparecen como valor NULL cuando se ven con Transact-SQL o SQL Server Management Studio.|  
    |Obligatorio|Requiere que un valor, distinto del valor predeterminado de diseño, se especifique antes de que el paquete se ejecute.|  
    |Descripción|Descripción del parámetro en cuanto a capacidad de mantenimiento. En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], establezca la descripción del parámetro en la ventana Propiedades de Visual Studio cuando el parámetro esté seleccionado en la ventana de parámetros aplicable.|  
  
5.  Guarde el proyecto para guardar los cambios realizados en los parámetros. Los valores de parámetro se almacenan en configuraciones en el archivo de proyecto. Guarde el archivo de proyecto para confirmar en el disco los cambios en los valores de parámetro.  
  
    > **¡ADVERTENCIA!** Puede realizar modificaciones en contexto en la lista o utilizar la ventana **Propiedades** para modificar los valores de las propiedades de parámetro. Puede eliminar un parámetro con el botón de la barra de herramientas **Eliminar (x)** . Con el último botón de la barra de herramientas que es para abrir el cuadro de diálogo **Administrar valores de parámetro** , puede especificar un valor para un parámetro que se use solamente cuando se ejecuta el paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
El cuadro de diálogo **Parametrizar** permite asociar un parámetro nuevo o existente con una propiedad de una tarea. Abra el cuadro de diálogo haciendo clic con el botón secundario en una tarea o en la pestaña Flujo de control en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y haciendo clic en **Parametrizar**. La siguiente lista describe los elementos de la interfaz de usuario en el cuadro de diálogo. Para más información sobre los parámetros, consulte [Parámetros de Integration Services (SSIS)](https://msdn.microsoft.com/library/hh213214.aspx).
  
### <a name="options"></a>Opciones  
 **Propiedad**  
 Seleccione la propiedad de la tarea que desea asociar con un parámetro. Esta lista se rellena con todas las propiedades que se pueden utilizar con parámetros.  
  
 **Usar parámetro existente**  
 Seleccione esta opción para asociar la propiedad de tarea con un parámetro existente y, a continuación, seleccione el parámetro de la lista desplegable.  
  
 **No usar el parámetro**  
 Seleccione esta opción para quitar una referencia a un parámetro. Parámetro no se elimina.  
  
 **Crear nuevo parámetro**  
 Seleccione esta opción para crear un nuevo parámetro que desee asociar con la propiedad de tarea.  
  
 **Nombre**  
 Especifique el nombre del parámetro que desea crear.  
  
 **Descripción**  
 Especifique la descripción del parámetro.  
  
 **Valor**  
 Especifique el valor predeterminado del parámetro. Se conoce también como valor predeterminado de diseño, el cual se puede invalidar más adelante durante la fase de implementación.  
  
 **Ámbito**  
 Especifique el ámbito del parámetro seleccionando la opción **Proyecto** o **Paquete** . Los parámetros de proyecto se usan para proporcionar cualquier entrada externa que el proyecto recibe a uno o más paquetes del proyecto. Los parámetros de paquete permiten modificar la ejecución del paquete sin tener que modificarlo ni volver a implementarlo.  
  
 **Con distinción**  
 Especifique si es un parámetro con distinción activando o desactivando la casilla. Los valores de parámetros con distinción se cifran en el catálogo y aparecen como valor NULL cuando se ven con Transact-SQL o SQL Server Management Studio.  
  
 **Obligatorio**  
 Especifique si el parámetro requiere que se especifique un valor, distinto del valor predeterminado de diseño, antes de que el paquete se ejecute.  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>Establecimiento de valores de parámetro después de la implementación del proyecto
El Asistente para la implementación permite establecer valores de parámetro predeterminados del servidor al implementar el proyecto en el catálogo. Después de que el proyecto esté en el catálogo, puede utilizar el Explorador de objetos de SQL Server Management Studio (SSMS) o Transact-SQL para establecer valores predeterminados del servidor.  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>Establecimiento de valores predeterminados del servidor con el Explorador de objetos de SSMS  
  
1.  Seleccione y haga clic con el botón derecho en el proyecto debajo del nodo **Integration Services**.  
  
2.  Haga clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades del proyecto** .  
  
3.  Abra la página de parámetros haciendo clic en **Parámetros** debajo de **Seleccionar una página**.  
  
4.  Seleccione el parámetro deseado en la lista **Parámetros** . Nota: la columna **Contenedor** ayuda a distinguir los parámetros del proyecto de los parámetros del paquete.  
  
5.  En la columna de **Valor** , especifique el valor del parámetro predeterminado del servidor deseado.  

### <a name="set-server-defaults-with-transact-sql"></a>Establecimiento de valores predeterminados del servidor con Transact-SQL  
 Para establecer valores predeterminados del servidor con Transact-SQL, use el procedimiento almacenado de [catalog.set_object_parameter_value &#40;base de datos de SSISDB&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md). Para ver los valores predeterminados actuales del servidor, consulte la vista [catalog.object_parameters &#40;base de datos de SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md). Para borrar un valor predeterminado del servidor, use el procedimiento almacenado [catalog.clear_object_parameter_value &#40;base de datos de SSISDB&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, [Sugerencia rápida de SSIS: parámetros necesarios](https://go.microsoft.com/fwlink/?LinkId=239781), en mattmasson.com.  
  
  

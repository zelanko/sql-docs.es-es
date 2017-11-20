---
title: Componente de script | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: e7b0923968137a76b68d0324223ffbb61e7443b9
ms.contentlocale: es-es
ms.lasthandoff: 08/19/2017

---
# <a name="script-component"></a>Componente de script
  El componente de script hospeda el script y permite a un paquete incluir y ejecutar código personalizado de script. Puede usar el componente de script en paquetes para los siguientes fines:  
  
-   Aplicar varias transformaciones a los datos en lugar de usar varias transformaciones en el flujo de datos. Por ejemplo, un script puede sumar los valores de dos columnas y luego calcular el promedio de la suma.  
  
-   Tener acceso a las reglas de negocios en un ensamblado .NET existente. Por ejemplo, un script puede aplicar una norma empresarial que especifica el intervalo de valores que son válidos en la columna **Income** .  
  
-   Usar fórmulas personalizadas y funciones, además de las funciones y operadores que proporciona la gramática de la expresión [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Por ejemplo, validar números de tarjeta de crédito mediante la fórmula LUHN.  
  
-   Validar datos de columna y omitir registros que contienen datos no válidos. Por ejemplo, un script puede evaluar si un valor de franqueo es razonable y omitir registros con valores extremadamente altos o bajos.  
  
 El componente de script proporciona una manera fácil y rápida de incluir funciones personalizadas en un flujo de datos. Sin embargo, si planea reutilizar el código de script en varios paquetes, quizás resulte más conveniente programar un componente personalizado en lugar de usar el componente de script. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
> [!NOTE]  
>  Si el componente de script contiene un script que intenta leer el valor de una columna que es NULL, se produce un error en el componente de script al ejecutar el paquete. Es recomendable que el script use el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> para determinar si la columna es NULL antes de intentar leer el valor de la columna.  
  
 El componente de script se puede usar como origen, transformación o destino. Este componente admite una entrada y varias salidas. Según la forma en que se usa el componente, admite una entrada o salidas, o ambas cosas. El script es invocado por cada fila en la entrada o la salida.  
  
-   Si se usa como origen, el componente de script admite varias salidas.  
  
-   Si se usa como transformación, el componente de script admite una entrada y varias salidas.  
  
-   Si se usa como destino, el componente de script admite una entrada.  
  
 El componente de script no admite salidas de error.  
  
 Una vez que haya decidido que el componente de script es la opción adecuada para su paquete, tiene que configurar las entradas y salidas, desarrollar el script que el componente utiliza y configurar el propio componente.  
  
## <a name="understanding-the-script-component-modes"></a>Descripción de los modos del componente de script  
 En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , el componente de script tiene dos modos: modo de diseño de metadatos y modo de diseño de código. En el modo de diseño de metadatos, se pueden agregar y modificar las entradas y salidas de componente de script, pero no se puede escribir código. Una vez configuradas todas las entradas y salidas, se cambia al modo de diseño de código para escribir el script. El componente de script genera automáticamente código base a partir de los metadatos de entradas y salidas. Si cambia los metadatos después de que el componente de script genere el código de base, es posible que su código ya no pueda compilarse porque el código base actualizado puede ser incompatible con su código.  
  
## <a name="writing-the-script-that-the-component-uses"></a>Escribir el script que el componente utiliza  
 El componente de script usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) como entorno para escribir los scripts. Puede tener acceso a VSTA en el **Editor de transformación Script**. Para obtener más información, vea [Editor de transformación Script &#40;página Script&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 El componente de script proporciona un proyecto de VSTA que incluye una clase autogenerada, llamada ScriptMain, que representa los metadatos del componente. Por ejemplo, si el componente de script se usa como una transformación que tiene tres salidas, ScriptMain incluye un método para cada salida. ScriptMain es el punto de entrada al script.  
  
 VSTA incluye todas las características estándar del entorno [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] , como el editor de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con códigos de color, IntelliSense y el Explorador de objetos. El script que usa el componente de script se almacena en la definición de paquete. Al diseñar el paquete, el código de script se escribe temporalmente en un archivo de proyecto.  
  
 VSTA es compatible con los lenguajes de programación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md). Para obtener información más específica acerca de cómo configurar el componente de script como origen, transformación o destino, vea [Developing Specific Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Para consultar ejemplos adicionales, como un destino ODBC, que ilustran el uso del componente de script, vea [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan en [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] y versiones posteriores. Al precompilar el script, no se carga el motor del lenguaje en tiempo de ejecución, por lo que el paquete se ejecuta con mayor rapidez. Sin embargo, los archivos binarios precompilados utilizan una cantidad considerable de espacio en disco.  
  
## <a name="configuring-the-script-component"></a>Configurar el componente de script  
 Puede configurar el componente de script de las maneras siguientes:  
  
-   Seleccionar las columnas de entrada a las que hacer referencia.  
  
    > [!NOTE]  
    >  Puede configurar solo una entrada al usar el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
-   Proporcionar el script que ejecuta el componente.  
  
-   Especificar el lenguaje de script.  
  
-   Proporcionar listas separadas por comas de variables de solo lectura y de lectura/escritura.  
  
-   Agregue más salidas, así como columnas de salida en las que el script realiza asignaciones.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>Configurar el componente de script en el Diseñador  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Configurar el componente de script mediante programación  
 Para obtener más información sobre las propiedades que se pueden establecer en la ventana **Propiedades** o mediante programación, haga clic en uno de los siguientes temas:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>Seleccionar el tipo de componente de script
  Use el cuadro de diálogo **Seleccionar el tipo de componente de script** para especificar si se creará una transformación Script que está configurada previamente para utilizarse como origen, transformación o destino.  
  
 Para obtener más información sobre el componente de Script, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opciones  
 La selección de **Origen**, **Destino**o **Transformación** afecta a la configuración de la transformación Script y a las páginas del Editor de transformación Script.  
  
## <a name="script-transformation-editor-connection-managers-page"></a>Editor de transformación Script (página Administradores de conexión)
  Use la página **Administradores de conexión** del **Editor de transformación Script** para seleccionar las conexiones que usará el script.  
  
 Para obtener más información sobre el componente de Script, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opciones  
 **Connection managers**  
 Vea la lista de conexiones disponibles para el uso del script.  
  
 **Nombre**  
 Escriba un nombre único y descriptivo para la conexión.  
  
 **Connection Manager**  
 Seleccione en la lista de administradores de conexiones disponibles o seleccione  **\<nueva conexión >** para abrir el **Agregar administrador de conexiones SSIS** cuadro de diálogo.  
  
 **Description**  
 Escriba la descripción de la conexión.  
  
 **Agregar**  
 Agregue otra conexión a la lista **Administradores de conexiones** .  
  
 **Quitar**  
 Quite la conexión seleccionada de la lista **Administradores de conexiones** .  
  
## <a name="script-transformation-editor-input-columns-page"></a>Editor de transformación Script (página Columnas de entrada)
  Utilice la página **Columnas de entrada** del cuadro de diálogo **Editor de transformación Script** para definir las propiedades de las columnas de entrada.  
  
> [!NOTE]  
>  La página **Columnas de entrada** no se muestra para los componentes de origen, que tienen salidas, pero no entradas.  
  
 Para obtener más información sobre el componente de Script, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opciones  
 **Nombre de entrada**  
 Seleccione las entradas disponibles de la lista.  
  
 **Columnas de entrada disponibles**  
 Mediante las casillas, indique las columnas que utilizarán la transformación de script.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles**.  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **Tipo de uso**  
 Especifique si la transformación Script tratará cada columna como **ReadOnly** o **ReadWrite**.  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>Editor de transformación Script (página Entradas y salidas)
  Use la página **Entradas y salidas** del cuadro de diálogo **Editor de transformación Script** para agregar, quitar y configurar las entradas y salidas de la transformación Script.  
  
> [!NOTE]  
>  Los componentes de origen tienen salidas y no tienen entradas, mientras que los componentes de destino tienen entradas y no tienen salidas. Las transformaciones tienen tanto entradas como salidas.  
  
 Para obtener más información sobre el componente de Script, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opciones  
 **Inputs and outputs**  
 Seleccione una entrada o salida de la izquierda para ver sus propiedades en la tabla de la derecha. Las propiedades disponibles para edición varían según la selección. Muchas de las propiedades mostradas son de solo lectura. Para obtener más información sobre las propiedades individuales, vea los temas siguientes.  
  
 [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **Agregar salida**  
 Se agrega una salida adicional a la lista.  
  
 **Agregar columna**  
 Seleccione la carpeta en la que quiere colocar la nueva columna de salida y haga clic en **Agregar columna**para agregar la columna.  
  
 **Quitar salida**  
 Seleccione una salida y, después, quítela al hacer clic en **Quitar salida**.  
  
 **Quitar columna**  
 Seleccione una columna y, después, quítela al hacer clic en **Quitar columna**.  
  
## <a name="script-transformation-editor-script-page"></a>Editor de transformación Script (página Script)
  Use la pestaña **Script** del cuadro de diálogo **Editor de transformación Script** para especificar un script y las propiedades relacionadas.  
  
 Para obtener más información sobre el componente de Script, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opciones  
 **Propiedades**  
 Vea y modifique las propiedades de la transformación de script. Muchas de las propiedades mostradas son de solo lectura. Puede modificar las siguientes propiedades:  
  
|Value|Description|  
|-----------|-----------------|  
|**Description**|Describe la transformación del script según su propósito.|  
|**LocaleID**|Especifica la configuración regional para proporcionar información específica de la región para ordenar y para la conversión de fecha y hora.|  
|**Nombre**|Escriba un nombre descriptivo para el componente.|  
|**ValidateExternalMetadata**|Indica si la transformación del script valida metadatos de columna con orígenes de datos externos en tiempo de diseño. El valor **false** retrasa la validación hasta el momento de la ejecución.|  
|**Variables de solo lectura**|Escriba una lista de variables separadas por comas (sin espacios) a la que la transformación del script tenga acceso de solo lectura.<br /><br /> Nota: Los nombres de variables distinguen entre mayúsculas y minúsculas.|  
|**Variables de lectura/escritura**|Escriba una lista de variables separadas por comas (sin espacios) a la que la transformación del script tenga acceso de lectura y escritura.<br /><br /> Nota: Los nombres de variables distinguen entre mayúsculas y minúsculas.|  
|**Lenguaje de script**|Seleccione el lenguaje de script que va a usar el componente de script.<br /><br /> Para establecer el lenguaje de script predeterminado para los componentes Script y las tareas de script, utilice la opción **Lenguaje de scripting** en la página **General** del cuadro de diálogo **Opciones** .|  
|**UserComponentTypeName**|Especifica la clase <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> y el ensamblado **Microsoft.SqlServer.TxScript** compatibles con la infraestructura de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 **Editar script**  
 Use [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) para crear o modificar un script.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  


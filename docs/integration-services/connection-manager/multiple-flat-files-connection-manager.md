---
title: Varios archivos planos, Administrador de conexiones | Documentos de Microsoft
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
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: f9069538cef2a85ed3e23e9ae3505a9fbfef01ae
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="multiple-flat-files-connection-manager"></a>administrador de conexiones de varios archivos planos
  Un administrador de conexiones de varios archivos planos permite a un paquete obtener acceso a datos de varios archivos planos. Por ejemplo, un origen de archivos planos puede utilizar un administrador de conexiones para varios archivos planos cuando la tarea Flujo de datos se encuentra en un contenedor de bucles, como el contenedor de bucles For. En cada bucle del contenedor, el origen de archivos planos carga los datos del siguiente nombre de archivo que proporciona el administrador de conexiones de varios archivos planos.  
  
 Cuando se agrega un administrador de conexiones de varios archivos planos a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve en una conexión de varios archivos planos en tiempo de ejecución, establece las propiedades del administrador de conexiones de varios archivos planos y agrega el administrador de conexiones de varios archivos planos a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MULTIFLATFILE**.  
  
 Puede configurar el administrador de conexiones de varios archivos planos de las maneras siguientes:  
  
-   Especificar los archivos, configuración regional y página de códigos que se debe usar. La configuración regional se usa para interpretar datos que dependen de la región, como las fechas, y la página de códigos se usa para convertir los datos de cadenas en Unicode.  
  
-   Especificar el formato de archivo. Se puede usar un ancho delimitado y fijo o un formato desigual a la derecha.  
  
-   Especificar delimitadores de filas de encabezados, de filas de datos y de columnas. Los delimitadores de columna se pueden establecer en el nivel de fila y se sobrescriben en el nivel de columna.  
  
-   Indicar si la primera fila de los archivos contiene nombres de columnas.  
  
-   Especificar un carácter calificador de texto. Cada columna se puede configurar para reconocer un calificador de texto.  
  
-   Establecer propiedades tales como el nombre, tipo de datos y ancho máximo de columnas individuales.  
  
 Si el administrador de conexiones de varios archivos planos hace referencia a varios archivos, las rutas de los archivos se separan con la barra vertical (|). La propiedad **ConnectionString** del administrador de conexiones tiene el formato siguiente:  
  
 \<*ruta de acceso*>|\<*ruta de acceso*>  
  
 También puede especificar varios archivos mediante caracteres comodín. Por ejemplo, para hacer referencia a todos los archivos de texto de la unidad C, el valor de la propiedad **ConnectionString** se puede establecer en C:\\*.txt.  
  
 Si un administrador de conexiones de varios archivos planos hace referencia a varios archivos, todos los archivos deben tener el mismo formato.  
  
 De forma predeterminada, el administrador de conexiones de varios archivos planos establece la longitud de las columnas de cadena en 50 caracteres. En el cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** , puede evaluar datos de muestra y automáticamente cambiar el tamaño de la longitud de esas columnas para evitar el truncamiento de datos o un ancho de columna excesivo. A menos que cambie el tamaño de la longitud de la columna en un origen de archivo plano o una transformación, la longitud de columna permanece invariable en todo el flujo de datos. Si estas columnas se asignan a columnas de destino más estrechas, aparecen mensajes de advertencia en la interfaz de usuario, y en tiempo de ejecución, se pueden generar errores debido al truncamiento de datos. Puede cambiar el tamaño de las columnas para que sean compatibles con las columnas de destino en el administrador de conexiones de archivos planos, el origen de archivo plano o una transformación. Para modificar la longitud de las columnas de salida, establezca la propiedad **Length** de la columna de salida en la pestaña **Propiedades de entrada y salida** del cuadro de diálogo **Editor avanzado** .  
  
 Si actualiza las longitudes de columna en el administrador de conexiones de varios archivos planos una vez que ya ha agregado y configurado el origen de archivo plano que utiliza el administrador de conexiones, no tiene que cambiar manualmente el tamaño de las columnas de salida en el origen de archivo plano. Cuando abre el cuadro de diálogo **Origen de archivo plano** , el origen de archivo plano proporciona una opción para sincronizar los metadatos de columna.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Configuración del administrador de conexiones de varios archivos planos  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor del administrador de conexiones de varios archivos planos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** para seleccionar un grupo de archivos que tengan el mismo formato de datos y para especificar su formato de datos. Una conexión de varios archivos planos permite que un paquete se conecte a un grupo de archivos de texto que tengan el mismo formato.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de varios archivos planos en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Nombres de archivos**  
 Escriba la ruta de acceso y los nombres de los archivos que se van a utilizar en la conexión de varios archivos planos. Puede especificar varios archivos mediante el uso de caracteres comodín, como en el ejemplo "C:\\*.txt", o mediante el uso del carácter de barra vertical (|) para separar varios nombres de archivo. Todos los archivos deben tener el mismo formato de datos.  
  
 **Examinar**  
 Busque los nombres de los archivos que se van a utilizar en la conexión de varios archivos planos. Puede seleccionar varios archivos. Todos los archivos deben tener el mismo formato de datos.  
  
 **Configuración regional**  
 Especifique la ubicación para proporcionar información de ordenación y de conversión de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. El uso de Unicode impide especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Indique si se utiliza formato delimitado, de ancho fijo o derecho irregular. Todos los archivos deben tener el mismo formato de datos.  
  
|Value|Description|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores, que se especifican en la página **Columnas** .|  
|Ancho fijo|Las columnas tienen un ancho fijo, que se especifica arrastrando líneas de marcador en la página **Columnas** .|  
|Derecho irregular|Los archivos de derecho irregular son los archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas, que se especifica en la página **Columnas** .|  
  
 **Calificador de texto**  
 Especifique el calificador de texto que se va a utilizar. Por ejemplo, puede especificar que el texto se incluya entre comillas.  
  
 **Delimitador de filas de encabezados**  
 Seleccione uno de los delimitadores de filas de encabezados de la lista o escriba el texto delimitador.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|La fila de encabezado está delimitada por una combinación de retorno de carro y avance de línea.|  
|**{CR}**|La fila de encabezado está delimitada por un retorno de carro.|  
|**{LF}**|La fila de encabezado está delimitada por un avance de línea.|  
|**Punto y coma {;}**|La fila de encabezado está delimitada por un punto y coma.|  
|**Dos puntos {:}**|La fila de encabezado está delimitada por dos puntos.|  
|**Coma {,}**|La fila de encabezado está delimitada por una coma.|  
|**Tabulación {t}**|La fila de encabezado está delimitada por una tabulación.|  
|**Barra vertical {&#124;}**|La fila de encabezado está delimitada por una barra vertical.|  
  
 **Filas de encabezados que se omitirán**  
 Especifica el número de filas de encabezados que se van a omitir, en caso de que esto ocurra.  
  
 **Nombres de columna de la primera fila de datos**  
 Indica si deben esperarse o deben especificarse nombres de columna en la primera fila de datos.  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>Editor del administrador de conexiones de varios archivos planos (página Columnas)
  Utilice el nodo **Columnas** del cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** para especificar la información de filas y columnas, y para obtener una vista previa del primer archivo seleccionado.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de varios archivos planos en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
### <a name="flat-file-format-dynamic-options"></a>Opciones dinámicas de formato para archivos planos  
  
#### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las filas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las filas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las filas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las filas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las filas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las filas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las filas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las filas se delimitan mediante una barra vertical.|  
  
 **Delimitador de columna**  
 Selecciónelo de la lista de delimitadores de columna disponibles o escriba el texto delimitador.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante un punto y coma.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
#### <a name="format--fixed-width"></a>Formato = Ancho fijo  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Ancho de fila**  
 Especifique la longitud de la fila antes de agregar los delimitadores para las columnas individuales. O bien arrastre la línea vertical en la ventana de vista previa para marcar el final de la fila. El valor del ancho de la fila se actualizará automáticamente.  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
#### <a name="format--ragged-right"></a>Formato = Derecho irregular  
  
> [!NOTE]  
>  Los archivos de derecho irregular son aquellos en los que todas las columnas tiene un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.  
  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las filas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las filas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las filas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las filas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las filas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las filas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las filas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las filas se delimitan mediante una barra vertical.|  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor del administrador de conexiones de varios archivos planos (página Avanzadas)
  Use la página **Avanzadas** del cuadro de diálogo **Editor del Administrador de conexiones de varios archivos planos** para establecer propiedades como el tipo de datos y los delimitadores de cada columna en los archivos de texto a los que se conecta el administrador de conexiones de archivos planos.  
  
 De forma predeterminada, la longitud de las columnas de cadena es de 50 caracteres. Puede evaluar datos de ejemplo y cambiar la longitud de estas columnas de forma automática para evitar el truncamiento de los datos o el exceso del ancho de columna. También puede actualizar otros metadatos para habilitar la compatibilidad con las columnas de destino. Por ejemplo, puede cambiar el tipo de datos de una columna que solo contiene tipos de datos enteros a un tipo de datos numéricos, como DT_I2.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para el Administrador de conexiones de varios archivos planos en el flujo de trabajo. Este nombre aparecerá en el área **Administradores de conexión** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Consulte la siguiente tabla para obtener una descripción de las propiedades de los tipos de datos. Algunas de las propiedades que aparecen en la lista solo son configurables en algunos formatos de archivos planos.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que se termina con el delimitador de filas.|  
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano.<br /><br /> Nota: en el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**DataType**|Seleccione los tipos de datos disponibles en la lista. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica si los datos de texto se han calificado mediante un carácter calificador de texto.<br /><br /> **True**: se califican los datos de texto del archivo plano.<br /><br /> **False**: no se califican los datos de texto del archivo plano.|  
|**Nombre**|Proporcione un nombre de columna. Una lista numerada de columnas es el valor predeterminado; sin embargo, puede elegir un nombre único y descriptivo.|  
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}** : las columnas se delimitan con una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}** : las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}** : las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}** : las columnas se delimitan mediante un punto y coma.<br /><br /> **Colon {:}** : las columnas se delimitan mediante dos puntos.<br /><br /> **Coma {,}** : las columnas se delimitan mediante una coma.<br /><br /> **Pestaña {t}** : las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}**: las columnas se delimitan con una barra vertical.|  
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|  
  
 **Nuevo**  
 Para agregar una columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón también tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Delete**  
 Seleccione una columna y, después, haga clic en **Eliminar**para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del primer archivo seleccionado y obtener sugerencias para los tipos de datos y la longitud de cada columna. Para más información, vea [Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>Editor del administrador de conexiones de varios archivos planos (página Vista previa)
  Use la página **Vista previa** del cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** para ver el contenido del primer archivo de origen seleccionado dividido en las columnas que ha definido.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de varios archivos planos en el flujo de trabajo. Este nombre aparecerá en el área **Administradores de conexión** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Filas de datos que se omitirán**  
 Especifique cuántas filas se omitirán al inicio del archivo plano.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del primer archivo plano seleccionado, divididos en columnas y filas mediante las opciones seleccionadas.  
  
## <a name="see-also"></a>Vea también  
 [Origen de archivo plano](../../integration-services/data-flow/flat-file-source.md)   
 [Destino de archivo plano](../../integration-services/data-flow/flat-file-destination.md)   
 [Integration Services &#40; SSIS &#41; Conexiones](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  


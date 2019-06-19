---
title: Administrador de conexiones de archivos planos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cf3156597035241398e354e8c80bfebb9c16d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728269"
---
# <a name="flat-file-connection-manager"></a>Administrador de conexiones de archivos planos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un administrador de conexiones de archivos planos permite a un paquete obtener acceso a datos en un archivo plano. Por ejemplo, el origen y el destino de archivos planos pueden hacer que los administradores de conexión de archivos planos extraigan y carguen datos.  
  
 El administrador de conexiones de archivos planos solo puede obtener acceso a un archivo. Para hacer referencia a varios archivos, use, en lugar de un Administrador de conexiones de archivos planos, un administrador de conexiones de varios archivos planos. Para más información, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Longitud de columnas  
 De forma predeterminada, el administrador de conexiones de archivos planos establece la longitud de las columnas de cadena en 50 caracteres. En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , puede evaluar datos de muestra y automáticamente cambiar el tamaño de la longitud de esas columnas para evitar el truncamiento de datos o un ancho de columna excesivo. Asimismo, a menos que posteriormente cambie el tamaño de la longitud de la columna en un origen de archivo plano o una transformación, la longitud de columna de la columna de cadena permanece invariable en todo el flujo de datos. Si estas columnas se asignan a columnas de destino más estrechas, aparecen mensajes de advertencia en la interfaz de usuario. Además, en tiempo de ejecución se pueden generar errores debido al truncamiento de datos Para evitar errores o el truncamiento de datos, puede cambiar el tamaño de las columnas para que sean compatibles con las columnas de destino en el administrador de conexiones de archivos planos, el origen de archivo plano o una transformación. Para modificar la longitud de las columnas de salida, establezca la propiedad **Length** de la columna de salida en la pestaña **Propiedades de entrada y salida** del cuadro de diálogo **Editor avanzado** .  
  
 Si actualiza las longitudes de columna en el administrador de conexiones de archivos planos una vez que ya ha agregado y configurado el origen de archivo plano que utiliza el administrador de conexiones, no tiene que cambiar manualmente el tamaño de las columnas de salida en el origen de archivo plano. Cuando abre el cuadro de diálogo **Origen de archivo plano** , el origen de archivo plano proporciona una opción para sincronizar los metadatos de columna.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configuración del administrador de conexiones de archivos planos  
 Cuando se agrega un administrador de conexiones de archivos planos a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve en una conexión de archivos planos en tiempo de ejecución, establece las propiedades de conexión del archivo plano y agrega el administrador de conexiones de archivos planos a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **FLATFILE**.  
  
 De forma predeterminada, el administrador de conexiones de archivos planos comprueba siempre si hay un delimitador de filas de datos sin comillas e inicia una nueva fila cuando se encuentra un delimitador de filas. Esta opción permite al administrador de conexiones analizar correctamente los archivos con filas que son campos de columna ausentes.  
  
 En algunos casos, si se deshabilita esta característica, se puede mejorar el rendimiento del paquete. Puede deshabilitar esta característica si establece la propiedad del administrador de conexiones de archivos planos, **AlwaysCheckForRowDelimiters**, en **False**.  
  
 Puede configurar el administrador de conexiones de archivos planos de las maneras siguientes:  
  
-   Especificar el archivo, configuración regional y página de códigos que se debe usar. La configuración regional se usa para interpretar datos que dependen de la región, como las fechas, y la página de códigos se usa para convertir los datos de cadenas en Unicode.  
  
-   Especificar el formato de archivo. Se puede usar un ancho delimitado y fijo o un formato desigual a la derecha.  
  
-   Especificar delimitadores de filas de encabezados, de filas de datos y de columnas. Los delimitadores de columna se pueden establecer en el nivel de fila y se sobrescriben en el nivel de columna.  
  
-   Indicar si la primera fila del archivo contiene nombres de columnas.  
  
-   Especificar un carácter calificador de texto. Cada columna se puede configurar para reconocer un calificador de texto.  
  
     El uso de un carácter calificador para incrustar un carácter calificador en una cadena calificada es compatible gracias al Administrador de conexiones de archivos planos. La instancia doble de un calificador de texto se interpreta como una instancia única literal de dicha cadena. Por ejemplo, si el calificador de texto es una comilla simple y los datos de entrada son 'abc', 'def', 'g'hi', los datos de salida son abc, def, g'hi. Sin embargo, una instancia de un calificador incrustado en una cadena calificada hace que el origen de archivo plano produzca el error DTS_E_PRIMEOUTPUTFAILED.
  
-   Establecer propiedades tales como el nombre, tipo de datos y ancho máximo de columnas individuales.  
  
 Para establecer la propiedad ConnectionString del administrador de conexiones de archivos planos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para evitar un error de validación, haga lo siguiente.  
  
-   Al utilizar una expresión para especificar el archivo, agregue una ruta en el cuadro **Nombre de archivo** del **Editor del administrador de conexiones de archivos planos**.  
  
-   Establezca la propiedad de **DelayValidation** en el administrador de conexión de archivos planos a **True**.  
  
 Puede utilizar una expresión para crear un nombre de archivo en tiempo de ejecución mediante el administrador de conexión de archivos planos al destino de archivo plano.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>Editor del administrador de conexiones de archivos planos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para seleccionar un archivo y un formato de datos. Las conexiones de archivos planos permiten que un paquete se conecte con un archivo de texto.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de archivo plano en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Nombre de archivo**  
 Escriba la ruta de acceso y el nombre de archivo que utilizará en la conexión de archivos planos.  
  
 **Examinar**  
 Busque el nombre de archivo que utilizará en la conexión de archivos planos.  
  
 **Configuración regional**  
 Especifique la configuración regional, que proporciona información específica del idioma para la ordenación y los formatos de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Indique si el archivo utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores, que se especifican en la página **Columnas** .|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto que se va a utilizar. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas.  
  
> [!NOTE]  
>  Tras seleccionar un calificador de texto, no puede volver a elegir la opción **Ninguno** . Escriba **Ninguno** para anular la selección del calificador de texto.  
  
 **Delimitador de filas de encabezados**  
 Seleccione uno de los delimitadores de filas de encabezados de la lista o escriba el texto delimitador.  
  
|Valor|Descripción|  
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
 Especifique el número de filas de encabezado o filas de datos iniciales que se deben omitir, si es necesario.  
  
 **Nombres de columna de la primera fila de datos**  
 Indica si deben esperarse o deben especificarse nombres de columna en la primera fila de datos.  
## <a name="flat-file-connection-manager-editor-columns-page"></a>Editor del administrador de conexiones de archivos planos (página Columnas)
  Utilice la página **Columnas** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para especificar la información de filas y columnas, y para obtener una vista previa del archivo.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de archivo plano en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
### <a name="flat-file-format-dynamic-options"></a>Opciones dinámicas de formato para archivos planos  
  
#### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Valor|Descripción|  
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
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante un punto y coma.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  
  
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto del cambio de delimitadores que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas mediante las opciones seleccionadas.  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
#### <a name="format--fixed-width"></a>Formato = Ancho fijo  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Ancho de fila**  
 Especifique la longitud de la fila antes de agregar los delimitadores para las columnas individuales. O bien arrastre la línea roja vertical en la ventana de vista previa para marcar el final de la fila. El valor del ancho de la fila se actualizará automáticamente.  
  
 **Restablecer columnas**  
 Al hacer clic en **Restablecer columnas**se eliminará todo, excepto las columnas originales.  
  
#### <a name="format--ragged-right"></a>Formato = Derecho irregular  
  
> [!NOTE]  
>  Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.  
  
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Valor|Descripción|  
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
## <a name="flat-file-connection-manager-editor-advanced-page"></a>Editor del administrador de conexiones de archivos planos (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para establecer prioridades que especifiquen la forma en que Integration Services debe leer y escribir datos en archivos planos. Puede cambiar los nombres de columna del archivo plano y establecer propiedades que incluyan tipos de datos y delimitadores para cada columna del archivo.  
  
 De forma predeterminada, la longitud de las columnas de cadena es de 50 caracteres. Puede cambiar la longitud de estas columnas para evitar el truncamiento de los datos o el exceso del ancho de columna. También puede actualizar otros metadatos para habilitar la compatibilidad con las columnas de destino. Por ejemplo, puede cambiar el tipo de datos de una columna que solo contiene tipos de datos enteros a un tipo de datos numéricos, como DT_I2. Puede realizar estas modificaciones de forma manual o puede hacer clic en el botón **Sugerir tipos...** para usar el cuadro de diálogo **Sugerir tipos de columna** a fin de evaluar datos de ejemplo y que algunos de estos cambios se realicen automáticamente.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para el administrador de conexiones de archivos planos en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Consulte la siguiente tabla para obtener una descripción de las propiedades de los tipos de datos. Algunas de las propiedades que aparecen en la lista solo son configurables en algunos formatos de archivos planos.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, el valor corresponde a un recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano. En el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**DataType**|Seleccione los tipos de datos disponibles en la lista. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica si los datos de texto están entre caracteres calificadores de texto como caracteres de comillas.<br /><br /> True: Se califican los datos de texto del archivo plano. False: No se califican los datos de texto del archivo plano.|  
|**Nombre**|Proporcione un nombre de columna descriptivo. Si no se escribe un nombre, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea uno automáticamente con el formato Columna 0, Columna 1, etc.|  
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}** . Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}** . Las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}** . Las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}** . Las columnas se delimitan mediante un punto y coma.<br /><br /> **Dos puntos {:}** . Las columnas se delimitan mediante un punto y coma.<br /><br /> **Coma {,}** . Las columnas se delimitan mediante una coma.<br /><br /> **Tabulación {t}** . Las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}** . Las columnas se delimitan mediante una barra vertical.|  
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|  
  
 **Nueva**  
 Para agregar una columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón siempre tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Eliminar**  
 Seleccione una columna y, después, haga clic en **Eliminar**para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del archivo y obtener sugerencias para el tipo de datos y la longitud de cada columna. Para más información, vea [Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
## <a name="flat-file-connection-manager-editor-preview-page"></a>Editor del administrador de conexiones de archivos planos (página Vista previa)
  Utilice el nodo **Vista previa** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para ver el contenido del archivo de origen en formato tabular.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para la conexión de archivo plano en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describe la conexión. Como método recomendado, describa la conexión desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Filas de datos que se omitirán**  
 Especifique cuántas filas se omitirán al inicio del archivo plano.  
  
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto de cambiar el número de filas que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas según las opciones seleccionadas.  
 

---
title: Conectarse a un origen de datos de archivo sin formato (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 568d02ef58102b47501415d35f64369e997e875b
ms.contentlocale: es-es
ms.lasthandoff: 10/18/2017

---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de archivo sin formato (SQL Server importar y exportar)
Este tema muestra cómo conectarse a un **archivos planos** del origen de datos (archivo de texto) desde el **elegir un origen de datos** o **elegir un destino** página del SQL Server Import y Export Asistente. Para archivos sin formato, estas dos páginas del Asistente para presentan diferentes conjuntos de opciones, por lo que este tema describe el origen de archivo sin formato y el destino de archivo sin formato por separado.

## <a name="an-alternative-for-simple-text-import"></a>Una alternativa para la importación de texto simple
Si tiene que importar un archivo de texto a SQL Server y no necesita todas las opciones de configuración disponibles en la importación y el Asistente para exportación, considere la posibilidad de usar el **Importar Asistente de archivo sin formato** en SQL Server Management Studio (SSMS). Para obtener más información, vea los artículos siguientes:
- [What’s new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (Novedades en SQL Server Management Studio 17.3)
- [Introducing the new Import Flat File Wizard in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) (Introducción al nuevo Asistente para importación de archivos planos en SSMS 17.3)

## <a name="connect-to-a-flat-file-source"></a>Conectarse a un origen de archivo sin formato
 
 Hay cuatro páginas de opciones para orígenes de datos de archivo sin formato. Es una gran cantidad de páginas. Pero no tendrá que dedicar mucho tiempo en cada página. A continuación se indican las tareas para tener en cuenta.
 
Página|Recomendación  |Tipo  
----|---------|---------
**General**|Asegúrese de actualizar las opciones de la **formato** sección.|Se recomienda    
**Columnas**|Asegúrese de comprobar los delimitadores de columna y fila (para un archivo delimitado) o marcar las columnas (para un archivo de ancho fijo).|Se recomienda
**Avanzadas**|Si lo desea, compruebe los tipos de datos y otras propiedades asignadas a las columnas de forma predeterminada.|Opcional
**Vista previa**|Si lo desea, puede obtener una vista previa una muestra de los datos, con la configuración que especificó.|Opcional

## <a name="general-page-source"></a>Página general (origen)
 En la página **General**, busque y seleccione el archivo, y compruebe la configuración en la sección **Formato**.
 
 ![Conexión general de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Opciones para especificar (**General** página)

 **Nombre de archivo**  
 Escriba la ruta de acceso y el nombre del archivo plano.  
  
 **Examinar**  
 Busque el archivo sin formato.  
  
 **Configuración regional**  
 Especificar la configuración regional para proporcionar información específica del lenguaje para la ordenación y de formatos de fecha y hora.  
  
 **Unicode**  
 Especifique si el archivo usa Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Seleccione si el archivo utiliza delimitado, ancho fijo o derecho irregular.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores. Especifique el delimitador en la **columnas** página.|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto, si existe, se utiliza el archivo. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas. (Esta propiedad solo se aplica a archivos delimitados por). 
  
> [!NOTE]
> Después de seleccionar un calificador de texto, no puede volver a seleccionar el **ninguno** opción. Escriba **Ninguno** para anular la selección del calificador de texto.  
  
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
 Especifique el número de filas que se omiten en la parte superior del archivo, si existe.  
  
 **Nombres de columna de la primera fila de datos**  
 Especifica si la primera fila (después de las filas omitidas) contiene los nombres de columna.

## <a name="columns-page---format--delimited-source"></a>Página de columnas - formato = delimitado (origen)
 En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **delimitado** como el formato de archivo sin formato.
 
![Archivo sin formato, formato delimitado, página columnas](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Opciones para especificar (**columnas** página - formato = delimitado)

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
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas mediante las opciones seleccionadas.  
 
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto del cambio de delimitadores que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
  
 **Restablecer columnas**  
 Restaurar las columnas originales.  

## <a name="columns-page---format--fixed-width-source"></a>Página de columnas - formato = ancho fijo (origen)
En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **ancho fijo** como el formato de archivo sin formato.
  
![Archivo plano, ancho, página columnas fijo](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Opciones para especificar (**columnas** página - formato = ancho fijo)

 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Ancho de fila**  
 Especifique la longitud de la fila antes de agregar los delimitadores para las columnas individuales. O bien arrastre la línea roja vertical en la ventana de vista previa para marcar el final de la fila. El valor del ancho de la fila se actualizará automáticamente.  
  
 **Restablecer columnas**  
 Restaurar las columnas originales.  
  
## <a name="columns-page---format--ragged-right-source"></a>Página de columnas - formato = derecho irregular (origen)
En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **desigual a la derecha** como el formato de archivo sin formato.

> [!NOTE]
> Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.  
 
![Archivo plano, derecho irregular, página columnas](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Opciones para especificar (**columnas** página - formato = derecho irregular)
   
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
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
 Restaurar las columnas originales.  

## <a name="advanced-page-source"></a>Página Opciones avanzadas (origen)
La página **Avanzadas** muestra información detallada sobre cada columna del origen de datos, incluidos su tamaño y tipo de datos. La siguiente captura de pantalla muestra la **avanzadas** página de la primera columna de un archivo sin formato delimitado.

![Página de archivo sin formato, formato delimitado, avanzadas](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

En la captura de pantalla, tenga en cuenta que la **identificador** columna, que contiene números, inicialmente, tiene un tipo de datos de cadena.

### <a name="options-to-specify-advanced-page"></a>Opciones para especificar (**avanzadas** página)

 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Vea la tabla siguiente para obtener una descripción de las propiedades de columna. Algunas de las propiedades enumeradas son configurables únicamente para determinados formatos de archivo sin formato y las columnas de determinados tipos de datos.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Nombre**|Proporcione un nombre de columna descriptivo. Si no especifica un nombre, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea automáticamente un nombre en el formato columna 0, columna 1 y así sucesivamente.|
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}**. Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}**. Las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}**. Las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}**. Las columnas se delimitan mediante un punto y coma.<br /><br /> **Dos puntos {:}**. Las columnas se delimitan mediante un punto y coma.<br /><br /> **Coma {,}**. Las columnas se delimitan mediante una coma.<br /><br /> **Tabulación {t}**. Las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}**. Las columnas se delimitan mediante una barra vertical.|
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, este valor es un recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos.|
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales.|
|**DataType**|Seleccione los tipos de datos disponibles en la lista.<br/>Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, el valor corresponde a un recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano. En el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**TextQualified**|Indica si los datos de texto están entre caracteres calificadores de texto como caracteres de comillas.<br /><br /> True: se califican los datos de texto del archivo plano. False: no se califican los datos de texto del archivo plano.|  
  
**Nuevo**  
 Para agregar una columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón siempre tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Delete**  
 Seleccione una columna y, después, haga clic en **Eliminar**para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del archivo y obtener sugerencias para el tipo de datos y la longitud de cada columna.  
 
Haga clic en **Sugerir tipos** para mostrar el cuadro de diálogo **Sugerir tipos de columna**. 

![Conexiones de archivos planos sugerir el cuadro de diálogo de tipos](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Después de elegir las opciones en el **Sugerir tipos de columna** cuadro de diálogo y haga clic en **Aceptar**, el asistente puede cambiar los tipos de datos de algunas de las columnas.

La captura de pantalla siguiente muestra que, al hacer clic en **Sugerir tipos**, reconoce que el Asistente para la **identificador** columna del origen de datos es en realidad un número y no una cadena de texto y ha cambiado el tipo de datos la columna de una cadena en un entero.

![Conexión avanzada de archivos planos (posterior)](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Para obtener más información, consulte [sugerir la referencia de cuadro de interfaz de usuario en el cuadro de diálogo de tipos de columna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Página de vista previa (origen)

En la página **Vista previa**, compruebe que la lista de columnas y los datos de ejemplos son lo que esperaba.

![Archivo plano, página de vista previa](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Opciones para especificar (**vista previa** página)

 **Filas de datos que se omitirán**  
 Especifique cuántas filas se omitirán al inicio del archivo plano.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas según las opciones seleccionadas.
 
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto de cambiar el número de filas que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
 
Para obtener más información sobre la página **Vista previa**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Conectarse a un destino de archivo sin formato
Para un destino de archivo plano, hay sólo una sola página de opciones, como se muestra en la siguiente captura de pantalla. Examinar para seleccionar el archivo, a continuación, compruebe la configuración en el **formato** sección.

![Conectarse al destino de archivo plano](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Opciones para especificar (**elegir un destino** página)

 **Nombre de archivo**  
 Escriba la ruta de acceso y el nombre del archivo plano.  
  
 **Examinar**  
 Busque el archivo sin formato.  
  
 **Configuración regional**  
 Especificar la configuración regional para proporcionar información específica del lenguaje para la ordenación y de formatos de fecha y hora.  
  
 **Unicode**  
 Especifique si el archivo usa Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Seleccione si el archivo utiliza delimitado, ancho fijo o derecho irregular.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores. Especifique el delimitador en la **columnas** página.|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto, si existe, se utiliza el archivo. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas. (Esta propiedad solo se aplica a archivos delimitados por). 
  
> [!NOTE] 
> Después de seleccionar un calificador de texto, no se vuelve a activar el **ninguno** opción. Escriba **Ninguno** para anular la selección del calificador de texto.  

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



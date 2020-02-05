---
title: Conexión a un origen de datos de archivo plano (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bef4e8032ad605382b3312cac11840ed959a7571
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296358"
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Conexión a un origen de datos de archivo plano (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En este tema se muestra cómo conectarse a un origen de datos de **archivo plano** (archivo de texto) desde la página **Seleccionar un origen de datos** o **Seleccionar un destino** del Asistente para importación y exportación de SQL Server. Para los archivos planos, estas dos páginas del Asistente presentan diferentes conjuntos de opciones, por lo que en este tema se describen el origen y el destino del archivo plano por separado.

## <a name="an-alternative-for-simple-text-import"></a>Una alternativa para la importación de texto simple
Si tiene que importar un archivo de texto en SQL Server y no necesita todas las opciones de configuración disponibles en el Asistente para importación y exportación, considere la posibilidad de usar el **Asistente para importación de archivos planos** en SQL Server Management Studio (SSMS). Para más información, consulte los siguientes artículos:
- [What's new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (Novedades en SQL Server Management Studio 17.3)
- [Introducing the new Import Flat File Wizard in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) (Introducción al nuevo Asistente para importación de archivos planos en SSMS 17.3)

## <a name="connect-to-a-flat-file-source"></a>Conexión a un origen de archivo plano
 
 Hay cuatro páginas de opciones para los orígenes de datos de archivos planos. Son muchas páginas. Sin embargo, no tendrá que dedicar mucho tiempo a cada página. A continuación se indican las tareas que debe tener en cuenta.
 
Página|Recomendación  |Tipo  
----|---------|---------
**General**|Asegúrese de actualizar las opciones de la sección **Formato**.|Recomendado    
**Columnas**|Asegúrese de comprobar los delimitadores de columna y fila (para un archivo delimitado) o marcar las columnas (para un archivo de ancho fijo).|Recomendado
**Avanzadas**|Si lo desea, compruebe los tipos de datos y otras propiedades asignadas a las columnas de forma predeterminada.|Opcional
**Versión preliminar**|Si lo desea, puede obtener una vista previa de una muestra de los datos con la configuración que especificó.|Opcional

## <a name="general-page-source"></a>Página General (origen)
 En la página **General**, busque y seleccione el archivo, y compruebe la configuración en la sección **Formato**.
 
 ![Conexión general de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Opciones que se deben especificar (página **General**)

 **Nombre de archivo**  
 Escriba la ruta y el nombre de archivo del archivo plano.  
  
 **Browse**  
 Busque el archivo plano.  
  
 **Configuración regional**  
 Especifique la configuración regional, que proporciona información específica del idioma para la ordenación y los formatos de fecha y hora.  
  
 **Unicode**  
 Especifique si el archivo usa Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Elija si el archivo utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores. Puede especificar el delimitador en la página **Columnas**.|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto, si corresponde, que se utiliza en el archivo. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas. (Esta propiedad solo se aplica a archivos delimitados). 
  
> [!NOTE]
> Tras seleccionar un calificador de texto, no puede volver a elegir la opción **Ninguno**. Escriba **Ninguno** para anular la selección del calificador de texto.  
  
 **Delimitador de filas de encabezados**  
 Seleccione uno de los delimitadores de filas de encabezados de la lista o escriba el texto delimitador.  
  
|Value|Descripción|  
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
 Especifique el número de filas que se omiten en el inicio del archivo, si corresponde.  
  
 **Nombres de columna de la primera fila de datos**  
 Especifique si la primera fila (después de las filas que se hayan omitido) contiene nombres de columna.

## <a name="columns-page---format--delimited-source"></a>Página Columnas: formato delimitado (origen)
 En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **Delimitado** como el formato de archivo plano.
 
![Página Columnas, archivo plano, delimitado](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Opciones que se deben especificar (página **Columnas**: formato delimitado)

 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Value|Descripción|  
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
  
|Value|Descripción|  
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
 Restaura las opciones originales.  

## <a name="columns-page---format--fixed-width-source"></a>Página Columnas: formato de ancho fijo (origen)
En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **Ancho fijo** como el formato de archivo plano.
  
![Página Columnas, archivo plano, ancho fijo](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Opciones para especificar (página **Columnas**: formato de ancho fijo)

 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Ancho de fila**  
 Especifique la longitud de la fila antes de agregar los delimitadores para las columnas individuales. O bien arrastre la línea roja vertical en la ventana de vista previa para marcar el final de la fila. El valor del ancho de la fila se actualizará automáticamente.  
  
 **Restablecer columnas**  
 Restaura las opciones originales.  
  
## <a name="columns-page---format--ragged-right-source"></a>Página Columnas: formato derecho irregular (origen)
En la página **Columnas**, compruebe la lista de columnas y los delimitadores que el asistente ha identificado. La captura de pantalla siguiente muestra la página cuando haya seleccionado **Derecho irregular** como el formato de archivo plano.

> [!NOTE]
> Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.  
 
![Página Columnas, archivo plano, derecho irregular](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Opciones para especificar (página **Columnas**: formato de derecho irregular)
   
 **Fuente**  
 Seleccione la fuente en la que se presentará la vista previa de los datos.  
  
 **Columnas de datos de origen**  
 Ajuste el ancho de la fila desplazando el marcador vertical de color rojo de la fila; ajuste el ancho de las columnas haciendo clic en la regla, en la parte superior de la ventana de vista previa.  
  
 **Delimitador de filas**  
 Selecciónelo de la lista de delimitadores de filas disponibles o escriba el texto delimitador.  
  
|Value|Descripción|  
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
 Restaura las opciones originales.  

## <a name="advanced-page-source"></a>Página Avanzadas (origen)
La página **Avanzadas** muestra información detallada sobre cada columna del origen de datos, incluidos su tamaño y tipo de datos. La siguiente captura de pantalla muestra la página **Avanzadas** de la primera columna de un archivo plano delimitado.

![Página Avanzadas, archivo plano, delimitado](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

En la captura de pantalla, tenga en cuenta que la columna **id**, que contiene números, inicialmente tiene un tipo de datos de cadena.

### <a name="options-to-specify-advanced-page"></a>Opciones para especificar (página **Avanzadas**)

 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Consulte la siguiente tabla para obtener una descripción de las propiedades de las columnas. Algunas de las propiedades que se muestran se pueden configurar únicamente para determinados formatos de archivo plano y para las columnas de determinados tipos de datos.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**Nombre**|Proporcione un nombre de columna descriptivo. Si no se escribe un nombre, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea uno automáticamente con el formato Columna 0, Columna 1, etc.|
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}** . Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}** . Las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}** . Las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}** . Las columnas se delimitan mediante un punto y coma.<br /><br /> **Dos puntos {:}** . Las columnas se delimitan mediante un punto y coma.<br /><br /> **Coma {,}** . Las columnas se delimitan mediante una coma.<br /><br /> **Tabulación {t}** . Las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}** . Las columnas se delimitan mediante una barra vertical.|
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, el valor es un recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos.|
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales.|
|**DataType**|Seleccione los tipos de datos disponibles en la lista.<br/>Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, el valor corresponde a un recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano. En el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**TextQualified**|Indica si los datos de texto están entre caracteres calificadores de texto como caracteres de comillas.<br /><br /> True: se califican los datos de texto del archivo plano. False: no se califican los datos de texto del archivo plano.|  
  
**Nuevo**  
 Para agregar una columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón siempre tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Eliminar**  
 Seleccione una columna y, después, haga clic en **Eliminar**para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del archivo y obtener sugerencias para el tipo de datos y la longitud de cada columna.  
 
Haga clic en **Sugerir tipos** para mostrar el cuadro de diálogo **Sugerir tipos de columna**. 

![Cuadro de diálogo Tipos de sugerencia de conexiones de archivos planos](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Después de que elija las opciones en el cuadro de diálogo **Sugerir tipos de columna** y haga clic en **Aceptar**, el asistente puede cambiar los tipos de datos de algunas de las columnas.

En la siguiente captura de pantalla se muestra que, después de hacer clic en **Sugerir tipos**, el asistente ha reconocido que la columna **id** del origen de datos es, de hecho, un número y no una cadena de texto, y ha cambiado el tipo de datos de la columna de una cadena a un entero.

![Conexión avanzada de archivos planos (posterior)](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Para obtener más información, vea [Suggest Column Types Dialog Box UI Reference](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md) (Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna).

## <a name="preview-page-source"></a>Página Vista previa (origen)

En la página **Vista previa**, compruebe que la lista de columnas y los datos de ejemplos son lo que esperaba.

![Página Vista previa, archivo plano](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Opciones que se deben especificar (página **Vista previa**)

 **Filas de datos que se omitirán**  
 Especifique cuántas filas se omitirán al inicio del archivo plano.  
  
 **Vista previa de filas**  
 Presenta datos de ejemplo del archivo plano, divididos en columnas y filas según las opciones seleccionadas.
 
 **Actualizar**  
 Al hacer clic en **Actualizar**, verá el efecto de cambiar el número de filas que se van a omitir. Este botón solo se hace visible después de cambiar otras opciones de conexión.  
 
Para obtener más información sobre la página **Vista previa**, consulte la siguiente página de referencia de Integration Services: [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Conexión a un destino de archivo plano
Para un destino de archivo plano, solo hay una página de opciones, como se muestra en la siguiente captura de pantalla. Busque y seleccione el archivo y compruebe la configuración en la sección **Formato**.

![Conexión a un destino de archivo plano](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Opciones para especificar (página **Seleccionar un destino**)

 **Nombre de archivo**  
 Escriba la ruta y el nombre de archivo del archivo plano.  
  
 **Browse**  
 Busque el archivo plano.  
  
 **Configuración regional**  
 Especifique la configuración regional, que proporciona información específica del idioma para la ordenación y los formatos de fecha y hora.  
  
 **Unicode**  
 Especifique si el archivo usa Unicode. Si utiliza Unicode, no puede especificar una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos para el texto no Unicode.  
  
 **Formato**  
 Elija si el archivo utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante delimitadores. Puede especificar el delimitador en la página **Columnas**.|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Especifique el calificador de texto, si corresponde, que se utiliza en el archivo. Por ejemplo, puede indicar que los archivos de texto se delimitan con comillas. (Esta propiedad solo se aplica a archivos delimitados). 
  
> [!NOTE] 
> Tras seleccionar un calificador de texto, no puede volver a elegir la opción **Ninguno**. Escriba **Ninguno** para anular la selección del calificador de texto.  

## <a name="see-also"></a>Consulte también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)


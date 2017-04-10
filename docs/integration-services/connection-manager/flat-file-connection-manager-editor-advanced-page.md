---
title: "Editor del administrador de conexiones de archivos planos (p&#225;gina Avanzadas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ffileconnection.columnproperties.f1"
helpviewer_keywords: 
  - "Administrador de conexiones de archivos planos, editor del"
ms.assetid: 58aa3dee-4774-4e0b-a956-96d199be4c3a
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# Editor del administrador de conexiones de archivos planos (p&#225;gina Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor del administrador de conexiones de archivos planos** para establecer prioridades que especifiquen la forma en que Integration Services debe leer y escribir datos en archivos planos. Puede cambiar los nombres de columna del archivo plano y establecer propiedades que incluyan tipos de datos y delimitadores para cada columna del archivo.  
  
 De forma predeterminada, la longitud de las columnas de cadena es de 50 caracteres. Puede cambiar la longitud de estas columnas para evitar el truncamiento de los datos o el exceso del ancho de columna. También puede actualizar otros metadatos para habilitar la compatibilidad con las columnas de destino. Por ejemplo, puede cambiar el tipo de datos de una columna que solo contiene tipos de datos enteros a un tipo de datos numéricos, como DT_I2. Puede realizar estas modificaciones de forma manual o puede hacer clic en el botón **Sugerir tipos...** para usar el cuadro de diálogo **Sugerir tipos de columna** a fin de evaluar datos de ejemplo y que algunos de estos cambios se realicen automáticamente.  
  
 Para obtener más información acerca del administrador de conexiones de archivos planos, vea [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
## Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para el administrador de conexiones de archivos planos en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Consulte la siguiente tabla para obtener una descripción de las propiedades de los tipos de datos. Algunas de las propiedades que aparecen en la lista solo son configurables en algunos formatos de archivos planos.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última. Se delimita mediante el delimitador de fila.|  
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, el valor corresponde a un recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano. En el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**DataType**|Seleccione los tipos de datos disponibles en la lista. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica si los datos de texto están entre caracteres calificadores de texto como caracteres de comillas.<br /><br /> True: se califican los datos de texto del archivo plano. False: no se califican los datos de texto del archivo plano.|  
|**Nombre**|Proporcione un nombre de columna descriptivo. Si no se escribe un nombre, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea uno automáticamente con el formato Columna 0, Columna 1, etc.|  
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}**. Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}**. Las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}**. Las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}**. Las columnas se delimitan mediante un punto y coma.<br /><br /> **Dos puntos {:}**. Las columnas se delimitan mediante un punto y coma.<br /><br /> **Coma {,}**. Las columnas se delimitan mediante una coma.<br /><br /> **Tabulación {t}**. Las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}**. Las columnas se delimitan mediante una barra vertical.|  
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|  
  
 **Nuevo**  
 Para agregar una nueva columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón siempre tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Delete**  
 Seleccione una columna y, después, haga clic en **Eliminar** para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del archivo y obtener sugerencias para el tipo de datos y la longitud de cada columna. Para más información, vea [Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)   
 [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  
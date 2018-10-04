---
title: Editor del Administrador de conexiones (página avanzadas) varios archivos planos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.advanced.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dda5cb294536354ed4bcc5003983d36f61167007
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143335"
---
# <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor del administrador de conexiones de varios archivos planos (página Avanzadas)
  Use la página **Avanzadas** del cuadro de diálogo **Editor del Administrador de conexiones de varios archivos planos** para establecer propiedades como el tipo de datos y los delimitadores de cada columna en los archivos de texto a los que se conecta el administrador de conexiones de archivos planos.  
  
 De forma predeterminada, la longitud de las columnas de cadena es de 50 caracteres. Puede evaluar datos de ejemplo y cambiar la longitud de estas columnas de forma automática para evitar el truncamiento de los datos o el exceso del ancho de columna. También puede actualizar otros metadatos para habilitar la compatibilidad con las columnas de destino. Por ejemplo, puede cambiar el tipo de datos de una columna que solo contiene tipos de datos enteros a un tipo de datos numéricos, como DT_I2.  
  
 Para obtener más información acerca del administrador de conexiones de varios archivos planos, vea [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Especifique un nombre único para el Administrador de conexiones de varios archivos planos en el flujo de trabajo. Este nombre aparecerá en el área **Administradores de conexión** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Configure las propiedades de cada columna**  
 Seleccione una columna del panel izquierdo para ver sus propiedades en el panel derecho. Consulte la siguiente tabla para obtener una descripción de las propiedades de los tipos de datos. Algunas de las propiedades que aparecen en la lista solo son configurables en algunos formatos de archivos planos.  
  
|Property|Descripción|  
|--------------|-----------------|  
|**ColumnType**|Denota si la columna es delimitada, de ancho fijo o derecho irregular. Esta propiedad es de solo lectura. Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que se termina con el delimitador de filas.|  
|**OutputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. En la tarea Flujo de datos este valor se utiliza para establecer el ancho de la columna de salida para el origen del archivo plano.<br /><br /> Nota: en el modelo de objetos, el nombre de esta propiedad es MaximumWidth.|  
|**DataType**|Seleccione los tipos de datos disponibles en la lista. Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica si los datos de texto se han calificado mediante un carácter calificador de texto. Los valores válidos son:<br /><br /> **True**: se califican los datos de texto del archivo plano.<br /><br /> **False**: no se califican los datos de texto del archivo plano.|  
|**Nombre**|Proporcione un nombre de columna. Una lista numerada de columnas es el valor predeterminado; sin embargo, puede elegir un nombre único y descriptivo.|  
|**DataScale**|Especifique la escala de los datos numéricos. La escala hace referencia al número de posiciones decimales. Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleccione los delimitadores de columna disponibles en la lista. Elija delimitadores que no sea probable encontrar en el texto. Este valor se omite para las columnas de ancho fijo.<br /><br /> **{CR}{LF}** : las columnas se delimitan con una combinación de retorno de carro y avance de línea.<br /><br /> **{CR}** : las columnas se delimitan mediante un retorno de carro.<br /><br /> **{LF}** : las columnas se delimitan mediante un avance de línea.<br /><br /> **Punto y coma {;}** : las columnas se delimitan mediante un punto y coma.<br /><br /> **Colon {:}** : las columnas se delimitan mediante dos puntos.<br /><br /> **Coma {,}**: las columnas se delimitan mediante una coma.<br /><br /> **Pestaña {t}** : las columnas se delimitan mediante un tabulador.<br /><br /> **Barra vertical {&#124;}**: las columnas se delimitan con una barra vertical.|  
|**DataPrecision**|Especifique la precisión de los datos numéricos. La precisión hace referencia al número de dígitos. Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifique un valor que se almacenará como recuento de bytes; en los archivos Unicode, aparecerá como recuento de caracteres. Este valor se omite para las columnas delimitadas.<br /><br /> **Nota** En el modelo de objetos, el nombre de esta propiedad es ColumnWidth.|  
  
 **Nueva**  
 Para agregar una columna, haga clic en **Nuevo**. De manera predeterminada, el botón **Nueva** agrega una columna nueva al final de la lista. El botón también tiene las siguientes opciones, disponibles en la lista desplegable.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Agregar columna**|Agrega una nueva columna al final de la lista.|  
|**Insertar delante**|Inserta una nueva columna antes de la columna seleccionada.|  
|**Insertar detrás**|Inserta una nueva columna detrás de la columna seleccionada.|  
  
 **Eliminar**  
 Seleccione una columna y, después, haga clic en **Eliminar**para quitarla.  
  
 **Sugerir tipos**  
 Use el cuadro de diálogo **Sugerir tipos de columna** para evaluar los datos de ejemplo del primer archivo seleccionado y obtener sugerencias para los tipos de datos y la longitud de cada columna. Para más información, vea [Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna](connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40;página columnas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor del Administrador de conexiones de varios archivos planos &#40;vista previa de página&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  

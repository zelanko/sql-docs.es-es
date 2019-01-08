---
title: Administrador de conexiones de archivos planos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 65cebbe74b1be5cc0d625a70c8c5b87e8f515150
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815297"
---
# <a name="flat-file-connection-manager"></a>Administrador de conexiones de archivos planos
  Un administrador de conexiones de archivos planos permite a un paquete obtener acceso a datos en un archivo plano. Por ejemplo, el origen y el destino de archivos planos pueden hacer que los administradores de conexión de archivos planos extraigan y carguen datos.  
  
 El administrador de conexiones de archivos planos solo puede obtener acceso a un archivo. Para hacer referencia a varios archivos, use, en lugar de un Administrador de conexiones de archivos planos, un administrador de conexiones de varios archivos planos. Para más información, consulte [Multiple Flat Files Connection Manager](multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Longitud de columnas  
 De forma predeterminada, el administrador de conexiones de archivos planos establece la longitud de las columnas de cadena en 50 caracteres. En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** , puede evaluar datos de muestra y automáticamente cambiar el tamaño de la longitud de esas columnas para evitar el truncamiento de datos o un ancho de columna excesivo. Asimismo, a menos que posteriormente cambie el tamaño de la longitud de la columna en un origen de archivo plano o una transformación, la longitud de columna de la columna de cadena permanece invariable en todo el flujo de datos. Si estas columnas se asignan a columnas de destino más estrechas, aparecen mensajes de advertencia en la interfaz de usuario. Además, en tiempo de ejecución se pueden generar errores debido al truncamiento de datos Para evitar errores o el truncamiento de datos, puede cambiar el tamaño de las columnas para que sean compatibles con las columnas de destino en el administrador de conexiones de archivos planos, el origen de archivo plano o una transformación. Para modificar la longitud de columnas de salida, establezca el `Length` propiedad de la columna de salida en el **propiedades de entrada y salida** pestaña en el **Editor avanzado** cuadro de diálogo.  
  
 Si actualiza las longitudes de columna en el administrador de conexiones de archivos planos una vez que ya ha agregado y configurado el origen de archivo plano que utiliza el administrador de conexiones, no tiene que cambiar manualmente el tamaño de las columnas de salida en el origen de archivo plano. Cuando abre el cuadro de diálogo **Origen de archivo plano** , el origen de archivo plano proporciona una opción para sincronizar los metadatos de columna.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configuración del administrador de conexiones de archivos planos  
 Cuando se agrega un administrador de conexiones de archivos planos a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión de archivos planos en tiempo de ejecución, Establece las propiedades de conexión de archivos planos y agrega el Administrador de conexiones de archivos planos a la `Connections` recopilación del paquete.  
  
 La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `FLATFILE`.  
  
 De forma predeterminada, el administrador de conexiones de archivos planos comprueba siempre si hay un delimitador de filas de datos sin comillas e inicia una nueva fila cuando se encuentra un delimitador de filas. Esta opción permite al administrador de conexiones analizar correctamente los archivos con filas que son campos de columna ausentes.  
  
 En algunos casos, si se deshabilita esta característica, se puede mejorar el rendimiento del paquete. Puede deshabilitar esta característica estableciendo la propiedad del Administrador de conexiones de archivos planos **AlwaysCheckForRowDelimiters**a `False`.  
  
 Puede configurar el administrador de conexiones de archivos planos de las maneras siguientes:  
  
-   Especificar el archivo, configuración regional y página de códigos que se debe usar. La configuración regional se usa para interpretar datos que dependen de la región, como las fechas, y la página de códigos se usa para convertir los datos de cadenas en Unicode.  
  
-   Especificar el formato de archivo. Se puede usar un ancho delimitado y fijo o un formato desigual a la derecha.  
  
-   Especificar delimitadores de filas de encabezados, de filas de datos y de columnas. Los delimitadores de columna se pueden establecer en el nivel de fila y se sobrescriben en el nivel de columna.  
  
-   Indicar si la primera fila del archivo contiene nombres de columnas.  
  
-   Especificar un carácter calificador de texto. Cada columna se puede configurar para reconocer un calificador de texto.  
  
     Ahora se admite el uso de un carácter calificador para incrustar un carácter calificador en una cadena calificada. La instancia doble de un calificador de texto se interpreta como una instancia única literal de dicha cadena. Por ejemplo, si el calificador de texto es una comilla simple y los datos de entrada son 'abc', 'def', 'g'hi', los datos de salida son abc, def, g'hi.  
  
-   Establecer propiedades tales como el nombre, tipo de datos y ancho máximo de columnas individuales.  
  
 Para establecer la propiedad ConnectionString del administrador de conexiones de archivos planos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para evitar un error de validación, haga lo siguiente.  
  
-   Al utilizar una expresión para especificar el archivo, agregue una ruta en el cuadro **Nombre de archivo** del **Editor del administrador de conexiones de archivos planos**.  
  
-   Establezca la propiedad de **DelayValidation** en el administrador de conexión de archivos planos a **True**.  
  
 Puede utilizar una expresión para crear un nombre de archivo en tiempo de ejecución mediante el administrador de conexión de archivos planos al destino de archivo plano.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  

---
title: Administrador de conexiones de varios archivos planos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 575bf85a81557e7a0a974dd1fc2210e58f34bde0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790537"
---
# <a name="multiple-flat-files-connection-manager"></a>administrador de conexiones de varios archivos planos
  Un administrador de conexiones de varios archivos planos permite a un paquete obtener acceso a datos de varios archivos planos. Por ejemplo, un origen de archivos planos puede utilizar un administrador de conexiones para varios archivos planos cuando la tarea Flujo de datos se encuentra en un contenedor de bucles, como el contenedor de bucles For. En cada bucle del contenedor, el origen de archivos planos carga los datos del siguiente nombre de archivo que proporciona el administrador de conexiones de varios archivos planos.  
  
 Cuando se agrega un administrador de conexiones de varios archivos planos a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión de varios archivos planos en tiempo de ejecución, Establece las propiedades en el Administrador de conexiones de varios archivos planos, y Agrega el Administrador de conexiones de varios archivos planos a la `Connections` recopilación del paquete.  
  
 La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `MULTIFLATFILE`.  
  
 Puede configurar el administrador de conexiones de varios archivos planos de las maneras siguientes:  
  
-   Especificar los archivos, configuración regional y página de códigos que se debe usar. La configuración regional se usa para interpretar datos que dependen de la región, como las fechas, y la página de códigos se usa para convertir los datos de cadenas en Unicode.  
  
-   Especificar el formato de archivo. Se puede usar un ancho delimitado y fijo o un formato desigual a la derecha.  
  
-   Especificar delimitadores de filas de encabezados, de filas de datos y de columnas. Los delimitadores de columna se pueden establecer en el nivel de fila y se sobrescriben en el nivel de columna.  
  
-   Indicar si la primera fila de los archivos contiene nombres de columnas.  
  
-   Especificar un carácter calificador de texto. Cada columna se puede configurar para reconocer un calificador de texto.  
  
-   Establecer propiedades tales como el nombre, tipo de datos y ancho máximo de columnas individuales.  
  
 Si el administrador de conexiones de varios archivos planos hace referencia a varios archivos, las rutas de los archivos se separan con la barra vertical (|). La propiedad `ConnectionString` del administrador de conexiones tiene el formato siguiente:  
  
 \<*ruta de acceso*>|\<*ruta de acceso*>  
  
 También puede especificar varios archivos mediante caracteres comodín. Por ejemplo, para hacer referencia unidad de todos los archivos de texto en C, el valor de la `ConnectionString` propiedad se puede establecer en C:\\*.txt.  
  
 Si un administrador de conexiones de varios archivos planos hace referencia a varios archivos, todos los archivos deben tener el mismo formato.  
  
 De forma predeterminada, el administrador de conexiones de varios archivos planos establece la longitud de las columnas de cadena en 50 caracteres. En el cuadro de diálogo **Editor del administrador de conexiones de varios archivos planos** , puede evaluar datos de muestra y automáticamente cambiar el tamaño de la longitud de esas columnas para evitar el truncamiento de datos o un ancho de columna excesivo. A menos que cambie el tamaño de la longitud de la columna en un origen de archivo plano o una transformación, la longitud de columna permanece invariable en todo el flujo de datos. Si estas columnas se asignan a columnas de destino más estrechas, aparecen mensajes de advertencia en la interfaz de usuario, y en tiempo de ejecución, se pueden generar errores debido al truncamiento de datos. Puede cambiar el tamaño de las columnas para que sean compatibles con las columnas de destino en el administrador de conexiones de archivos planos, el origen de archivo plano o una transformación. Para modificar la longitud de columnas de salida, establezca el `Length` propiedad de la columna de salida en el **propiedades de entrada y salida** pestaña en el **Editor avanzado** cuadro de diálogo.  
  
 Si actualiza las longitudes de columna en el administrador de conexiones de varios archivos planos una vez que ya ha agregado y configurado el origen de archivo plano que utiliza el administrador de conexiones, no tiene que cambiar manualmente el tamaño de las columnas de salida en el origen de archivo plano. Cuando abre el cuadro de diálogo **Origen de archivo plano** , el origen de archivo plano proporciona una opción para sincronizar los metadatos de columna.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Configuración del administrador de conexiones de varios archivos planos  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Origen de archivo plano](../data-flow/flat-file-source.md)   
 [Destino de archivo plano](../data-flow/flat-file-destination.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  

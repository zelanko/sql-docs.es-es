---
title: Rutas de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: efe52410b491848001fc7e0861e27732d36bc173
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410637"
---
# <a name="integration-services-paths"></a>Rutas de Integration Services
  Una ruta conecta dos componentes en un flujo de datos conectando la salida de un componente de flujo de datos con la entrada de otro componente. Una ruta tiene un origen y un destino. Por ejemplo, si una ruta conecta un origen de OLE DB y una transformación Ordenar, el origen de OLE DB es el origen de la ruta y la transformación Ordenar es el destino de la ruta. El origen es el componente donde se inicia la ruta y el destino es el componente donde finaliza la ruta.  
  
 Si ejecuta un paquete en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede ver los datos en un flujo de datos adjuntando los visores de datos a una ruta. Un visor de datos se puede configurar para mostrar los datos en una cuadrícula. Un visor de datos es una herramienta de depuración útil. Para más información, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="configure-the-path"></a>Configurar la ruta  
 El Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona el cuadro de diálogo **Editor de rutas de flujo de datos** para establecer las propiedades de ruta, ver los metadatos de las columnas de datos que pasan por la ruta y configurar los visores de datos.  
  
 Entre las propiedades configurables de la ruta se incluyen el nombre, descripción y anotación de la ruta. También puede configurar rutas mediante programación. Para obtener más información, vea [Conectar componentes de flujo de datos mediante programación](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Una anotación de ruta muestra el nombre del origen de ruta o el nombre de ruta en la superficie de diseño de la pestaña **Flujo de datos** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Las anotaciones de ruta son similares a las anotaciones que se pueden agregar a los flujos de datos, flujos de control y controladores de eventos. La única diferencia es que una anotación de ruta se adjunta a una ruta, mientras que otras anotaciones aparecen en las pestañas **Flujo de datos**, **Flujo de control**y **Controlador de eventos**del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Los metadatos muestran el nombre, tipo de datos, precisión, escala, longitud, página de códigos y componente de origen de cada columna en la salida del componente anterior. El componente de origen es el componente de flujo de datos que creó la columna. Este componente puede ser el primero en el flujo de datos, o puede no serlo. Por ejemplo, las transformaciones Unión de todo y Ordenar crean sus propias columnas, y son los orígenes de sus columnas de salida. Por otro lado, una transformación Copiar columna puede pasar por columnas sin modificarlas o puede crear nuevas columnas copiando columnas de entrada. La transformación Copiar columna es el componente de origen solamente de las nuevas columnas.  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>Establecer las propiedades de una ruta con el Editor de rutas de flujo de datos
Las rutas conectan dos componentes de flujo de datos. Para poder establecer propiedades de ruta, el flujo de datos debe contener por lo menos dos componentes de flujo de datos conectados.
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, después, haga doble clic en una ruta.  
  
4.  En el **Editor de rutas de flujo de datos**, haga clic en **General**. A partir de este momento puede editar el nombre predeterminado de la ruta y proporcionar una descripción de la ruta. También puede modificar la propiedad PathAnnotation.  
  
5.  Haga clic en **Aceptar**.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  

## <a name="general-page---data-flow-path-editor"></a>Página General, Editor de rutas de flujo de datos
Utilice el cuadro de diálogo **Editor de rutas de flujo de datos** para establecer propiedades de ruta, ver metadatos de columna y administrar los visores de datos adjuntados a la ruta.  
  
 Utilice el nodo **General** del cuadro de diálogo **Editor de rutas de flujo de datos** para nombrar y describir la ruta, y para especificar las opciones de anotación de ruta.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la ruta.  
  
 **ID**  
 El identificador de linaje de la ruta. Esta propiedad es de solo lectura.  
  
 **IdentificationString**  
 La cadena que identifica la ruta. Se automáticamente a partir del nombre especificado con anterioridad.  
  
 **Descripción**  
 Describe la ruta.  
  
 **PathAnnotation**  
 Especificar el tipo de anotación que se va a usar. Elija **Nunca** para deshabilitar anotaciones, **AsNeeded** para habilitar anotaciones a petición, **SourceName** para realizar anotaciones automáticamente utilizando el valor de la opción **SourceName** y **PathName** para realizar anotaciones automáticamente utilizando el valor de la propiedad **Nombre** .  
  
 **DestinationName**  
 Muestra la entrada que es el final de la ruta.  
  
 **SourceName**  
 Muestra la salida que es el inicio de la ruta.  
 
## <a name="metadata-page---data-flow-path-editor"></a>Página Metadatos: Editor de rutas de flujo de datos
Utilice la página **Metadatos** del cuadro de diálogo **Editor de rutas de flujo de datos** para ver los metadatos de las columnas de rutas.  
  
### <a name="options"></a>Opciones  
 **Metadatos de ruta**  
 Muestra los metadatos de columna. Haga clic en los encabezados de columna para ordenar los datos de columna.  
  
 **Nombre**  
 Muestra el nombre de la columna.  
  
 **Tipo de datos**  
 Muestra el tipo de datos de la columna.  
  
 **Precisión**  
 Muestra el número de dígitos de un valor numérico.  
  
 **Escala**  
 Muestra el número de dígitos a la derecha del separador decimal de un valor numérico.  
  
 **Longitud**  
 Muestra la longitud actual de la columna.  
  
 **Página de códigos**  
 Muestra la página de códigos de la columna. El valor **0** indica que la columna no utiliza una página de códigos. Esto se produce cuando los datos están en formato Unicode o tienen un tipo de datos numérico, de fecha o de hora.  
  
 **Posición de criterio de ordenación**  
 Muestra la posición de criterio de ordenación de la columna. El valor **0** indica que la columna no está ordenada.  
  
> [!NOTE]  
>  El prefijo menos (-) indica que el orden de la columna es descendente.  
  
 **Marcas de comparación**  
 Muestra las marcas de comparación que se aplican a la columna.  
  
 **Componente de origen**  
 Muestra el componente de flujo de datos de origen de la columna.  
  
 **Copiar al Portapapeles**  
 Copia los metadatos de la columna al Portapapeles. De forma predeterminada, todas las filas de metadatos se copian en el orden mostrado actualmente.  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>Página Visores de datos: Editor de rutas de flujo de datos
Utilice la página **Visores de datos** del cuadro de diálogo **Editor de rutas de flujo de datos** para administrar los visores de datos que se adjuntan a la ruta.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Muestra los visores de datos.  
  
 **Tipo de visor de datos**  
 Muestra el tipo del visor de datos.  
  
 **Agregar**  
 Haga clic en esta opción para agregar un visor de datos mediante el cuadro de diálogo **Configurar visor de datos** .  
  
 **Eliminar**  
 Haga clic en esta opción para eliminar el visor de datos seleccionado.  
  
 **Configurar**  
 Haga clic en esta opción para configurar un visor de datos seleccionado mediante el cuadro de diálogo **Configurar visor de datos** .  
 
## <a name="path-properties"></a>Path Properties
Los objetos de flujo de datos del modelo de objetos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tienen propiedades comunes y propiedades personalizadas en el nivel del componente, de las entradas y salidas, y de las columnas de entrada y de salida. Muchas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
 En este tema se enumeran y describen las propiedades personalizadas de las rutas de acceso que conectan los objetos del flujo de datos.  
  
### <a name="custom-properties-of-a-path"></a>Propiedades personalizadas de una ruta  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], una ruta de acceso que conecta componentes en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 La tabla siguiente describe las propiedades configurables de las rutas de acceso en un flujo de datos. El motor de flujo de datos también asigna valores a propiedades de solo lectura adicionales no enumeradas aquí.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer (enumeración)|Un valor que indica si una anotación se debería mostrar con la ruta de acceso en el área del diseñador. Los valores posibles son **AsNeeded**, **SourceName**, **PathName**y **Never**. El valor predeterminado es **AsNeeded**.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|La entrada asociada a la ruta de acceso.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|La salida asociada a la ruta de acceso.|  

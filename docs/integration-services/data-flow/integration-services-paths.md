---
title: "Rutas de Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.patheditor.general.f1"
  - "sql13.dts.designer.patheditor.metadata.f1"
  - "sql13.dts.designer.patheditor.visualizers.f1"
helpviewer_keywords: 
  - "rutas de acceso [Integration Services], acerca de rutas de acceso"
  - "flujo de datos [Integration Services], rutas de acceso"
  - "rutas [Integration Services]"
  - "destinos [Integration Services], rutas de acceso"
  - "orígenes [Integration Services], rutas de acceso"
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Rutas de Integration Services
  Una ruta conecta dos componentes en un flujo de datos conectando la salida de un componente de flujo de datos con la entrada de otro componente. Una ruta tiene un origen y un destino. Por ejemplo, si una ruta conecta un origen de OLE DB y una transformación Ordenar, el origen de OLE DB es el origen de la ruta y la transformación Ordenar es el destino de la ruta. El origen es el componente donde se inicia la ruta y el destino es el componente donde finaliza la ruta.  
  
 Si ejecuta un paquete en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede ver los datos en un flujo de datos adjuntando los visores de datos a una ruta. Un visor de datos se puede configurar para mostrar los datos en una cuadrícula. Un visor de datos es una herramienta de depuración útil. Para más información, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## Configuración de la ruta de acceso  
 El Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona el cuadro de diálogo **Editor de rutas de flujo de datos** para establecer las propiedades de ruta, ver los metadatos de las columnas de datos que pasan por la ruta y configurar los visores de datos.  
  
 Entre las propiedades configurables de la ruta se incluyen el nombre, descripción y anotación de la ruta. También puede configurar rutas mediante programación. Para obtener más información, vea [Conectar componentes de flujo de datos mediante programación](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Una anotación de ruta muestra el nombre del origen de ruta o el nombre de ruta en la superficie de diseño de la pestaña **Flujo de datos** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Las anotaciones de ruta son similares a las anotaciones que se pueden agregar a los flujos de datos, flujos de control y controladores de eventos. La única diferencia es que una anotación de ruta se adjunta a una ruta, mientras que otras anotaciones aparecen en las pestañas **Flujo de datos**, **Flujo de control**y **Controlador de eventos**del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Los metadatos muestran el nombre, tipo de datos, precisión, escala, longitud, página de códigos y componente de origen de cada columna en la salida del componente anterior. El componente de origen es el componente de flujo de datos que creó la columna. Este componente puede ser el primero en el flujo de datos, o puede no serlo. Por ejemplo, las transformaciones Unión de todo y Ordenar crean sus propias columnas, y son los orígenes de sus columnas de salida. Por otro lado, una transformación Copiar columna puede pasar por columnas sin modificarlas o puede crear nuevas columnas copiando columnas de entrada. La transformación Copiar columna es el componente de origen solamente de las nuevas columnas.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden establecer en el cuadro de diálogo **Editor de rutas de flujo de datos** , haga clic en uno de los siguientes temas:  
  
-   [Editor de rutas de flujo de datos &#40;página General&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(General%20Page\).md)  
  
-   [Editor de rutas de flujo de datos &#40;página Metadatos&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(Metadata%20Page\).md)  
  
-   [Editor de rutas de flujo de datos &#40;página Visores de datos&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(Data%20Viewers%20Page\).md)  
  
 Para obtener más información acerca de las propiedades que puede establecer mediante programación, vea [Path Properties](../Topic/Path%20Properties.md).  
  
## Tareas relacionadas  
  
-   [Ver los metadatos de rutas con el Editor de rutas de flujo de datos](../Topic/View%20Path%20Metadata%20in%20the%20Data%20Flow%20Path%20Editor.md)  
  
-   [Conectar componentes de un flujo de datos](../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
## Vea también  
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
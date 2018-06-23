---
title: Conectar componentes con rutas de acceso | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5152147f82d1d413806eeb8f9644e70af9a04828
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107695"
---
# <a name="connect-components-with-paths"></a>Conectar componentes con rutas de acceso
  El flujo de datos de un paquete se genera en la superficie de diseño de la pestaña **Flujo de datos** en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Si un flujo de datos contiene dos componentes de flujo de datos, puede conectar ambos conectando la salida de un origen o transformación con la entrada de una transformación o destino. El conector entre dos componentes de flujo de datos se denomina ruta.  
  
 El siguiente diagrama muestra un flujo de datos simple con un componente de origen, dos transformaciones, un componente de destino y las rutas que los conectan.  
  
 ![Flujo de datos](media/mw-dts-08.gif "flujo de datos")  
  
 Una vez conectados dos componentes, puede ver los metadatos de los datos que se mueven por la ruta y las propiedades de la ruta en el **Editor de rutas de flujo de datos**. Para más información, consulte [Integration Services Paths](data-flow/integration-services-paths.md).  
  
 También puede agregar visores de datos a las rutas. Un visor de datos permite ver los datos que se mueven entre los componentes de flujo de datos cuando se ejecuta el paquete.  
  
### <a name="to-connect-components-in-a-data-flow"></a>Para conectar los componentes de un flujo de datos  
  
-   [Conectar componentes de un flujo de datos](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-path-properties"></a>Para establecer las propiedades de la ruta  
  
-   [Establecer las propiedades de una ruta de acceso mediante el Editor de rutas de flujo de datos](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>Para ver metadatos de ruta  
  
-   [Ver los metadatos de ruta de acceso en el Editor de rutas de flujo de datos](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>Para ver metadatos de ruta  
  
-   [Agregar un visor de datos a un flujo de datos](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="see-also"></a>Vea también  
 [Tarea Flujo de datos](control-flow/data-flow-task.md)   
 [Flujo de datos](data-flow/data-flow.md)   
 [Transformación de datos con transformaciones](data-flow/transformations/transform-data-with-transformations.md)   
 [Control de errores en los datos](data-flow/error-handling-in-data.md)  
  
  
---
title: "Editor de destino de procesamiento de dimensiones (página Administrador de conexiones) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e7ca96a91f35b88ea344fa2ad63f61f52fc95e7
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>Editor de destino de procesamiento de dimensiones (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de procesamiento de dimensiones** para especificar una conexión a un proyecto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obtener más información acerca del destino de procesamiento de dimensiones, vea [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opciones  
 **Connection manager**  
 Seleccione un administrador de conexiones existente de la lista, o haga clic en **Nuevo** para crear un nuevo administrador de conexiones.  
  
 **Nuevo**  
 Cree una nueva conexión mediante el cuadro de diálogo **Agregar administrador de conexiones con Analysis Services** .  
  
 **Lista de dimensiones disponibles**  
 Seleccione la dimensión para procesar.  
  
 **Método de procesamiento**  
 En la lista, seleccione el método de procesamiento a aplicar a la dimensión seleccionada. El valor predeterminado de esta opción es **Completa**.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar (incremental)**|Realiza un procesamiento incremental de la dimensión.|  
|**Completa**|Realiza un procesamiento completo de la dimensión.|  
|**Update**|Realiza un procesamiento actualizado de la dimensión.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de procesamiento de dimensiones &#40; Página Asignaciones &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)   
 [Editor de destino de procesamiento de dimensiones &#40; Página avanzadas &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-advanced-page.md)  
  
  

---
title: Editor de destino de procesamiento de dimensiones (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c34da1807f405c25ec071bb94232c3647b7efecd
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429472"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>Editor de destino de procesamiento de dimensiones (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de procesamiento de dimensiones** para especificar una conexión a un proyecto de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obtener más información acerca del destino de procesamiento de dimensiones, vea [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones**  
 Seleccione un administrador de conexiones existente de la lista, o haga clic en **Nuevo** para crear un nuevo administrador de conexiones.  
  
 **Nuevo**  
 Permite crear una conexión con el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** .  
  
 **Lista de dimensiones disponibles**  
 Seleccione la dimensión para procesar.  
  
 **Método de procesamiento**  
 En la lista, seleccione el método de procesamiento a aplicar a la dimensión seleccionada. El valor predeterminado de esta opción es **Completa**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Agregar (incremental)**|Realiza un procesamiento incremental de la dimensión.|  
|**Completa**|Realiza un procesamiento completo de la dimensión.|  
|**Update**|Realiza un procesamiento actualizado de la dimensión.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página asignaciones&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página Avanzadas&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  

---
title: Editor de destino de procesamiento de particiones (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b86348e6e7fa8331697c4a0aa3b23a494ae54a5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374763"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>Editor de destino de procesamiento de particiones (página Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de procesamiento de particiones** para especificar una conexión a un proyecto de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obtener más información acerca del destino de procesamiento de particiones, vea [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Las tareas aquí descritas no se aplican a los modelos tabulares de Analysis Services.  No se pueden asignar las columnas de entrada a las de partición para los modelos tabulares. En su lugar puede usar la tarea Ejecutar DDL de Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) para procesar la partición.  
  
## <a name="options"></a>Opciones  
 **Connection manager**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Permite crear una conexión con el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** .  
  
 **Lista de particiones disponibles**  
 Seleccione la partición para procesar.  
  
 **Método de procesamiento**  
 Seleccione el método de procesamiento. El valor predeterminado de esta opción es **Completa**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Agregar (incremental)|Realiza un procesamiento incremental de la partición.|  
|Completo|Realiza un procesamiento completo de la partición.|  
|Solo datos|Realiza un procesamiento de actualización de la partición.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de procesamiento de particiones &#40;página Asignaciones&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [Editor de destino de procesamiento de particiones &#40;página Avanzadas&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  

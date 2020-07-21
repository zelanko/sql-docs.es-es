---
title: Editor de bucles foreach (página asignaciones de variables) | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 043077496e1ec1a1cad147725d7f722364f6a54c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425502"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Editor de bucles Foreach (página Asignaciones de variables)
  Use la página **Asignaciones de variables** del cuadro de diálogo **Editor de bucles Foreach** para asignar variables al valor de la colección. El valor de la variable se actualiza con los valores de la colección en cada iteración del bucle.  
  
 Para obtener más información acerca de cómo utilizar el contenedor de bucles Foreach en un paquete de Integration Services, vea [Foreach Loop Container](control-flow/foreach-loop-container.md) . Para saber cómo se configura, vea [Configurar un contenedor de bucles Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tutorial creación de un tutorial de paquete ETL sencillo incluye una lección que le enseña a agregar y configurar un bucle foreach.  
  
## <a name="options"></a>Opciones  
 **Variable**  
 Seleccione una variable existente o haga clic en \<**New variable...**> para crear una nueva variable.  
  
> [!NOTE]  
>  Una vez asignada una variable, se agregará automáticamente una nueva fila a la lista **Variable**.  
  
 **Temas relacionados**: [Integration Services &#40;SSIS&#41; variables](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
 **Índice**  
 Si utiliza el enumerador de elementos para Foreach, especifique el índice de la columna en el valor de la colección para asignarlo a la variable. Si utiliza otros tipos de enumeradores, el índice será de solo lectura.  
  
> [!NOTE]  
>  El índice se basa en 0.  
  
 **Temas relacionados**: crear [bucles entre archivos y tablas de Excel mediante un contenedor de bucles foreach](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **Eliminar**  
 Seleccione una variable y haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de bucles foreach &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Página colección de &#40;del editor de bucles foreach&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Contenedor de bucles For](control-flow/for-loop-container.md)  
  
  

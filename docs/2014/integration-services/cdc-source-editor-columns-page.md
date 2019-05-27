---
title: Editor de origen de CDC (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 980b9cf22e2c50cd1de3eb90a06e6496c01cc093
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061032"
---
# <a name="cdc-source-editor-columns-page"></a>Editor de origen de CDC (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de origen de CDC** para asignar una columna de salida a cada columna externa (origen).  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Columnas del Editor de origen de CDC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el origen de CDC.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de CDC.  
  
3.  En el **Editor de origen de CDC**, haga clic en **Columnas**.  
  
## <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Lista de las columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas. Seleccione las columnas que se van a usar en el origen. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que se seleccionan.  
  
 **Columna externa**  
 Vista de las columnas externas (origen) en el orden en que se verán cuando configure componentes que usen datos del origen de CDC. Para cambiar este orden, en primer lugar borre las columnas seleccionadas en la lista **Columnas externas disponibles** y, a continuación, seleccione las columnas externas en la lista en un orden diferente. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que las haya seleccionado.  
  
 **Columna de salida**  
 Especifique un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir cualquier nombre único y descriptivo. El nombre especificado se muestra en el Diseñador de SSIS.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Editor de origen de CDC &#40;página Salida de error&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  

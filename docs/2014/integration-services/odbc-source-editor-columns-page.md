---
title: Editor de origen ODBC (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 51897dbc1b7cde8707e28678d8de7f3cd7913e81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144671"
---
# <a name="odbc-source-editor-columns-page"></a>Editor de origen de ODBC (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de orígenes ODBC** para asignar una columna de salida a cada columna externa (origen).  
  
 Para obtener más información acerca del origen de ODBC, vea [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Columnas del Editor de origen de ODBC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen ODBC.  
  
3.  En el **Editor de origen de ODBC**, haga clic en **Columnas**.  
  
## <a name="options"></a>Opciones  
  
### <a name="available-external-columns"></a>Columnas externas disponibles  
 Lista de las columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas. Seleccione las columnas que se van a usar desde el origen. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que se seleccionan.  
  
 Active la casilla **Seleccionar todas** para seleccionar todas las columnas.  
  
### <a name="external-column"></a>Columna externa  
 Vista de las columnas externas (origen) en el orden en que se verán cuando configure los componentes que usan datos del origen de ODBC.  
  
### <a name="output-column"></a>Columna de salida  
 Especifique un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre especificado se muestra en el Diseñador de SSIS.  
  
## <a name="see-also"></a>Vea también  
 [Editor de orígenes ODBC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de orígenes ODBC &#40;página de salida de Error&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  

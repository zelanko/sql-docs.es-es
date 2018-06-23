---
title: Editor de origen ODBC (página columnas) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c81948bfcb6d0c2c523d563e850e9466ae45679a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199938"
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
 [Editor de origen ODBC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de origen ODBC &#40;página de salida de Error&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
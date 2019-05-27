---
title: Editor de origen ODBC (página salida de Error) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b19a94e71eaef45184c1777ce299809b2b2d7f8d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057128"
---
# <a name="odbc-source-editor-error-output-page"></a>Editor de origen de ODBC (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen de ODBC** para seleccionar las opciones de control de errores.  
  
 Para obtener más información acerca del origen de ODBC, vea [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Salida de error del Editor de origen de ODBC**  
  
-   En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el origen de ODBC.  
  
-   En el **Editor de origen de ODBC**, haga clic en **Salida de error**.  
  
## <a name="options"></a>Opciones  
  
### <a name="inputoutput"></a>Entrada/salida  
 Muestra el nombre del origen de datos.  
  
### <a name="column"></a>columna  
 No se usa.  
  
### <a name="error"></a>Error  
 Seleccione la forma en la que el origen de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="truncation"></a>Truncamiento  
 Seleccione la forma en la que el origen de ODBC debe controlar el truncamiento en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="description"></a>Descripción  
 No se usa.  
  
### <a name="set-this-value-to-selected-cells"></a>Establecer este valor en las celdas seleccionadas  
 Seleccione cómo el origen de ODBC va a controlar todas las celdas seleccionadas cuando se produzca un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="apply"></a>Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
## <a name="error-handling-options"></a>Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el origen de ODBC controla errores y truncamientos.  
  
### <a name="fail-component"></a>Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
### <a name="ignore-failure"></a>Omitir error  
 Se omite el error o el truncamiento.  
  
### <a name="redirect-flow"></a>Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del origen de ODBC. Para más información, consulte [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="see-also"></a>Vea también  
 [Editor de orígenes ODBC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de orígenes ODBC &#40;página Columnas&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)  
  
  

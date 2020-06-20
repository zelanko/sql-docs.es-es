---
title: Editor de origen de ODBC (página salida de error) | Microsoft Docs
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
ms.openlocfilehash: 4653b963bd5e8f997832f153a09d87aaeef9c39c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965005"
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
  
### <a name="column"></a>Columna  
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
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Este es el comportamiento predeterminado.  
  
### <a name="ignore-failure"></a>Omitir error  
 Se omite el error o el truncamiento.  
  
### <a name="redirect-flow"></a>Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del origen de ODBC. Para más información, consulte [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="see-also"></a>Consulte también  
 [Editor de origen de ODBC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de orígenes ODBC &#40;página Columnas&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)  
  
  

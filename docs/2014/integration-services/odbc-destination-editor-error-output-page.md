---
title: Editor de destino de ODBC (página salida de Error) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fba1021e4152d5d810b54d29417864936f067800
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183375"
---
# <a name="odbc-destination-editor-error-output-page"></a>Editor de destinos de ODBC (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de destinos de ODBC** para seleccionar las opciones de control de errores.  
  
 Para obtener más información acerca del destino de ODBC, vea [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Para abrir la página Salida de error del Editor de destinos de ODBC**  
  
## <a name="task-list"></a>Lista de tareas  
  
-   En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el destino de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el destino de ODBC.  
  
-   En el **Editor de destinos de ODBC**, haga clic en **Salida de error**.  
  
## <a name="options"></a>Opciones  
  
### <a name="inputoutput"></a>Entrada/salida  
 Muestra el nombre del origen de datos.  
  
### <a name="column"></a>columna  
 No se usa.  
  
### <a name="error"></a>Error  
 Seleccione la forma en la que el destino de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="truncation"></a>Truncamiento  
 Seleccione la forma en la que el destino de ODBC debe controlar los truncamientos en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="description"></a>Descripción  
 Muestra una descripción del error.  
  
### <a name="set-this-value-to-selected-cells"></a>Establecer este valor en las celdas seleccionadas  
 Seleccione la forma en la que el destino de ODBC controla todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### <a name="apply"></a>Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
## <a name="error-handling-options"></a>Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el destino de ODBC controla errores y truncamientos.  
  
### <a name="fail-component"></a>Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
### <a name="ignore-failure"></a>Omitir error  
 Se omite el error o el truncamiento.  
  
### <a name="redirect-flow"></a>Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del destino de ODBC. Para obtener más información, vea Destino de ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../../2014/integration-services/odbc-destination-editor-connection-manager-page.md)   
 [Editor de destino de ODBC &#40;página asignaciones&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)  
  
  

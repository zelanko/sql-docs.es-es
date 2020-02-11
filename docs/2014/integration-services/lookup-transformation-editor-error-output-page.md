---
title: Editor de transformación búsqueda (página salida de error) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12f1a73c1d21986d2089878bfe9d29dd4450f222
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057856"
---
# <a name="lookup-transformation-editor-error-output-page"></a>Editor de transformación Búsqueda (página Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de transformación Búsqueda** para especificar las opciones de control de errores.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre de la entrada.  
  
 **Columna**  
 No se usa.  
  
 **Error**  
 Especifica el tipo de error que se producirá al administrar filas sin entradas coincidentes en el conjunto de datos de referencia:  
  
-   Pasar por alto el error y dirigir las filas a un resultado.  
  
-   Redirigir las filas a una salida de error.  
  
-   Producir un error en el componente.  
  
 Esta opción no está disponible al seleccionar **Redirigir filas a resultados no coincidentes** en la lista **Especificar cómo tratar las filas sin entradas coincidentes** . La lista está en la página **General** del cuadro de diálogo **Editor de transformación Búsqueda** .  
  
 **Temas relacionados:** [control de errores en los datos](data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 Especifica lo que debe suceder cuando se produce un truncamiento de datos:  
  
-   Pasar por alto el error.  
  
-   Redirigir la fila.  
  
-   Producir un error en el componente.  
  
 **Descripción**  
 Muestra la descripción de la operación.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Especifica qué debe suceder a todas las celdas seleccionadas cuando se produce un error o truncación:  
  
-   Pasar por alto el error.  
  
-   Redirigir la fila.  
  
-   Producir un error en el componente.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  

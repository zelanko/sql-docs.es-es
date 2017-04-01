---
title: "Editor de transformaci&#243;n B&#250;squeda (p&#225;gina Salida de error) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.lookuptransformation.erroroutput.f1"
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Editor de transformaci&#243;n B&#250;squeda (p&#225;gina Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de transformación Búsqueda** para especificar las opciones de control de errores.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opciones  
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
  
 **Temas relacionados:** [Control de errores en los datos](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 **Truncamiento**  
 Especifica lo que debe suceder cuando se produce un truncamiento de datos:  
  
-   Pasar por alto el error.  
  
-   Redirigir la fila.  
  
-   Producir un error en el componente.  
  
 **Description**  
 Muestra la descripción de la operación.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Especifica qué debe suceder a todas las celdas seleccionadas cuando se produce un error o truncación:  
  
-   Pasar por alto el error.  
  
-   Redirigir la fila.  
  
-   Producir un error en el componente.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  
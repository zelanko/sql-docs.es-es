---
title: "Convertir el tipo de datos mediante el uso de transformación conversión de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 3a6de227fc2fd0e93abfc9e8ac5300dbf0a137ac
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="convert-data-type-by-using-data-conversion-transformation"></a>Convertir el tipo de datos mediante el uso de transformación conversión de datos
  Para agregar y configurar una transformación Conversión de datos, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen.  
  
### <a name="to-convert-data-to-a-different-data-type"></a>Para convertir datos en un tipo de datos diferente  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** , y luego, desde el **cuadro de herramientas**, arrastre la transformación Conversión de datos a la superficie de diseño.  
  
4.  Conecte la transformación Conversión de datos al flujo de datos arrastrando el conector desde el origen o la transformación anterior a la transformación Conversión de datos.  
  
5.  Haga doble clic en la transformación Conversión de datos.  
  
6.  En el cuadro de diálogo **Editor de transformación Conversión de datos** , en la tabla **Columnas de entrada disponibles** , active la casilla que aparece junto a las columnas cuyo tipo de datos quiere convertir.  
  
    > [!NOTE]  
    >  Puede aplicar varias conversiones de datos a una columna de entrada.  
  
7.  Opcionalmente, modifique los valores predeterminados en la columna **Alias de salida** .  
  
8.  En la lista **Tipo de datos** , seleccione el nuevo tipo de datos para la columna. El tipo de datos predeterminado es el tipo de datos de la columna de entrada.  
  
9. Opcionalmente, según el tipo de datos seleccionado, actualice los valores en las columnas **Longitud**, **Precisión**, **Escala**, y **Página de códigos** .  
  
10. Para configurar la salida de error, haga clic en **Configurar la salida de errores**. Para más información, consulte [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Haga clic en **Aceptar**.  
  
12. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Transformación conversión de datos](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tipos de datos de Integration Services](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Tarea flujo de datos](../../../integration-services/control-flow/data-flow-task.md)  
  
  

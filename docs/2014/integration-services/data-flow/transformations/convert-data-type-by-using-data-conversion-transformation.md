---
title: Convertir datos en un tipo de datos diferente mediante la transformación conversión de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13faac66894298c4d08cd40a1eab9d3d823fd0ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900875"
---
# <a name="convert-data-to-a-different-data-type-by-using-the-data-conversion-transformation"></a>Convertir datos en un tipo de datos diferente mediante la transformación Conversión de datos
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
  
10. Para configurar la salida de error, haga clic en **Configurar la salida de errores**. Para obtener más información, vea [Configurar una salida de error en un componente de flujo de datos](../../configure-an-error-output-in-a-data-flow-component.md).  
  
11. Haga clic en **OK**.  
  
12. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Data Conversion Transformation](data-conversion-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)   
 [Rutas de Integration Services](../integration-services-paths.md)   
 [Tipos de datos de Integration Services](../integration-services-data-types.md)   
 [Tarea Flujo de datos](../../control-flow/data-flow-task.md)  
  
  

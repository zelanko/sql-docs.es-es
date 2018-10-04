---
title: Convertir datos a un tipo de datos diferente mediante la transformación conversión de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa23f7b520fd224323122f7f3674bbafd25eb53c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069165"
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
  
10. Para configurar la salida de error, haga clic en **Configurar la salida de errores**. Para más información, vea [Configurar una salida de error en un componente de flujo de datos](../../configure-an-error-output-in-a-data-flow-component.md).  
  
11. Haga clic en **Aceptar**.  
  
12. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Transformación conversión de datos](data-conversion-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)   
 [Rutas de Integration Services](../integration-services-paths.md)   
 [Tipos de datos de Integration Services](../integration-services-data-types.md)   
 [Tarea de flujo de datos] ((.. /.. /Control-Flow/Data-Flow-Task.MD)  
  
  

---
title: Identificar filas de datos similares mediante la transformación Agrupación aproximada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 991940b819e3d72fcb7b94eb031b0e40b7102667
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939546"
---
# <a name="identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation"></a>Identificar filas de datos similares mediante la transformación Agrupación aproximada
  Para agregar y configurar una transformación Agrupación aproximada, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen.  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>Para implementar la transformación Agrupación aproximada en un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre la transformación Agrupación aproximada a la superficie de diseño.  
  
4.  Conecte la transformación Agrupación aproximada al flujo de datos arrastrando el conector desde el origen de datos o una transformación anterior a la transformación Agrupación aproximada.  
  
5.  Haga doble clic en la transformación Agrupación aproximada.  
  
6.  En el cuadro de diálogo **Editor de transformación Agrupación aproximada** , en la pestaña **Administrador de conexiones** , seleccione un administrador de conexiones OLE DB que se conecte con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  La transformación requiere una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para crear tablas e índices temporales.  
  
7.  Haga clic en la pestaña **Columnas** y en la lista **Columnas de entrada disponibles** , active la casilla de las columnas de entrada que se deben usar para identificar filas similares en el conjunto de datos.  
  
8.  Active la casilla de la columna **Paso a través** para identificar las columnas de entrada que pasan a través de la salida de transformación. Las columnas de paso a través no se incluyen en el proceso de identificación de filas duplicadas.  
  
    > [!NOTE]  
    >  Las columnas de entrada que se usan para agrupar se seleccionan automáticamente como columnas de paso a través, y no se puede eliminar su selección mientras se usan para la agrupación.  
  
9. Opcionalmente, actualice los nombres de las columnas de salida en la columna **Alias de salida** .  
  
10. También puede actualizar los nombres de las columnas limpias en la columna **Alias de salida de grupo** .  
  
    > [!NOTE]  
    >  Los nombres predeterminados de las columnas son los nombres de las columnas de entrada con el sufijo "_clean".  
  
11. Opcionalmente, actualice el tipo de coincidencia que se debe usar en la columna **Tipo de coincidencia** .  
  
    > [!NOTE]  
    >  Al menos una columna debe usar coincidencia aproximada.  
  
12. Especifique las columnas de nivel de similitud mínima en la columna **Similitud mínima** . El valor debe estar entre 0 y 1. Cuanto más cercano sea el valor a 1, más similares deberán ser los valores en las columnas de entrada para formar un grupo. Una similitud mínima de 1 indica una coincidencia exacta.  
  
13. Opcionalmente, actualice los nombres de las columnas de similitud en la columna **Alias de salida de similitud** .  
  
14. Para especificar el manejo de números en valores de datos, actualice los valores en la columna **Números** .  
  
15. Para especificar la manera en que la transformación compara los datos de cadenas en una columna, modifique la selección predeterminada de las opciones de comparación en la columna **Marcas de comparación** .  
  
16. Haga clic en la pestaña **Avanzadas** para modificar los nombres de las columnas que la transformación agrega a la salida para el identificador de filas únicas (_key_in), el identificador de filas duplicadas (_key_out) y el valor de similitud (_score).  
  
17. Opcionalmente, ajuste el umbral de similitud moviendo la barra del control deslizante.  
  
18. También puede desactivar las casillas de delimitadores de token para omitir los delimitadores en los datos.  
  
19. Haga clic en **OK**.  
  
20. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)   
 [Rutas de Integration Services](../integration-services-paths.md)   
 [Tarea Flujo de datos](../../control-flow/data-flow-task.md)  
  
  

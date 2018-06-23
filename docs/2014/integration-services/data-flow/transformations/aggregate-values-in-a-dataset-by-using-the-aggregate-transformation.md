---
title: Agregar valores en un conjunto de datos mediante la transformación Agregado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 21f4e4749518036a1c2c40496102617c556f6aec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200999"
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>Agregar valores en un conjunto de datos mediante la transformación Agregado
  Para agregar y configurar una transformación Agregado, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>Para agregar valores en un conjunto de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **Cuadro de herramientas**, arrastre la transformación Agregado a la superficie de diseño.  
  
4.  Conecte la transformación Agregado al flujo de datos arrastrando el conector desde un origen o una transformación anterior a la transformación Agregado.  
  
5.  Haga doble clic en la transformación.  
  
6.  En el cuadro de diálogo **Editor de transformación Agregado** , haga clic en la pestaña **Agregaciones** .  
  
7.  En la lista **Columnas de entrada disponibles** , active la casilla situada junto a las columnas en las que desea agregar valores. Las columnas seleccionadas aparecen en la tabla.  
  
    > [!NOTE]  
    >  Puede seleccionar una columna muchas veces, aplicando varias transformaciones a la columna. Para identificar de manera exclusiva las agregaciones, se anexa un número al nombre predeterminado del alias de salida de la columna.  
  
8.  Opcionalmente, modifique el valor en las columnas **Alias de salida** .  
  
9. Para cambiar la operación de agregación predeterminada, **GROUP BY**, seleccione otra operación en la lista **Operación** .  
  
10. Para cambiar la comparación predeterminada, seleccione las marcas de comparación individuales enumeradas en la columna **Marcas de comparación** . De forma predeterminada, una comparación omite la distinción entre mayúsculas y minúsculas, el tipo de kana, los caracteres sin espacio y el ancho de caracteres.  
  
11. Opcionalmente, para la agregación **Count distinct** , especifique un número exacto de valores distintos en la columna **Claves Count Distinct** , o seleccione un recuento aproximado en la columna **Escala Count Distinct** .  
  
    > [!NOTE]  
    >  Al proporcionar el número de valores distintos, sea exacto o aproximado, se optimiza el rendimiento, dado que la transformación puede asignar previamente una cantidad apropiada de memoria para realizar el trabajo.  
  
12. Opcionalmente, haga clic en **Avanzado** y actualice el nombre de la salida de transformación Agregado. Si las agregaciones incluyen una `Group By` operación, puede seleccionar un recuento aproximado de valores de clave de agrupación la **escala de claves** columna o especifique un número exacto de valores de clave de agrupación la **claves** columna.  
  
    > [!NOTE]  
    >  Al proporcionar el número de valores distintos, sea exacto o aproximado, se optimiza el rendimiento, dado que la transformación puede asignar previamente una cantidad apropiada de memoria para realizar el trabajo.  
  
    > [!NOTE]  
    >  Las opciones **Escala de claves** y **Claves** se excluyen mutuamente. Si escribe valores en ambas columnas, se utiliza el valor más grande en **Escala de claves** o en **Claves** .  
  
13. También puede hacer clic en la pestaña **Avanzado** y establecer los atributos que se aplican a la optimización de todas las operaciones que realiza la transformación Agregado.  
  
14. Haga clic en **Aceptar**.  
  
15. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Transformación agregado](aggregate-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)   
 [Rutas de Integration Services](../integration-services-paths.md)   
 [Tarea de flujo de datos] ((.. /.. /Control-Flow/Data-Flow-Task.MD)  
  
  
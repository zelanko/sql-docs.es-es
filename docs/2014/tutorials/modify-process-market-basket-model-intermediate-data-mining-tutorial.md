---
title: Modificar y procesar el modelo de cesta de la compra (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63301372"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>Modificar y procesar el modelo de cesta de la compra (Tutorial intermedio de minería de datos)
  Antes de procesar el modelo de minería de datos de asociación que creó, debe cambiar los valores predeterminados de dos de los parámetros: *compatibilidad* y *probabilidad*.  
  
-   La *compatibilidad* define el porcentaje de casos en los que debe existir una regla antes de que se considere válida. Especificará que una regla se debe encontrar en un uno por ciento de casos al menos.  
  
-   La *probabilidad* define la probabilidad de que una asociación sea antes de que se considere válida. Considerará cualquier asociación con una probabilidad de al menos el 10 por ciento.  
  
 Para obtener más información sobre los efectos de aumentar o reducir la compatibilidad y la probabilidad, consulte [referencia técnica del algoritmo de Asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 Después de definir la estructura y los parámetros para el modelo de minería de datos **Association** , procesará el modelo.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Para ajustar los parámetros del modelo Association  
  
1.  Abra la pestaña **modelos de minería** de datos del diseñador de minería de datos.  
  
2.  Haga clic con el botón secundario en la columna **Asociación** de la cuadrícula en el diseñador y seleccione **establecer parámetros de algoritmo para abrir el cuadro de diálogo parámetros de algoritmo** .  
  
3.  En la columna **valor** del cuadro de diálogo **parámetros de algoritmo** , establezca los parámetros siguientes:  
  
     MINIMUM_PROBABILITY = 0,1  
  
     MINIMUM_SUPPORT = 0,01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>Para procesar el modelo de minería de datos  
  
1.  En el menú modelo de minería [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]de **datos** de, seleccione **procesar estructura de minería de datos y todos los modelos.**  
  
2.  En la advertencia en la que se pregunta si desea generar e implementar el proyecto, haga clic en **Sí**.  
  
     Se abrirá el cuadro **de diálogo procesar estructura de minería de datos** .  
  
3.  Haga clic en **Ejecutar**.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo. El procesamiento de la nueva estructura y del nuevo modelo puede tardar algún tiempo.  
  
4.  Cuando se complete el proceso, haga clic en **Cerrar** para salir del cuadro de diálogo **Progreso del proceso** .  
  
5.  Vuelva a hacer clic en **cerrar** para salir del cuadro **de diálogo procesar estructura de minería de datos-Asociación** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar los modelos de cesta de la compra &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  

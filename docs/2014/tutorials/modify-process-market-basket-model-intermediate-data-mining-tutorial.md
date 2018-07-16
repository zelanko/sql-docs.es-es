---
title: Modificar y procesar el modelo de cesta (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1f0fe6899be3f9828a8ba9d91f2c9abf7ba48b6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246125"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>Modificar y procesar el modelo de cesta de la compra (Tutorial intermedio de minería de datos)
  Antes de procesar el modelo de minería de datos de asociación que creó, debe cambiar los valores predeterminados de dos de los parámetros: *soporte* y *probabilidad*.  
  
-   *Compatibilidad con* define el porcentaje de casos en que una regla debe existir antes de que se considere válido. Especificará que una regla se debe encontrar en un uno por ciento de casos al menos.  
  
-   *Probabilidad* define cómo es probable que una asociación debe estar antes de que se considera válido. Considerará cualquier asociación con una probabilidad de al menos el 10 por ciento.  
  
 Para obtener más información sobre los efectos de aumentar o disminuir la probabilidad y compatibilidad, consulte [Microsoft Association Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 Después de haber definido la estructura y los parámetros para el **asociación** modelo de minería de datos, procesará el modelo.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Para ajustar los parámetros del modelo Association  
  
1.  Abra el **modelos de minería de datos** ficha del Diseñador de minería de datos.  
  
2.  Haga clic en el **asociación** columna en la cuadrícula en el diseñador y seleccione **establecer parámetros de algoritmo para abrir los parámetros del algoritmo** cuadro de diálogo.  
  
3.  En el **valor** columna de la **parámetros de algoritmo** diálogo cuadro, establezca los parámetros siguientes:  
  
     MINIMUM_PROBABILITY = 0,1  
  
     MINIMUM_SUPPORT = 0,01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>Para procesar el modelo de minería de datos  
  
1.  En el **Mining Model** menú de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], seleccione **procesar estructura de minería de datos y todos los modelos.**  
  
2.  En la advertencia en la que se pregunta si desea generar e implementar el proyecto, haga clic en **Sí**.  
  
     El **procesar estructura de minería de datos - Association** abre el cuadro de diálogo.  
  
3.  Haga clic en **Ejecutar**.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo. El procesamiento de la nueva estructura y del nuevo modelo puede tardar algún tiempo.  
  
4.  Cuando se complete el proceso, haga clic en **Cerrar** para salir del cuadro de diálogo **Progreso del proceso** .  
  
5.  Haga clic en **cerrar** nuevo para salir del **procesar estructura de minería de datos - Association** cuadro de diálogo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar los modelos Market Basket &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  

---
title: Con la obtención de detalles en datos de estructura (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec32e6f46f63c6de342b6b4cab63bb8e6556bfb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198355"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>Usar la obtención de detalles en datos de estructura (Tutorial básico de minería de datos)
  Como parte de su campaña de publicidad [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] está enviando un formulario a los clientes potenciales de entre 34 y 40 años de edad demográficos. El departamento de marketing ha decidido que les gustaría también enviar el formulario a los clientes que compraron bicicletas de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] hace más de cinco años. En esta lección, identificará los clientes con bicicletas anteriores y recuperará su información de contacto. Esta información no está incluida en el modelo, pero se incluye en la estructura. Para recuperar la información de contacto, primero se asegurará de que la obtención de detalles está habilitada para la estructura y, a continuación, la utilizará para revelar los nombres y direcciones de los clientes objetivo.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Para habilitar la obtención de detalles en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el **modelos de minería de datos** ficha del Diseñador de minería de datos, haga clic en el **TM_Decision_Tree** del modelo y seleccione **propiedades**.  
  
2.  En las ventanas Propiedades, haga clic en **AllowDrillThrough**y seleccione **True**.  
  
3.  En la pestaña Modelos de minería de datos, haga clic con el botón secundario en el modelo y seleccione **Procesar modelo**.  
  
 Para obtener más información, consulte [consultas de obtención de detalles &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para ver los datos de obtención de detalles de un modelo de minería de datos  
  
1.  En el Diseñador de minería de datos, haga clic en la pestaña **Visor de modelo de minería de datos** .  
  
2.  Seleccione el modelo **TM_Decision_Tree** en la lista **Modelo de minería de datos** .  
  
3.  Cambiar el **en segundo plano** valor `1`. De esta forma, se muestra solo la parte del modelo que está relacionada con los clientes que compraron bicicletas.  
  
4.  En la lista **Visor** , seleccione Visor de árboles de Microsoft. De esta manera, se forzará la actualización del visor con las condiciones de filtro. A continuación, busque el **Age > = 34 y < 41** con el botón secundario en el nodo y el nodo.  
  
5.  Seleccione **Obtener detalles**y después **Columnas de modelo y estructura** para abrir la ventana **Obtener detalles** .  
  
6.  Desplácese a la columna **Structure.Date First Purchase** para ver la fecha de compra de las bicicletas anteriores.  
  
7.  Para copiar los datos en el Portapapeles, haga clic con el botón secundario en cualquier fila de la tabla y seleccione **Copiar todo.**  
  
 Felicidades, ha completado el Tutorial básico de minería de datos. Ahora que conoce más las herramientas de minería de datos, recomendamos que también complete el Tutorial intermedio de minería de datos, que demuestra cómo crear modelos de pronóstico, análisis de la cesta de la compra y agrupación en clústeres de secuencia.  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Crear predicciones &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  

---
title: Usar la obtención de detalles en datos de estructura (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745546"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>Usar la obtención de detalles en datos de estructura (Tutorial básico de minería de datos)
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] está enviando un formulario a los clientes potenciales de entre 34 y 40 años de edad como parte de su campaña de publicidad. El departamento de marketing ha decidido que quieren enviar también el formulario a los clientes que compraron bicicletas de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] hace más de cinco años. En esta lección, identificará los clientes con bicicletas anteriores y recuperará su información de contacto. Esta información no está incluida en el modelo, pero se incluye en la estructura. Para recuperar la información de contacto, primero se asegurará de que la obtención de detalles está habilitada para la estructura y, a continuación, la utilizará para revelar los nombres y direcciones de los clientes objetivo.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Para habilitar la obtención de detalles en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón secundario en el modelo **TM_Decision_Tree** y seleccione **Propiedades**.  
  
2.  En las ventanas Propiedades, haga clic en **AllowDrillThrough**y seleccione **True**.  
  
3.  En la pestaña Modelos de minería de datos, haga clic con el botón secundario en el modelo y seleccione **Procesar modelo**.  
  
 Para obtener más información, vea [consultas de obtención de detalles &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para ver los datos de obtención de detalles de un modelo de minería de datos  
  
1.  En el Diseñador de minería de datos, haga clic en la pestaña **Visor de modelo de minería de datos** .  
  
2.  Seleccione el modelo **TM_Decision_Tree** en la lista **Modelo de minería de datos** .  
  
3.  Cambie el **Background** valor de fondo `1`a. De esta forma, se muestra solo la parte del modelo que está relacionada con los clientes que compraron bicicletas.  
  
4.  En la lista **Visor** , seleccione Visor de árboles de Microsoft. De esta manera, se forzará la actualización del visor con las condiciones de filtro. A continuación, busque el nodo **Age >= 34 y <41** y haga clic con el botón secundario en el nodo.  
  
5.  Seleccione **Obtener detalles**y después **Columnas de modelo y estructura** para abrir la ventana **Obtener detalles** .  
  
6.  Desplácese a la columna **Structure.Date First Purchase** para ver la fecha de compra de las bicicletas anteriores.  
  
7.  Para copiar los datos en el Portapapeles, haga clic con el botón derecho en cualquier fila de la tabla y seleccione **Copiar todo**.  
  
 Felicidades, ha completado el Tutorial básico de minería de datos. Ahora que conoce más las herramientas de minería de datos, recomendamos que también complete el Tutorial intermedio de minería de datos, que demuestra cómo crear modelos de pronóstico, análisis de la cesta de la compra y agrupación en clústeres de secuencia.  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Crear predicciones &#40;Tutorial básico de minería de datos&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  

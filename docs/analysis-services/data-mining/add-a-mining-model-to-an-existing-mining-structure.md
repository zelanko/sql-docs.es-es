---
title: Agregar un modelo de minería de datos a una estructura de minería de datos existente | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8b995a5b3fb89956e690598c786dc0a09474021
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>Agregar un modelo de minería de datos a una estructura de minería de datos existente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una vez agregado el modelo de minería de datos inicial, podrá agregar más modelos a una estructura de minería de datos. Los modelos deben incluir columnas que estén presentes en la estructura, pero se puede definir el uso de las columnas de un modo distinto para cada modelo de minería de datos. Para obtener más información sobre la forma de definir columnas del modelo de minería de datos, vea [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>Para agregar un modelo de minería de datos a la estructura  
  
1.  En el elemento de menú **Modelo de minería de datos** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione **Nuevo modelo de minería de datos**.  
  
     Se abrirá el cuadro de diálogo **Nuevo modelo de minería de datos** .  
  
2.  En **Nombre del modelo**, escriba un nombre para el nuevo modelo de minería de datos.  
  
3.  En **Nombre del algoritmo**, seleccione el algoritmo a partir del cual se va a generar el modelo de minería de datos.  
  
4.  Haga clic en **Aceptar**.  
  
 Aparece un modelo de minería de datos nuevo en la pestaña **Modelos de minería de datos** . El modelo utiliza las columnas predeterminadas que están presentes en la estructura. Para obtener información sobre cómo modificar las columnas, vea [Cambiar las propiedades de un modelo de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md).  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  

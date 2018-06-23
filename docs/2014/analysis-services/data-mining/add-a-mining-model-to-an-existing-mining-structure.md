---
title: Agregar un modelo de minería de datos a una estructura de minería de datos existente | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], adding
- mining structures [Analysis Services], mining models
- adding mining models
ms.assetid: fcf72300-0674-4e73-a826-9b8eeffefbb5
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 708d03cac04dc8c3574c40398c005fd17faf4bb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105285"
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>Agregar un modelo de minería de datos a una estructura de minería de datos existente
  Una vez agregado el modelo de minería de datos inicial, podrá agregar más modelos a una estructura de minería de datos. Los modelos deben incluir columnas que estén presentes en la estructura, pero se puede definir el uso de las columnas de un modo distinto para cada modelo de minería de datos. Para obtener más información sobre la forma de definir columnas del modelo de minería de datos, vea [Columnas del modelo de minería de datos](mining-model-columns.md).  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>Para agregar un modelo de minería de datos a la estructura  
  
1.  En el elemento de menú **Modelo de minería de datos** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione **Nuevo modelo de minería de datos**.  
  
     Se abrirá el cuadro de diálogo **Nuevo modelo de minería de datos** .  
  
2.  En **Nombre del modelo**, escriba un nombre para el nuevo modelo de minería de datos.  
  
3.  En **Nombre del algoritmo**, seleccione el algoritmo a partir del cual se va a generar el modelo de minería de datos.  
  
4.  Haga clic en **Aceptar**.  
  
 Aparece un modelo de minería de datos nuevo en la pestaña **Modelos de minería de datos** . El modelo utiliza las columnas predeterminadas que están presentes en la estructura. Para obtener información sobre cómo modificar las columnas, vea [Cambiar las propiedades de un modelo de minería de datos](change-the-properties-of-a-mining-model.md).  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  
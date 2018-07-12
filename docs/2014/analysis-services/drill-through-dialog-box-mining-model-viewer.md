---
title: Obtención de detalles (Visor de modelos de minería de datos) del cuadro de diálogo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 331ab6da3e2e244f3a0413d80006ceeb907704f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151476"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>Cuadro de diálogo Obtener detalles (Visor de modelos de minería de datos)
  Cuando vea un modelo de minería de datos utilizando la pestaña **Visor de modelos de minería de datos** del Diseñador de minería de datos, podrá obtener detalles sobre los datos de los casos, siempre que el modelo tenga habilitada la obtención de detalles. Además, si la estructura de minería de datos subyacente tiene habilitada la obtención de detalles, también podrá ver las columnas de la estructura de minería de datos, incluso si dichas columnas no se incluyeron en el modelo de minería de datos. En la lista de columnas, las columnas de estructura tienen como prefijo la etiqueta "Structure." .  
  
> [!NOTE]  
>  No puede habilitar la obtención de detalles en una estructura de minería existente. En su lugar, debe volver a crear la estructura de minería de datos y habilitar la obtención de detalles durante el proceso de creación.  
  
 Para obtener información sobre cómo tener acceso a los datos de los casos desde cada visor de modelos de minería de datos que admitan la obtención de detalles, **vea** [Obtener detalles de datos de caso a partir de un modelo de minería de datos](data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
## <a name="options"></a>Opciones  
 **Casos clasificados en**  
 Muestra la definición de la regla, el conjunto de elementos y el clúster contenidos en el nodo seleccionado.  
  
 **Lista de columnas**  
 Muestra las columnas del modelo, seguidas por las columnas de estructura.  
  
 **Nota** : las columnas de estructura solamente se muestran si la obtención de detalles está habilitada en la estructura de minería de datos y si se ha seleccionado la opción, **Columnas de modelo y estructura**. Además, debe tener permisos de obtención de detalles en el modelo de minería de datos y en la estructura de minería de datos para ver las columnas.  
  
 Las columnas de estructura que no están incluidas en el modelo aparecen como **estructura.\< nombre de columna >**.  
  
> [!NOTE]  
>  Puede hacer clic con el botón derecho en cualquier lugar de la cuadrícula de columnas y seleccionar **Copiar todo** para copiar en el Portapapeles los datos de la obtención de detalles, en formato delimitado por tabuladores. Los datos copiados incluyen solo los datos de los casos, no la definición del nodo.  
  
 **Reproducir**  
 Haga clic en el botón de flecha verde para actualizar los datos.  
  
## <a name="see-also"></a>Vea también  
 [Las consultas de obtención de detalles &#40;minería de datos&#41;](data-mining/drillthrough-queries-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  

---
title: Crear un Alias para una columna de modelo | Documentos de Microsoft
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
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cf049cdd7fabbc50fdacf5ab72ca3ce1845482f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112130"
---
# <a name="create-an-alias-for-a-model-column"></a>Crear un alias para una columna de modelo
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede crear un alias para una columna de modelo. Esto puede resultar útil cuando el nombre de la estructura de minería de datos es demasiado largo para trabajar con él fácilmente, o si desea cambiar el nombre de la columna para que describa mejor su contenido o su uso en el modelo. Por ejemplo, si realiza una copia de una columna de estructura y, a continuación, discretiza la columna de manera diferente para un modelo determinado, puede cambiar el nombre de la columna para reflejar con más precisión el contenido.  
  
 Para crear un alias para una columna de modelo, utilice el panel **Propiedades** y establezca la propiedad [Name](../scripting/properties/name-element-assl.md) de la columna.  
  
 En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, el alias parece entre paréntesis al lado de la etiqueta de uso de columna.  
  
 Para más información sobre cómo establecer las propiedades de un modelo de minería de datos, vea [Columnas del modelo de minería de datos](mining-model-columns.md).  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>Para agregar un alias a una columna de modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en la celda del modelo de minería perteneciente a la columna que quiere cambiar y, luego, seleccione **Propiedades**.  
  
2.  En la ventana **Propiedades** situada a la derecha de la pantalla, haga clic en la celda existente junto a la propiedad Name y elimine el valor actual. Escriba un nuevo nombre para la columna.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](mining-model-tasks-and-how-tos.md)   
 [Propiedades del modelo de minería de datos](mining-model-properties.md)  
  
  
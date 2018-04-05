---
title: Crear una dimensión de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], dimensions
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 786ef852e8bb6e820c4f52df87767478b68e74f2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-data-mining-dimension"></a>Crear una dimensión de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Si la estructura de minería de datos se basa en un cubo OLAP, puede crear una dimensión que contiene el contenido del modelo de minería de datos. A continuación, puede volver a incorporar la dimensión en el cubo de origen.  
  
 También puede examinar la dimensión, utilizarla para explorar los resultados del modelo o consultar la dimensión mediante MDX.  
  
### <a name="to-create-a-data-mining-dimension"></a>Para crear una dimensión de minería de datos  
  
1.  En el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], seleccione la pestaña **Estructura de minería de datos** o la pestaña **Modelos de minería de datos** .  
  
2.  En el menú **Modelo de minería de datos** , seleccione **Crear una dimensión de minería de datos**.  
  
     Aparece el cuadro de diálogo **Crear una dimensión de minería de datos** .  
  
3.  En la lista **Nombre del modelo** del cuadro de diálogo **Crear una dimensión de minería de datos** , seleccione el modelo de minería de datos OLAP.  
  
4.  En el cuadro **Nombre de dimensión** , escriba el nombre de la nueva dimensión de minería de datos.  
  
5.  Si desea crear un cubo que incluya la nueva dimensión de minería de datos, seleccione **Crear cubo**. Después de seleccionar **Crear cubo**, puede escribir un nuevo nombre para el cubo.  
  
6.  Haga clic en **Aceptar**.  
  
     La dimensión de minería de datos se crea y se agrega a la carpeta **Dimensiones** del Explorador de dimensiones. Si ha seleccionado **Crear cubo**, también se crea un cubo nuevo que se agrega a la carpeta **Cubos** .  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

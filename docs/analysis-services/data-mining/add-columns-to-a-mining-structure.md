---
title: Agregar columnas a una estructura de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c5d68b5442320bbd48123a3f8335154b7153b260
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="add-columns-to-a-mining-structure"></a>Agregar columnas a una estructura de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Utilice el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para agregar columnas a una estructura de minería de datos después de definirla en el Asistente para minería de datos. Puede agregar cualquier columna existente en la vista de origen que se haya utilizado para definir la estructura de minería de datos.  
  
> [!NOTE]  
>  Puede agregar varias copias de una columna a una estructura de minería de datos; sin embargo, no debería utilizar más de una copia de la columna dentro del mismo modelo para evitar las correlaciones falsas entre la columna de origen y la derivada.  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>Para agregar una columna a una estructura de minería de datos  
  
1.  Seleccione la pestaña **Estructura de minería de datos** en el Diseñador de minería de datos.  
  
2.  Haga clic con el botón derecho en la estructura de minería de datos y seleccione **Agregar una columna**.  
  
     Se abrirá el cuadro de diálogo **Seleccionar una columna** .  
  
3.  En **Tabla de origen**, seleccione la tabla de la vista del origen de datos en la que reside la columna.  
  
4.  En **Columna de origen**, seleccione la columna que desee agregar a la estructura de minería de datos.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Si agrega una columna que ya existe, se incluirá una copia en la estructura con el número "1" adjuntado al nombre. Para cambiar el nombre de la columna copiada a algo más descriptivo, escriba un nuevo nombre en la propiedad **Name** de la columna de la estructura de minería de datos.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de estructura de minería de datos y procedimientos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

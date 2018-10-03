---
title: Agregar columnas a una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 954159ba298b47c1a10a5e7baef1cff523dcc4b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171255"
---
# <a name="add-columns-to-a-mining-structure"></a>Agregar columnas a una estructura de minería de datos
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
 [Tareas y procedimientos de las estructuras de minería de datos](mining-structure-tasks-and-how-tos.md)  
  
  

---
title: Alinear los datos en un gráfico en una tabla o una matriz (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 939aee299710da15e3b7714b40175e0edba4fb54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249575"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>Alinear los datos en un gráfico en una tabla o una matriz (Generador de informes y SSRS)
  Los minigráficos y barras de datos son gráficos pequeños y sencillos que comunican mucha información con pocos detalles. Al activar esta opción, los valores de los minigráficos y las barras de datos se alinearán en todas las celdas distintas de la tabla o matriz, aun cuando falten valores en los datos en que se basan.  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 En esta imagen, el gráfico de columnas muestra las ventas cotidianas para cada empleado. Tenga en cuenta que durante los días que un empleado no tiene ninguna venta, el gráfico deja un espacio en blanco y alinea los días subsiguientes horizontalmente. También alinea verticalmente los gráficos, para lo que hace que los tamaños de los distintos gráficos estén en relación unos con otros. Para obtener más información, vea [Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="align-the-data-in-a-sparkline-or-data-bar"></a>Alinear los datos en un minigráfico o una barra de datos  
  
1.  Haga clic en el minigráfico o la barra de datos y, a continuación, haga clic en **Propiedades del Eje horizontal** o **Propiedades del Eje vertical**.  
  
2.  En la pestaña **Opciones del eje** , active el cuadro **Alinear los ejes en** y, a continuación en la lista desplegable, seleccione el grupo en el que alinear el eje.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Agregar minigráficos y barras de datos &#40;generador de informes y SSRS&#41;](add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  

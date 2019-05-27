---
title: Agregar minigráficos y barras de datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1dbb3fd9ec10c5e1ca11a7e150f0d8a4c0fec883
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106519"
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>Agregar minigráficos y barras de datos (Generador de informes y SSRS)
  Los minigráficos y barras de datos son gráficos pequeños y accesorios que comunican mucha información con pocos detalles. Para más información, vea [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
 Los minigráficos y las barras de datos se suelen colocar en celdas en una tabla o matriz. Normalmente, los minigráficos solo muestran una serie cada uno. Las barras de datos puede contener uno o varios puntos de datos. El efecto de los minigráficos y las barras de datos deriva de la repetición de la información de la serie para cada fila de la tabla o matriz.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>Para agregar un minigráfico o una barra de datos a una tabla o matriz  
  
1.  Si aún no lo ha hecho, cree una tabla o matriz con los datos que desee mostrar. Para obtener más información, vea [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md) y [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Inserte una columna en la tabla o matriz. Para más información, vea [Insertar o eliminar una columna &#40;Generador de informes y SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  En la pestaña **Insertar** , haga clic en **Minigráfico** o en **Barra de datos**y, a continuación, haga clic en una celda de la nueva columna.  
  
    > [!NOTE]  
    >  No se pueden colocar minigráficos en un grupo de detalles de una tabla. Deben estar en una celda asociada a un grupo.  
  
4.  En el cuadro de diálogo **Cambiar tipo de minigráfico o barra de datos** , haga clic en el tipo de minigráfico o barra de datos que prefiera y, después, haga clic en **Aceptar**.  
  
5.  Haga clic en el minigráfico o barra de datos.  
  
     El panel **Datos del gráfico** se abre.  
  
6.  En el área **Valores** , haga clic en el signo más ( **) de** Agregar campos **+** y, después, haga clic en el campo cuyos valores quiera incluir en el gráfico.  
  
7.  En el área **Grupos de categorías** , haga clic en el signo más ( **) de** Agregar campos **+** y, después, haga clic en el campo por cuyos valores quiera agrupar.  
  
     Normalmente, para los minigráficos y barras de datos, no se agregará un campo al área **Grupo de series** porque solo se desea una serie para cada fila.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Alinear los datos en un gráfico en una tabla o una matriz &#40;Generador de informes y SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  

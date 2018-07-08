---
title: Establecer y configurar unidades de medida (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 9105abf7bc25b4327d1c3d75a214cb667850a7eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179232"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>Establecer y configurar unidades de medida (Generador de informes y SSRS)
  Los indicadores proporcionan dos unidades de medida: porcentaje y numérico. De forma predeterminada, los indicadores se configuran para usar porcentajes como unidad de medida. Esto significa que un intervalo de porcentajes determina los valores de indicador asignados a cada icono del indicador. Los intervalos de porcentajes están divididos uniformemente entre los iconos del conjunto de indicadores. Cada icono representa un estado del indicador. Puede cambiar los porcentajes para cada icono en el conjunto de indicadores especificando porcentajes inicial y final diferentes. Los indicadores también detectan automáticamente los valores máximo y mínimo de los datos.  
  
 Puede cambiar la unidad de medida para que sea un valor numérico. En este caso, no especifica para los datos el valor mínimo sino el máximo; en su lugar, solo proporciona los valores inicial y final para cada icono que usa el indicador.  
  
 Opciones como las unidades de medida se pueden establecer mediante expresiones. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-use-the-numeric-state-measurement-unit"></a>Utilizar la unidad de medida de estado numérica  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  En la lista **Unidad de medida de estados** , haga clic en **Numérico**.  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece los valores de la opción.  
  
4.  Para cada icono en el indicador establecido, actualice los valores de los cuadros de texto **Inicial** y **Final** .  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece los valores de las opciones **Inicial** y **Final** .  
  
    > [!NOTE]  
    >  Los valores de los cuadros de texto **Inicial** y **Final** deben ser numéricos.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-percentage-measurement-unit"></a>Para utilizar la unidad de medida en porcentaje  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  En la lista **Unidad de medida de estados** , haga clic en **Porcentaje**.  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece los valores de la opción.  
  
4.  Opcionalmente, cambie las opciones **Mínimo** y **Máximo** para usar valores concretos en lugar de detectar automáticamente los valores máximo y mínimo de los datos usados en el indicador. El valor de **Mínimo** debe ser menor que el valor de **Máximo**.  
  
    > [!NOTE]  
    >  Si establece los valores mínimo y máximo explícitamente, el indicador utiliza ese intervalo de valores sin tener en cuenta los valores máximo y mínimo reales de los datos. Esto significa que los valores menores que el mínimo y mayores que el máximo se excluye de la evaluación que determina qué icono de indicador se va a mostrar en el informe.  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece los valores de la opción.  
  
5.  Para cada icono en el indicador establecido, actualice los valores de los cuadros de texto **Inicial** y **Final** .  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece los valores de las opciones **Inicial** y **Final** .  
  
    > [!NOTE]  
    >  Los valores de los cuadros de texto **Inicial** y **Final** deben ser numéricos.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  

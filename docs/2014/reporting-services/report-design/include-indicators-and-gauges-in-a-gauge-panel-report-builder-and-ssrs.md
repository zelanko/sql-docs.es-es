---
title: Incluir indicadores y medidores en un panel de medidores (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 848eb1bc39b45d76e1e1ffd97fbd05d557a740a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225004"
---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>Incluir indicadores y medidores en un panel de medidores (Generador de informes y SSRS)
  El panel de medidores es el contenedor de nivel superior que contiene uno o más medidores e indicadores. Los indicadores se pueden incrustar en los medidores o colocar a su lado en el panel de medidores.  
  
 Si el indicador y el medidor son adyacentes en el panel de medidores y muestran datos de campos distintos, podría desear agregar etiquetas para dejar claro qué datos comunican el medidor y el indicador.  
  
 Las opciones del medidor y el indicador se pueden establecer mediante expresiones. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>Para incrustar un indicador en un medidor  
  
1.  Abra un informe existente o cree un informe que contenga una tabla y matriz con los datos que desea mostrar. Para obtener más información, vea [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md) y [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Inserte una columna en la tabla o matriz. Para más información, vea [Insertar o eliminar una columna &#40;Generador de informes y SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  En la pestaña **Insertar** , en el grupo **Regiones de datos** , haga clic en **Medidor**y, a continuación, en una de las celdas de la nueva columna. Aparece el cuadro de diálogo **Seleccionar tipo de medidor** .  
  
4.  Haga clic en **Radial**. Se selecciona el primer medidor radial.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Haga clic en el medidor. El panel **Medidor de datos** se abre.  
  
7.  En el área **Valores** , en el cuadro de lista **(Sin especificar)** , haga clic en el campo cuyos valores quiere que se muestren en el medidor. Si lo prefiere, puede arrastrar el campo que desea utilizar desde el conjunto de datos de informe.  
  
8.  Haga clic con el botón derecho en el medidor, haga clic en **Agregar indicador**y, después, haga clic en **Secundario**. Se abre el cuadro de diálogo **Seleccionar estilo de indicador** .  
  
9. En el cuadro de diálogo **Seleccionar estilo de indicador** , en el panel izquierdo, haga clic en el tipo de indicador que desea y, a continuación, haga clic en el indicador establecido.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
11. Haga clic en el indicador. El panel **Medidor de datos** se abre.  
  
12. En el área **Valores** , en el cuadro de lista **(Sin especificar)** , haga clic en el campo cuyos valores quiera mostrar como un indicador. Si lo prefiere, puede arrastrar el campo que desea utilizar desde el conjunto de datos de informe.  
  
     El campo puede ser el mismo que el utilizado en el medidor, u otro distinto.  
  
13. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>Para mostrar un indicador y medidor en paralelo  
  
1.  Abra un informe existente o cree un informe que contenga una tabla y matriz con los datos que desea mostrar. Para obtener más información, vea [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md) y [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Inserte una columna en la tabla o matriz. Para más información, vea [Insertar o eliminar una columna &#40;Generador de informes y SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  En la pestaña **Insertar** , en el grupo **Regiones de datos** , haga clic en **Medidor**y, a continuación, en una de las celdas de la columna que ha insertado. Aparecerá el cuadro de diálogo **Seleccionar tipo de medidor** .  
  
4.  Haga clic en **Radial**. Se selecciona el primer medidor radial.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Haga clic en el medidor. El panel **Medidor de datos** se abre.  
  
7.  En el área **Valores** , en el cuadro de lista **(Sin especificar)** , haga clic en el campo cuyos valores quiere que se muestren en el medidor. Si lo prefiere, puede arrastrar el campo que desea utilizar desde el conjunto de datos de informe.  
  
8.  Haga clic con el botón derecho en el medidor, haga clic en **Agregar indicador**y, después, haga clic en **Adyacente**. Se abre el cuadro de diálogo **Seleccionar estilo de indicador** .  
  
9. En el cuadro de diálogo **Seleccionar estilo de indicador** , en el panel izquierdo, haga clic en el tipo de indicador que desea y, a continuación, haga clic en el indicador establecido.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
11. Haga clic en el indicador. El panel **Medidor de datos** se abre.  
  
12. En el área **Valores** , en el cuadro de lista **(Sin especificar)** , haga clic en el campo cuyos valores quiera mostrar como un indicador. Si lo prefiere, puede arrastrar el campo que desea utilizar desde el conjunto de datos de informe.  
  
     El campo puede ser el mismo que el utilizado en el medidor, u otro distinto.  
  
13. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
14. Haga clic con el botón derecho en el panel de medidores y, después, haga clic en **Agregar etiqueta**. Se agregará una etiqueta al panel de medidores. Realice los mismos pasos una vez más.  
  
     En el panel de medidores habrá dos etiquetas.  
  
15. Arrastre cada etiqueta hasta un lugar próximo al medidor o indicador.  
  
16. Haga clic con el botón derecho en la etiqueta próxima al medidor, haga clic en **Propiedades de etiqueta**y escriba el texto que quiera en el cuadro **Texto** .  
  
17. Haga clic con el botón derecho en la etiqueta próxima al indicador, haga clic en **Propiedades de etiqueta**y escriba el texto que quiera en el cuadro **Texto** .  
  
18. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  

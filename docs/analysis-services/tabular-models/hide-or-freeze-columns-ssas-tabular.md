---
title: Ocultar o Inmovilizar columnas | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e588e16549a609fe15f0f7d7eaf89a010a5bde2c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042479"
---
# <a name="hide-or-freeze-columns"></a>Ocultar o Inmovilizar columnas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Si en el diseñador de modelos hay columnas que no desea mostrar en una tabla, puede ocultarlas temporalmente. Si oculta una columna, dispone de más espacio en la pantalla para agregar columnas nuevas o para trabajar solo con las columnas de datos pertinentes. Puede ocultar y mostrar columnas desde el menú **Columna** del diseñador de modelos y desde el menú contextual disponible en cada encabezado de columna. Para mantener visible un área de un modelo mientras se desplaza a otra área del modelo, puede inmovilizar columnas específicas para bloquearlas.  
  
> [!IMPORTANT]  
>  La capacidad de ocultar columnas no tiene como finalidad la seguridad de los datos; solo pretende simplificar y acortar la lista de columnas visibles en el diseñador de modelos o en los informes. Para proteger los datos, puede definir roles de seguridad. Los roles solo pueden restringir los metadatos y los datos visibles a los objetos definidos en el rol. Para obtener más información, consulte [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 A la hora de ocultar una columna, tiene la opción de ocultarla mientras trabaja en el diseñador de modelos o en los informes. Si oculta todas las columnas, la tabla aparece vacía en su totalidad en el Diseñador de modelos.  
  
> [!NOTE]  
>  Si necesita ocultar muchas columnas, puede crear una perspectiva en lugar de ocultarlas y mostrarlas. Una perspectiva es una vista personalizada de los datos que facilita el trabajo con subconjuntos de datos relacionados. Para obtener más información, vea [crear y administrar perspectivas](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)  
  
### <a name="to-hide-an-individual-column"></a>Para ocultar una sola columna  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga la columna que desee ocultar.  
  
2.  Haga clic con el botón derecho en la columna, haga clic en **Ocultar columnas**y, después, haga clic en **Desde el Diseñador e Informes**, **Desde informes**o **Desde diseñador**.  
  
### <a name="to-hide-multiple-columns"></a>Para ocultar varias columnas  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga las columnas que desee ocultar.  
  
2.  Haga clic en el menú **Columnas** y, a continuación, en **Ocultar y mostrar**.  
  
3.  En el cuadro de diálogo **Ocultar y mostrar columnas** , busque cada columna que desee ocultar y, a continuación, anule la selección de una de las opciones **En diseñador** y **En informes**, o ambas.  
  
4.  Haga clic en **Aceptar**.  
  
### <a name="to-freeze-columns"></a>Para inmovilizar columnas  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga las columnas que desee inmovilizar.  
  
2.  Seleccione las columnas que desee inmovilizar.  
  
3.  Haga clic en el menú **Columnas** y, a continuación, en **Inmovilizar**.  
  
    > [!NOTE]  
    >  Cuando se inmovilizan columnas, estas se mueven a la izquierda (o delante) de la tabla en el diseñador. Cuando se libera una columna, esta no recupera su ubicación original.  
  
## <a name="see-also"></a>Vea también  
 [Tablas y columnas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  

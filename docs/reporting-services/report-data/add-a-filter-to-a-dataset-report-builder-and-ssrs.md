---
title: Agregar un filtro a un conjunto de datos (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68838748a77567747cd7f44f7924738d87b68450
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>Agregar un filtro a un conjunto de datos (Generador de informes y SSRS)
  Agregue un filtro a un conjunto de datos para limitar los datos en un informe una vez recuperados de un origen de datos externo. Al agregar un filtro a un conjunto de datos, todos los elementos de informe o regiones de datos usan solo los datos que cumplen las condiciones del filtro.  
  
 En el caso de un conjunto de datos compartido, un filtro que se aplica a todos los elementos dependientes debe formar parte de la definición del conjunto de datos compartida en el servidor de informes. Un informe o elemento de informe que contenga una instancia de un conjunto de datos compartido puede crear un filtro adicional que se aplique solo a esa instancia.  
  
 Para agregar un filtro, debe especificar una o varias condiciones que son las ecuaciones del filtro. Una ecuación de filtro se compone de una expresión que identifica los datos que se van a filtrar, un operador y el valor con el que se va a llevar a cabo la comparación. Los tipos de datos de los datos filtrados y el valor deben coincidir. No está permitido el filtrado por valores agregados para un conjunto de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>Para agregar un filtro a un conjunto de datos compartido  
  
1.  Abra un conjunto de datos compartido en modo de conjunto de datos compartido.  
  
2.  En la pestaña **Inicio** , en el grupo **Conjuntos de datos compartidos** , haga clic en Conjuntos de datos. Se abre el cuadro de diálogo **Propiedades del conjunto de datos** .  
  
3.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
4.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
5.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
6.  En el cuadro de lista, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
7.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
8.  En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>Para agregar un filtro a un conjunto de datos incrustado o una instancia de conjunto de datos compartido  
  
1.  Abra un informe en el modo de diseño de informes.  
  
2.  En el panel **Datos de informe** , haga clic con el botón derecho en un conjunto de datos y, después, haga clic en **Propiedades del conjunto de datos**. Se abre el cuadro de diálogo **Propiedades del conjunto de datos** .  
  
3.  Haga clic en **Filtros**. Aparece la lista actual de ecuaciones de filtro. La lista aparece vacía de forma predeterminada.  
  
4.  Haga clic en **Agregar**. Aparece una nueva ecuación de filtro en blanco.  
  
5.  En **Expresión**, escriba o seleccione la expresión para el campo que va a filtrar. Para editar la expresión, haga clic en el botón de expresión (*fx*).  
  
6.  En la lista desplegable, seleccione el tipo de datos que coincide con el tipo de datos de la expresión que ha creado en el paso anterior.  
  
7.  En el cuadro **Operador** , seleccione el operador que deberá usar el filtro para comparar los valores de los cuadros **Expresión** y **Valor** . El operador que elija determinará el número de valores que se usarán en el paso siguiente.  
  
8.  En el cuadro **Valor** , escriba la expresión o el valor que deberá usar el filtro para evaluar el valor de **Expresión**.  
  
     Para obtener ejemplos de ecuaciones de filtro, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Ejemplos de expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Agregar un filtro &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  


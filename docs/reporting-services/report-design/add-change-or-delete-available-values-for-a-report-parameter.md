---
title: Agregar, cambiar o eliminar los valores disponibles para un parámetro de informe | Microsoft Docs
description: Personalice la lista de opciones que un usuario tiene para un parámetro en el Generador de informes mediante la especificación de una lista de valores disponibles que se mostrarán al usuario.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b9d826682f2bcb742ab4ba7ae9e2b6fba33600c0
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681334"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter"></a>Agregar, cambiar o eliminar los valores disponibles para un parámetro de informe
  Después de crear un parámetro de informe, puede especificar la lista de valores disponibles que verá el usuario. La existencia de una lista de valores disponibles limita las opciones del usuario a únicamente los valores válidos para el parámetro.  
  
 Los valores disponibles aparecen en una lista desplegable junto al parámetro de informe en la barra de herramientas cuando se ejecuta el informe. Los parámetros de informe pueden representar uno o varios valores. Cuando hay varios valores, en la parte superior de la lista aparece la característica **Seleccionar todo** , que permite al usuario seleccionar o desactivar todos los valores con un solo clic.  
  
 Puede proporcionar una lista estática de valores o una lista procedente de un conjunto de datos de informe. Opcionalmente, puede proporcionar un nombre descriptivo para los valores; para hacerlo, solo tiene que especificar un campo de etiqueta. Por ejemplo, para un parámetro basado en un campo `ProductID` , puede mostrar el campo `ProductName` en la etiqueta de parámetro. Cuando se ejecute el informe, el usuario podrá elegir entre los nombres de producto, pero el valor elegido realmente será el `ProductID`correspondiente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Después de publicar un informe, puede invalidar los valores disponibles que define en el informe en la herramienta de creación de informes; para ello, establezca los valores de propiedad de parámetro en el servidor de informes. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>Para agregar o cambiar los valores disponibles para un parámetro de informe  
  
1.  En el panel Datos de informe, expanda el nodo Parámetros. Haga clic con el botón derecho en el parámetro y, después, haga clic en **Propiedades del parámetro**. Se abrirá el cuadro de diálogo **Propiedades de parámetro de informe** .  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no es visible, haga clic en **Ver** y, después, haga clic en **Datos de informe**.  
  
2.  Haga clic en **Valores disponibles**. Seleccione una opción de valores disponibles:  
  
    -   Haga clic en **Especificar valores** para especificar manualmente una lista de valores y, de manera opcional, nombres descriptivos (las etiquetas) para dichos valores.  
  
         Haga clic en **Agregar** ; a continuación, especifique el valor en el cuadro de texto **Valor** y, opcionalmente, especifique la etiqueta en el cuadro de texto **Etiqueta** . Si no proporciona ninguna etiqueta, se usará el valor. Puede escribir una expresión como valor. El tipo de datos debe coincidir con el tipo de datos del parámetro. No se pueden usar nombres de campo en una expresión para un parámetro. Para obtener ejemplos, vea [Filtros de uso frecuente &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md).  
  
         Repita este paso tantas veces como valores desee proporcionar. El orden de los elementos en esta lista determina el orden en que los verá el usuario en la lista desplegable. Para cambiar el orden de un elemento en la lista, haga clic en un cuadro de texto **Valor** o **Etiqueta** para seleccionar el elemento y, a continuación, use los botones de flecha arriba y flecha abajo para mover el elemento hacia arriba o hacia abajo en la lista.  
  
    -   Haga clic en **Obtener valores a partir de una consulta** para proporcionar el nombre de un conjunto de datos existente que recupere los valores, y opcionalmente, los nombres descriptivos para este parámetro.  
  
        > [!IMPORTANT]  
        >  Si el mismo conjunto de datos contiene el correspondiente parámetro de consulta para el parámetro de informe, el informe mostrará un mensaje de error cuando intente ejecutarlo. Este error se resuelve usando un conjunto de datos distinto para recuperar los valores.  
  
         En **Conjunto de datos**, elija el nombre del conjunto de datos.  
  
         En **Campo de valor**, elija el nombre del campo que proporciona los valores de parámetro.  
  
         En **Campo de etiqueta**, elija el nombre del campo que proporciona los nombres descriptivos para el parámetro. Si no hay ningún campo independiente para los nombres descriptivos, elija el mismo campo que eligió para el campo **Valor** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Cuando muestre una vista previa del informe, verá una lista desplegable de valores disponibles para el parámetro.  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>Para quitar los valores disponibles para un parámetro de informe  
  
1.  En el panel Datos de informe, expanda el nodo Parámetros. Haga clic con el botón derecho en el parámetro y, después, haga clic en **Propiedades del parámetro**. Se abrirá el cuadro de diálogo **Parámetros del informe** .  
  
2.  Haga clic en **Valores disponibles**.  
  
3.  En **Seleccione una de las opciones siguientes**, haga clic en **Ninguno**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Cuando muestre una vista previa del informe, no verá la lista desplegable de valores disponibles para el parámetro.  
  
## <a name="see-also"></a>Consulte también  
 [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Usar referencias a la colección de parámetros &#40;generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

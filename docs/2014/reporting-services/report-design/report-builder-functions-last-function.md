---
title: Función Last (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 123b78a0-d6c9-4f78-b0e7-73b21854a250
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c9dc383d9a895218cf644bafc53be3b43cdc698a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197322"
---
# <a name="last-function-report-builder-and-ssrs"></a>Función Last (Generador de informes y SSRS)
  Devuelve el último valor de la expresión especificada en el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Last(expression, scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *expression*  
 (`Variant` o `Binary`) expresión en la que se lleva a cabo la agregación, por ejemplo, `=Fields!Fieldname.Value`.  
  
 *ámbito*  
 (`String`) (opcional). Nombre de un conjunto de datos, una región de datos o un grupo que contiene los elementos de informe a los que se va a aplicar la función de agregado. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo devuelto  
 Varía según el tipo de expresión.  
  
## <a name="remarks"></a>Notas  
 La función `Last` devuelve el último valor de un conjunto de datos después de aplicar todos los filtros y la configuración de ordenación al ámbito especificado.  
  
 El `Last` función no se puede usar en expresiones de filtro de grupo con nada excepto el actual ámbito (valor predeterminado).  
  
 También puede usar `Last` en un encabezado de página para devolver el último valor de la `ReportItems` colección de una página con el fin de generar los encabezados de estilo diccionario que muestren la primera y última entrada en una página.  
  
 El valor de *scope* tiene que ser una constante de cadena y no puede ser una expresión. Para los agregados exteriores o los que no especifican a otros agregados, *scope* debe hacer referencia al ámbito actual o a un ámbito de contenido. Para los agregados de agregados, los agregados anidados pueden especificar un ámbito secundario.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   *Scope* , para los agregados anidados, debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   *Scope* , para los agregados anidados, no puede ser el nombre de un conjunto de datos.  
  
-   *Expresión* no debe contener `First`, `Last`, `Previous`, o `RunningValue` funciones.  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código devuelve el último número de producto del grupo `Category` de una región de datos.  
  
```  
=Last(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
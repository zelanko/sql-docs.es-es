---
title: Función RunningValue (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5176ddc4f06531dcbfea383362bdd195a215fe84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63216177"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>Función RunningValue (Generador de informes y SSRS)
  Devuelve un agregado actualizado de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *expression*  
 Expresión en la que se lleva a cabo la agregación; por ejemplo, `[Quantity]`.  
  
 *function*  
 (`Enum`). Nombre de la función de agregado que se aplica a la expresión; por ejemplo, `Sum`. Esta función no puede ser `RunningValue`, `RowNumber` ni `Aggregate`.  
  
 *ámbito*  
 (`String`) Constante de cadena que es el nombre de un conjunto de datos, grupo, región de datos o NULL (`Nothing` en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica el contexto en el que evaluar la agregación. `Nothing` especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="return-type"></a>Tipo devuelto  
 Viene determinado por la función de agregado especificada en el parámetro *function* .  
  
## <a name="remarks"></a>Comentarios  
 El valor para `RunningValue` se restablece en 0 para cada nueva instancia del ámbito. Si se especifica un grupo, el valor actual se restablece cuando cambia la expresión de grupo. Si se especifica una región de datos, el valor actual se restablece en cada instancia nueva de la región de datos. Si se especifica un conjunto de datos, el valor actual no se restablece en todo el conjunto de datos.  
  
 `RunningValue` no se puede utilizar en un filtro o expresión de ordenación.  
  
 El conjunto de datos para los que se calcula el valor en ejecución debe tener el mismo tipo de datos. Si desea convertir datos de varios tipos de datos numéricos al mismo tipo de datos, use funciones de conversión como `CInt`, `CDbl` o `CDec`. Para obtener más información, vea [Funciones de conversión de tipos](https://go.microsoft.com/fwlink/?LinkId=96142).  
  
 *Scope* no puede ser una expresión.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   El ámbito para los agregados anidados debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   El ámbito para los agregados anidados no puede ser el nombre de un conjunto de datos.  
  
-   *Expresión* no puede contener `First`, `Last`, `Previous`, o `RunningValue` funciones.  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para calcular el valor actual del número de filas, use `RowNumber`. Para más información, vea [Función RowNumber &#40;Generador de informes y SSRS&#41;](report-builder-functions-rownumber-function.md).  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo de código siguiente proporciona la suma actual del campo denominado `Cost` en el ámbito más externo, que es el conjunto de datos.  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 El ejemplo de código siguiente proporciona la suma actual del campo denominado `Score` en el conjunto de datos denominado `DataSet1`.  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 El ejemplo de código siguiente proporciona la suma actual del campo denominado `Traffic Charges` en el ámbito más externo.  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

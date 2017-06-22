---
title: "Función RunningValue (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f6a4dbc99e73afca24ede68d160c2c48a7422ef1
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="report-builder-functions---runningvalue-function"></a>Notificar a las funciones del generador - función RunningValue
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
 (**Enum**) Nombre de la función de agregado que se aplica a la expresión; por ejemplo, **Sum**. Esta función no puede ser **RunningValue**, **RowNumber**ni **Aggregate**.  
  
 *ámbito*  
 (**String**) Constante de cadena que es el nombre de un conjunto de datos, grupo, región de datos o NULL (**Nothing** en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica el contexto en el que evaluar la agregación. **Nothing** especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="return-type"></a>Tipo devuelto  
 Viene determinado por la función de agregado especificada en el parámetro *function* .  
  
## <a name="remarks"></a>Comentarios  
 El valor para **RunningValue** se restablece en 0 para cada nueva instancia del ámbito. Si se especifica un grupo, el valor actual se restablece cuando cambia la expresión de grupo. Si se especifica una región de datos, el valor actual se restablece en cada instancia nueva de la región de datos. Si se especifica un conjunto de datos, el valor actual no se restablece en todo el conjunto de datos.  
  
 **RunningValue** no se puede utilizar en un filtro o expresión de ordenación.  
  
 El conjunto de datos para los que se calcula el valor en ejecución debe tener el mismo tipo de datos. Si desea convertir datos de varios tipos de datos numéricos al mismo tipo de datos, use funciones de conversión como **CInt**, **CDbl** o **CDec**. Para obtener más información, vea [Funciones de conversión de tipos](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 *Scope* no puede ser una expresión.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   El ámbito para los agregados anidados debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   El ámbito para los agregados anidados no puede ser el nombre de un conjunto de datos.  
  
-   *Expression* no debe contener las funciones **First**, **Last**, **Previous**o **RunningValue** .  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para calcular el valor actual del número de filas, use **RowNumber**. Para obtener más información, vea [Función RowNumber &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-rownumber-function.md).  
  
 Para obtener más información, consulte [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obtener más información sobre los agregados recursivos, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
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
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

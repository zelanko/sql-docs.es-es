---
title: Función Aggregate (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2adafc32be75ff6386d3a892b6a8d253274820d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109755"
---
# <a name="aggregate-function-report-builder-and-ssrs"></a>Función de agregado (Generador de informes y SSRS)
  Devuelve un agregado personalizado de la expresión especificada, según esté definido en el proveedor de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *expression*  
 Expresión en la que se lleva a cabo la agregación. La expresión debe ser una referencia de campo sencilla.  
  
 *ámbito*  
 (`String`) Nombre de un conjunto de datos, grupo o región de datos que contiene el informe de elementos que se va a aplicar la función de agregado. *Scope* tiene que ser una constante de cadena y no puede ser una expresión. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo devuelto  
 El tipo de valor devuelto viene determinado por el proveedor de datos. Devuelve `Nothing` si el proveedor de datos no admite esta función o datos no están disponibles.  
  
## <a name="remarks"></a>Comentarios  
 La función `Aggregate` proporciona una manera de utilizar los agregados que se calculan en el origen de datos externo. La extensión de datos determina la compatibilidad con esta característica. Por ejemplo, la extensión de procesamiento de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recupera los conjuntos de filas planas de una consulta MDX. Algunas filas del conjunto de resultados pueden contener valores agregados calculados en el servidor del origen de datos. Estos se conocen como *agregados de servidor*. Para ver los agregados de servidor en el diseñador gráfico de consultas para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede usar el botón **Mostrar agregaciones** de la barra de herramientas. Para más información, vea [Interfaz de usuario del Diseñador de consultas MDX de Analysis Services &#40;Generador de informes&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md).  
  
 Cuando se muestra la combinación de valores agregados y valores de conjunto de datos de detalle en las filas de detalles de una región de datos Tablix, normalmente no se incluyen los agregados de servidor porque no son datos de detalle. Sin embargo, es probable que desee mostrar todos los valores recuperados para el conjunto de datos y personalizar la forma en que se calculan y se muestran los datos agregados.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta el uso de la `Aggregate` función en las expresiones del informe con el fin de determinar si se mostrarán los agregados de servidor en las filas de detalles. Si incluye `Aggregate` en una expresión en una región de datos, los agregados de servidor solo pueden aparecer en el grupo total o grand total de filas, no en las filas de detalle. Si desea mostrar los agregados de servidor en las filas de detalles, no use la función `Aggregate`.  
  
 Para cambiar este comportamiento predeterminado, cambie el valor de la opción **Interpretar los subtotales como filas de detalles** en el cuadro de diálogo **Propiedades del conjunto de datos** . Si esta opción se establece en `True`, todos los datos, incluidos los agregados de servidor, aparecen como datos de detalle. Si se establece en `False`, los agregados de servidor aparecen como totales. El valor de esta propiedad afecta a todas las regiones de datos que están vinculadas a este conjunto de datos.  
  
> [!NOTE]  
>  Todos los grupos contenedores del elemento de informe que hacen referencia a  `Aggregate` deben incluir referencias de campo sencillas en sus expresiones de grupo; por ejemplo, `[FieldName]`. No puede usar `Aggregate` en una región de datos que usa expresiones de grupo complejas. Para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extensión de procesamiento de datos, la consulta debe incluir campos MDX del tipo `LevelProperty` (no `MemberProperty`) para admitir la agregación con el `Aggregate`función.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   *Scope* , para los agregados anidados, debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   *Scope* , para los agregados anidados, no puede ser el nombre de un conjunto de datos.  
  
-   *Expresión* no puede contener `First`, `Last`, `Previous`, o `RunningValue` funciones.  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Diferencias entre las funciones Aggregate y Sum  
 El `Aggregate` función difiere de las funciones agregadas numéricas como `Sum` en que el `Aggregate` función devuelve un valor que se calcula mediante la extensión de procesamiento de datos o proveedor de datos. Las funciones agregadas numéricas como `Sum` devuelven un valor calculado por el procesador de informes en un conjunto de datos del conjunto de datos que viene determinada por la *ámbito* parámetro. Para más información, vea la lista de funciones de agregado en [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente muestra una expresión que recupera un agregado de servidor para el campo `LineTotal`. La expresión se agrega a una celda de una fila que pertenece al grupo `GroupbyOrder`.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

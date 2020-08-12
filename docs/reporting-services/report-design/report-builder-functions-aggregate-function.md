---
title: Función Aggregate (Generador de informes) | Microsoft Docs
description: La función Aggregate devuelve un agregado personalizado de la expresión especificada, según la defina el proveedor de datos.
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: aef4411334ee9ca345a5b2f2c8b325c6fd2dae70
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462419"
---
# <a name="report-builder-functions---aggregate-function"></a>Funciones del Generador de informes: función Aggregate
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
  
 *scope*  
 (**String**) Nombre de un conjunto de datos, grupo o región de datos que contiene los elementos de informe donde se aplicará la función de agregado. *Scope* tiene que ser una constante de cadena y no puede ser una expresión. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 El tipo de valor devuelto viene determinado por el proveedor de datos. Devuelve el valor **Nothing** si el proveedor de datos no admite esta función o no hay datos disponibles.  
  
## <a name="remarks"></a>Observaciones  
 La función **Aggregate** proporciona una manera de utilizar los agregados que se calculan en el origen de datos externo. La extensión de datos determina la compatibilidad con esta característica. Por ejemplo, la extensión de procesamiento de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recupera los conjuntos de filas planas de una consulta MDX. Algunas filas del conjunto de resultados pueden contener valores agregados calculados en el servidor del origen de datos. Estos se conocen como *agregados de servidor*. Para ver los agregados de servidor en el diseñador gráfico de consultas para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede usar el botón **Mostrar agregaciones** de la barra de herramientas. Para más información, vea [Interfaz de usuario del Diseñador de consultas MDX de Analysis Services &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26).  
  
 Cuando se muestra la combinación de valores agregados y valores de conjunto de datos de detalle en las filas de detalles de una región de datos Tablix, normalmente no se incluyen los agregados de servidor porque no son datos de detalle. Sin embargo, es probable que desee mostrar todos los valores recuperados para el conjunto de datos y personalizar la forma en que se calculan y se muestran los datos agregados.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta el uso de la función **Aggregate** en las expresiones del informe y para determinar si se mostrarán los agregados de servidor en las filas de detalles. Si incluye **Aggregate** en una expresión en una región de datos, los agregados de servidor solo podrán aparecer en las filas de total de grupo o en las filas de total general, no en las filas de detalles. Si desea mostrar los agregados de servidor en las filas de detalles, no use la función **Aggregate** .  
  
 Para cambiar este comportamiento predeterminado, cambie el valor de la opción **Interpretar los subtotales como filas de detalles** en el cuadro de diálogo **Propiedades del conjunto de datos** . Si esta opción se establece en **True**, todos los datos, incluidos los agregados de servidor, aparecen como datos de detalle. Si se establece en **False**, los agregados de servidor aparecen como totales. El valor de esta propiedad afecta a todas las regiones de datos que están vinculadas a este conjunto de datos.  
  
> [!NOTE]
>  Todos los grupos contenedores del elemento de informe que hacen referencia a **Aggregate** necesitan tener referencias de campo sencillas en sus expresiones de grupo (por ejemplo, `[FieldName]`). No puede usar **Aggregate** en una región de datos que usa expresiones de grupo complejas. Para la extensión de procesamiento de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , es necesario incluir en la consulta los campos MDX del tipo **LevelProperty** (no de **MemberProperty**) para admitir la agregación con la función **Aggregate**.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   *Scope* , para los agregados anidados, debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   *Scope* , para los agregados anidados, no puede ser el nombre de un conjunto de datos.  
  
-   *Expression* no debe contener las funciones **First**, **Last**, **Previous**o **RunningValue** .  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Diferencias entre las funciones Aggregate y Sum  
 La función **Aggregate** difiere de las funciones de agregado numéricas como **Sum** en que **Aggregate** devuelve un valor calculado por el proveedor de datos o por la extensión de procesamiento de datos. Las funciones de agregado numéricas como **Sum** devuelven un valor calculado por el procesador de informes en un conjunto de datos perteneciente al conjunto de datos determinado por el parámetro *scope* . Para más información, vea la lista de funciones de agregado en [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente muestra una expresión que recupera un agregado de servidor para el campo `LineTotal`. La expresión se agrega a una celda de una fila que pertenece al grupo `GroupbyOrder`.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

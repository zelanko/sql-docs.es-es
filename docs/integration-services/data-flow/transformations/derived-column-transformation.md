---
title: "Transformación Columna derivada | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66e45a47fd340aa62b852193ec75aac7c1cde8ed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="derived-column-transformation"></a>Transformación Columna derivada
  La transformación Columna derivada crea nuevos valores de columna aplicando expresiones a las columnas de entrada de la transformación. Una expresión puede contener cualquier combinación variables, funciones, operadores y columnas de la entrada de transformación. El resultado puede agregarse como una nueva columna o insertarse en una columna existente como un valor de reemplazo. La transformación Columna derivada puede definir varias columnas derivadas, y cualquier variable o columna de entrada puede aparecer en varias expresiones.  
  
 Puede utilizar esta transformación para realizar las siguientes tareas:  
  
-   Concatenar datos de distintas columnas en una columna derivada. Por ejemplo, puede combinar valores de las columnas **FirstName** y **LastName** en una sola columna derivada, denominada **FullName**, mediante la expresión `FirstName + " " + LastName`.  
  
-   Extraer caracteres de datos de cadena mediante funciones como SUBSTRING y después almacenar el resultado en una columna derivada. Por ejemplo, puede extraer de la columna **FirstName** la inicial del nombre de una persona mediante la expresión `SUBSTRING(FirstName,1,1)`.  
  
-   Aplicar funciones matemáticas a datos numéricos y almacenar el resultado en una columna derivada. Por ejemplo, puede cambiar la longitud y la precisión de una columna numérica, **SalesTax**, a un número con dos cifras decimales mediante la expresión `ROUND(SalesTax, 2)`.  
  
-   Crear expresiones que comparen columnas de entrada y variables. Por ejemplo, puede comparar la variable **Version** con los datos de la columna **ProductVersion**y, en función del resultado de la comparación, usar el valor de **Version** o **ProductVersion**mediante la expresión `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Extraer partes de un valor datetime. Por ejemplo, puede utilizar las funciones GETDATE y DATEPART para extraer el año actual mediante la expresión `DATEPART("year",GETDATE())`.  
  
-   Convierta las cadenas de fecha a un formato específico mediante una expresión.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Configuración de la transformación Columna derivada  
 Puede configurar la transformación Columna derivada de las maneras siguientes:  
  
-   Proporcionar una expresión para cada columna de entrada o nueva columna que se vaya a modificar. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Si una expresión hace referencia a una columna de entrada sobrescrita por la transformación Columna derivada, la expresión utiliza el valor original de la columna, no el valor derivado.  
  
-   Si agrega resultados a columnas nuevas y el tipo de datos es **string**, especifique una página de códigos. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 La transformación Columna derivada incluye la propiedad personalizada FriendlyExpression. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para obtener más información, vea [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md)y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una salida normal y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Derivar valores de columna mediante la transformación Columna derivada](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>Columna derivada, editor de transformación
  Utilice el cuadro de diálogo **Editor de transformación Columna derivada** para crear expresiones que rellenan columnas nuevas o de reemplazo.  
  
### <a name="options"></a>.  
 **Variables y columnas**  
 Genere una expresión que utiliza una variable o una columna de entrada arrastrándolas de la lista de variables y columnas disponibles a una fila de tabla existente en el siguiente panel, o bien a una nueva fila al final de la lista.  
  
 **Funciones y operadores**  
 Genere una expresión que utiliza una función o un operador para evaluar los datos de entrada y los datos de salida directa arrastrando las funciones y operadores de la lista al siguiente panel.  
  
 **Nombre de columna derivada**  
 Especifique un nombre de columna derivada. De forma predeterminada, se muestra una lista numerada de columnas derivadas; no obstante, puede elegir un nombre único descriptivo.  
  
 **Columna derivada**  
 Seleccione una columna derivada de la lista. Elija si desea agregar la columna derivada como columna de salida nueva o reemplazar los datos de una columna existente.  
  
 **Expresión**  
 Escriba una expresión o genere una arrastrando elementos de la lista anterior de columnas, variables, funciones y operadores disponibles.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Temas relacionados**: [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operadores &#40;expresión de SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41](../../../integration-services/expressions/functions-ssis-expression.md).  
  
 **Tipo de datos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece el tipo de datos según corresponda. El valor de esta columna es de solo lectura. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Longitud**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece la longitud de columna para los datos de cadena. El valor de esta columna es de solo lectura.  
  
 **Precisión**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la precisión de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Escala**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la escala de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Página de códigos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la página de códigos para el tipo de datos DT_STR. Puede actualizar la **Página de códigos**.  
  
 **Configurar la salida de errores**  
 Especifique cómo quiere controlar los errores mediante el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  

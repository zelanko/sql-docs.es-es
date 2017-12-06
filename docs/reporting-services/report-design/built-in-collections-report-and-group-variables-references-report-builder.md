---
title: Referencias a las colecciones de variables de informe y de grupo (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 423768a2a0381377a3d780e632399a41ecf11e5a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>Colecciones integradas: referencias a variables de grupo e informe (Generador de informes)
  Si existe un cálculo complejo que se usa más de una vez en las expresiones de un informe, es probable que le interese crear una variable. Puede crear una variable de informe o una variable de grupo. Los nombres de variable deben ser únicos en un informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>Variables de informe  
 Use una variable de informe para hospedar un valor para cálculos dependientes del tiempo, como los tipos de cambio de divisas o las marcas de tiempo, o para los cálculos complejos a los que se hace referencia varias veces. De forma predeterminada, una variable de informe se calcula una sola vez y se puede usar en expresiones en cualquier parte del informe. Las variables de informe son de solo lectura de forma predeterminada. Puede cambiar el valor predeterminado para habilitar una variable de informe como de lectura y escritura. El valor de una variable de informe se conserva en toda una sesión, hasta que se vuelve a procesar el informe.  
  
 Para agregar una variable de informe, abra el cuadro de diálogo **Propiedades del informe** , haga clic en **Variables**y especifique un nombre y un valor. Los nombres son cadenas con distinción de mayúsculas y minúsculas que empiezan por una letra y no tienen espacios. Un nombre puede incluir letras, números o caracteres de subrayado (_).  
  
 Para hacer referencia a la variable en una expresión, use la sintaxis de colección global, por ejemplo, `=Variables!CustomTimeStamp.Value`. En la superficie de diseño, el valor aparece en un cuadro de texto como `<<Expr>>`.  
  
 Puede utilizar las variables de informe de varias maneras:  
  
-   **Uso de solo lectura** Configure un valor una vez para crear una constante para la sesión del informe, por ejemplo, para crear una marca de tiempo.  
  
     Dado que las expresiones de los cuadros de texto se evalúan a petición mientras el usuario pasa por las páginas de un informe, los valores dinámicos (por ejemplo, una expresión que incluya la función `Now()` , que devuelve la hora) pueden devolver valores diferentes si se avanza y retrocede de página en página con el botón **Atrás** . Al establecer el valor de una variable de informe en la expresión `=Now()`y, a continuación, agregar la variable a una expresión, se asegurará de que se usa el mismo valor durante todo el procesamiento del informe.  
  
-   **Uso de lectura y escritura** Configure un valor una vez y serialícelo dentro de una sesión del informe. La opción de lectura y escritura para las variables es más aconsejable que el uso de una variable estática en el bloque de código de la definición de informe.  
  
     Si elimina la opción **Solo lectura** de una variable, la propiedad Writable de la variable se establece en **true**. Para actualizar el valor desde una expresión, use el método SetValue, por ejemplo, `=Variables!MyVariable.SetValue("123")`.  
  
    > [!NOTE]  
    >  El momento en que el procesador de informes inicializa una variable o evalúa una expresión que actualiza una variable no se puede controlar. El orden de ejecución para la inicialización de variables no está definido.  
  
 Para obtener más información acerca de las sesiones, vea [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="group-variables"></a>Variables de grupo  
 Use una variable de grupo para calcular una expresión compleja una vez en el ámbito de un grupo. Una variable de grupo solo es válida en el ámbito del grupo y de sus grupos secundarios.  
  
 Por ejemplo, imagine que una región de datos muestra datos de inventario para elementos que pertenecen a categorías de impuestos diferentes y que desea aplicar tipos impositivos diferentes a cada categoría. Agrupará los datos por categoría y definirá una variable *Tax* en el grupo primario. Después, definirá una variable de grupo para *ItemTax* para cada categoría de impuesto y asignará cada uno de los subgrupos de categoría a la variable de grupo adecuada. Por ejemplo:  
  
-   Para el grupo primario basado en `[Category]`, defina la variable *Tax* con un valor `[Tax]`. Imagine que los valores de categoría son Alimentos y Ropa.  
  
-   Para el grupo secundario basado en `[Subcategory]`, defina la variable *ItemsTax* como `=Variables!Tax.Value * Sum(Fields!Price.Value)`. Imagine que los valores de subcategoría para la categoría Alimentos son Bebidas y Pan. Imagine que los valores de subcategoría para Ropa son Camisas y Sombreros.  
  
-   Agregue la expresión `=Variables!ItemsTax.Value`para un cuadro de texto de una fila del grupo secundario.  
  
     En el cuadro de texto se muestra el impuesto total para Bebidas y Pan tras aplicar el impuesto para Alimentos, y el impuesto total para Camisas y Sombreros tras aplicar el impuesto para Ropa.  
  
 Para agregar una variable de grupo, abra el cuadro de diálogo **Propiedades de grupo de Tablix** , haga clic en **Variables**y proporcione un nombre y un valor. La variable de grupo se calcula una vez para cada valor de grupo único.  
  
 Para hacer referencia a la variable en una expresión, use la sintaxis de colección global, por ejemplo, `=Variables!GroupDescription.Value`. En la superficie de diseño, el valor aparece en un cuadro de texto como `<<Expr>>`.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  

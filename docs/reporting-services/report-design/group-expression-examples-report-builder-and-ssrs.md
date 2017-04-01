---
title: "Ejemplos de expresi&#243;n de grupo (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "datos [Reporting Services], agrupación"
  - "agrupar datos"
  - "expresiones [Reporting Services], agregar"
  - "grupos [Reporting Services], expresiones"
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: 24
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 24
---
# Ejemplos de expresi&#243;n de grupo (Generador de informes y SSRS)
  En una región de datos, puede agrupar los datos por un solo campo o crear expresiones más complejas que identifiquen los datos por los que se debe realizar la agrupación. Las expresiones complejas incluyen referencias a varios campos o parámetros, instrucciones condicionales o código personalizado. Al definir un grupo para una región de datos, debe agregar estas expresiones a las propiedades del **Grupo** . Para obtener más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Para combinar dos o más grupos basados en expresiones de campo simples, agregue cada campo a la lista de expresiones de grupo en la definición de grupo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Ejemplos de expresiones de grupo  
 En la siguiente tabla, se incluyen ejemplos de expresiones de grupo que se pueden usar para definir un grupo.  
  
|Description|Expresión|  
|-----------------|----------------|  
|Agrupar por el campo `Region` .|`=Fields!Region.Value`|  
|Agrupar por apellidos y nombre.|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|Agrupar por la primera letra del apellido.|`=Fields!LastName.Value.Substring(0,1)`|  
|Agrupar por parámetro, en función de la selección del usuario.<br /><br /> En este ejemplo, el parámetro `GroupBy` debe estar basado en una lista de valores disponibles que proporcione una opción válida por la que agrupar.|`=Fields(Parameters!GroupBy.Value).Value`|  
|Agrupar por tres intervalos de edad independientes:<br /><br /> "Under 21", "Between 21 and 50" y "Over 50".|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|Agrupar por varios intervalos de edad. En este ejemplo se muestra código personalizado, escrito en .NET [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , que devuelve una cadena para los intervalos siguientes:<br /><br /> 25 or Under<br /><br /> 26 to 50<br /><br /> 51 to 75<br /><br /> Over 75|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> Código personalizado:<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## Vea también  
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  
---
title: PropertyRef, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: 4
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1b4d64cc0e0e59029361412bc96bd98559be51b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198062"
---
# <a name="propertyref-element-csdlbi"></a>PropertyRef, elemento (CSDLBI)
  El elemento PropertyRef es un tipo simple que proporciona una referencia a una columna que incluye un valor requerido por otra propiedad.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento PropertyRef.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Nombre|Sí|Cadena que contiene el nombre de la propiedad que es el destino de la referencia.|  
  
## <a name="propertyrefs-element"></a>Elemento PropertyRefs  
 PropertyRefs es un tipo complejo que define una colección de propiedades cada una de las cuales está incluida en un elemento PropertyRef.  
  
 En la tabla siguiente se enumeran los elementos y atributos del tipo PropertyRefs.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|PropertyRef|Sí|Cadena que contiene la referencia de propiedad.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un elemento PropertyRef que especifica el origen de una fórmula utilizada en una medida, en el ejemplo de modelo tabular AdventureWorks.  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un KPI del cubo de operaciones de Contoso. Los elementos PropertyRef apuntan a las columnas que contienen la fórmula o los valores utilizados para definir el objetivo y el estado del KPI en relación con ese objetivo.  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
   <Documentation>  
     <Summary>KPI Description</Summary>  
   </Documentation>  
     <bi:Measure   
         Caption="Sum of SalesAmount"   
         ReferenceName="Sum of SalesAmount"   
         FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
     <bi:Kpi   
           StatusGraphic="Three Circles Colored">  
         <bi:KpiGoal>  
            <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
          </bi:KpiGoal>  
          <bi:KpiStatus>  
              <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
          </bi:KpiStatus>  
     </bi:Kpi>  
     </bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
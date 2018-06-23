---
title: Medir el elemento (CSDLBI) | Documentos de Microsoft
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
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 36dda5645c53a88fa497682e6946331c85ca67db
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105226"
---
# <a name="measure-element-csdlbi"></a>Measure, elemento (CSDLBI)
  El elemento Measure es un tipo complejo basado en el elemento Property de CSDL. Las anotaciones CSDLBI agregan atributos que admiten la definición de fórmulas complejas para su uso en modelos de datos de Business Intelligence.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Measure, así como todos los atributos aplicables al elemento Property.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Kpi|no|Elemento necesario solo para las medidas que se utilizan como KPI. No todas las medidas son KPI, pero todos los KPI deben basarse en la definición de una medida.<br /><br /> [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)|  
|IsSimpleMeasure|no|Valor true/false que indica si la fórmula utilizada en la medida es una de las agregaciones simples (SUM, COUNT, MIN, MAX, AVG, DistinctCount).<br /><br /> El valor predeterminado es true.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestran dos medidas del ejemplo de modelo tabular AdventureWorks. La segunda medida se ha convertido en un KPI agregando elementos KPI.  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensiona;**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra una medida del cubo de operaciones de Contoso que se utiliza como un KPI.  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
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
  
  
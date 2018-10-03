---
title: Medir el elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de02e5c0233fb5cb1699f038b87871c8757f0256
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068405"
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
  
  

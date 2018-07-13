---
title: Kpigoal, elemento (CSDLBI) | Microsoft Docs
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
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b64e3124ba7a848921e1b0844b20d03e9aa82af4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165246"
---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal, elemento (CSDLBI)
  El elemento KpiGoal proporciona una referencia a la columna que se utiliza para definir el objetivo de un indicador clave de rendimiento ((KPI).  
  
 En CSDLBI, los KPI están basados en medidas, y el elemento Measure contiene la fórmula (si existe), mientras que otros metadatos asociados con el KPI se definen como parte del [KPI, elemento &#40;CSDLBI&#41;](kpi-element-csdlbi.md).  El elemento Kpigoal es un subtipo del elemento Kpi.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los atributos que definen el elemento KpiGoal.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|PropertyRef|Sí|Referencia a la columna que contiene el valor objetivo del KPI.<br /><br /> El elemento Kpigoal debe contener exactamente un elemento PropertyRef.<br /><br /> Vea [PropertyRef, elemento &#40;CSDLBI&#41;](propertyref-element-csdlbi.md).|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un KPI del modelo de ejemplo AdventureWorks.  
  
```  
  
<Property Name="InternetCurrentSalesPerformance" Type="Double">  
  <bi:Measure>  
    <bi:Kpi StatusGraphic="Three Stars Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Goal" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Status" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un KPI del cubo de operaciones de Contoso.  
  
```  
<bi:Measure   
       Caption="Sum of SalesAmount"   
       ReferenceName="Sum of SalesAmount"   
       FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
    <bi:Kpi   
       StatusGraphic="Three Circles Colored">  
      <bi:KpiGoal>  
         <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Goal" />  
       </bi:KpiGoal>  
       <bi:KpiStatus>  
          <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Status" />  
        </bi:KpiStatus>  
       </bi:Kpi>  
</bi:Measure>  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
  

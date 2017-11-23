---
title: KPI, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 203ee6e8-eef2-4476-b09f-bd95e492ddaa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8941555a0768f80a30947c043aea639469ec8df3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="kpi-element-csdlbi"></a>KPI, elemento (CSDLBI)
  El elemento Kpi define un cálculo que se puede utilizar como un indicador clave de rendimiento (KPI). En un modelo de datos de Business Intelligence, los KPI están basados en medidas y, como tales, la definición del KPI contiene todos los metadatos asociados con dichas medidas, así como la información necesaria para la presentación de los valores del KPI, incluyendo un gráfico predeterminado.  
  
 El elemento Kpi no especifica la fórmula, que está incluida en la definición de la medida, sino los metadatos adicionales asociados con medidas que se utilizan como KPI. Una vez que haya designado una medida como KPI, no podrá utilizarla como medida en otros contextos.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Kpi.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Documentación|No|Descripción del KPI.|  
|KpiGoal|Sí|Referencia a una columna que contiene valores que se pueden utilizar como objetivo.<br /><br /> Vea [PropertyRef, elemento &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md).|  
|KpiStatus|Sí|Referencia a una columna que contiene valores que representan el estado actual del KPI.|  
|StatusGraphic|Sí|Referencia a una imagen que indica un progreso negativo, neutro o positivo con relación a los objetivos definidos en el KPI.|  
  
## <a name="remarks"></a>Comentarios  
 Para crear un KPI al diseñar un modelo, cree una medida y defina su uso como KPI. A continuación, agregue la información específica de los KPI, como el gráfico que se va a utilizar para mostrar las tendencias.  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.0 de CSDLBI, se muestra un KPI que mide las ventas en el ejemplo de modelo tabular AdventureWorks.  
  
```  
  
<Property Name="InternetCurrSalesPerf" Type="Double">  
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
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

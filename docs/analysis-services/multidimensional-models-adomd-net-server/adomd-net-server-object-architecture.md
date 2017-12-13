---
title: Arquitectura de objetos de servidor ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0a08f60225aeed3c7b4266caf5596b6e639a88f5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="adomdnet-server-object-architecture"></a>Arquitectura de objetos de servidor ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Los objetos de servidor ADOMD.NET son objetos auxiliares que pueden usarse para crear funciones definidas por el usuario (UDF) o procedimientos almacenados en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Para usar el **Microsoft.AnalysisServices.AdomdServer** espacio de nombres (y estos objetos), debe agregarse una referencia a msmgdsrv.dll en el proyecto UDF o procedimiento almacenado.  
  
 ![Muestra las relaciones de objetos de servidor ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-server/media/adomdnetserverobjectmodel.gif "muestra las relaciones de objetos de servidor ADOMD.NET")  
Modelo de objetos ADOMD.NET  
  
 La interacción con la jerarquía de objetos ADOMD.NET suele comenzar con uno o más de los objetos del nivel superior, como se describe en la tabla siguiente.  
  
|Para|Utilice este objeto|  
|--------|---------------------|  
|Evaluar expresiones MDX (Expresiones multidimensionales)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression> proporciona una forma de ejecutar una expresión MDX y evaluar dicha expresión bajo una tupla especificada.|  
|Proporcionar compatibilidad para la ejecución de funciones MDX sin construir la instrucción MDX completa|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> resulta adecuado para llamar a las funciones MDX predefinidas sin utilizar el objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression>. En versiones futuras habrá disponibles funciones adicionales para el objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX>.|  
|Representar el contexto de ejecución actual de la UDF|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> expone información como el modelo de minería de datos o el cubo actual y varias recopilaciones de metadatos. Un uso clave del objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> es la propiedad <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy>. Este uso clave permite que el autor de la UDF o el procedimiento almacenado tome decisiones en función del miembro de cierta dimensión sobre el que se realiza la consulta.|  
|Crear conjuntos y tuplas|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> proporciona una forma de crear conjuntos inmutables, mientras que <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> proporciona una forma de crear tuplas inmutables.|  
|Admitir la conversión implícita entre los seis tipos básicos del lenguaje MDX|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> proporciona conversión implícita entre los tipos siguientes:<br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Level><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Member><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Set><br /><br /> Escalar o tipos de valor|  
  
## <a name="see-also"></a>Vea también  
 [Programación del servidor ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  

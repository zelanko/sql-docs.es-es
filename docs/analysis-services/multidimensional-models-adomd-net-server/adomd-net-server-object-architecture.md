---
title: Arquitectura de objetos de servidor ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f5ad515251a783705e3f8e04c73674a8e978348
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889988"
---
# <a name="adomdnet-server-object-architecture"></a>Arquitectura de objetos de servidor ADOMD.NET
  Los objetos de servidor ADOMD.NET son objetos auxiliares que se pueden usar para crear funciones definidas por el usuario (UDF) o procedimientos [!INCLUDE[msCoName](../../includes/msconame-md.md)] almacenados en. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
> [!NOTE]  
>  Para usar el espacio de nombres **Microsoft. AnalysisServices. AdomdServer** (y estos objetos), se debe agregar una referencia a msmgdsrv. dll al proyecto o procedimiento almacenado de UDF.  
  
 ![Muestra las relaciones de objeto en el servidor de ADOMD.net](https://docs.microsoft.com/analysis-services/analysis-services/multidimensional-models-adomd-net-server/media/adomdnetserverobjectmodel.gif "Muestra las relaciones de objeto en el servidor de ADOMD.net")  
Modelo de objetos ADOMD.NET  
  
 La interacción con la jerarquía de objetos ADOMD.NET suele comenzar con uno o más de los objetos del nivel superior, como se describe en la tabla siguiente.  
  
|En|Utilice este objeto|  
|--------|---------------------|  
|Evaluar expresiones MDX (Expresiones multidimensionales)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression> proporciona una forma de ejecutar una expresión MDX y evaluar dicha expresión bajo una tupla especificada.|  
|Proporcionar compatibilidad para la ejecución de funciones MDX sin construir la instrucción MDX completa|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> resulta adecuado para llamar a las funciones MDX predefinidas sin utilizar el objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression>. En versiones futuras habrá disponibles funciones adicionales para el objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX>.|  
|Representar el contexto de ejecución actual de la UDF|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> expone información como el modelo de minería de datos o el cubo actual y varias recopilaciones de metadatos. Un uso clave del objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> es la propiedad <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy>. Este uso clave permite que el autor de la UDF o el procedimiento almacenado tome decisiones en función del miembro de cierta dimensión sobre el que se realiza la consulta.|  
|Crear conjuntos y tuplas|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> proporciona una forma de crear conjuntos inmutables, mientras que <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> proporciona una forma de crear tuplas inmutables.|  
|Admitir la conversión implícita entre los seis tipos básicos del lenguaje MDX|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> proporciona conversión implícita entre los tipos siguientes:<br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Level><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Member><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Set><br /><br /> Escalar o tipos de valor|  
  
## <a name="see-also"></a>Vea también  
 [Programación del servidor ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  

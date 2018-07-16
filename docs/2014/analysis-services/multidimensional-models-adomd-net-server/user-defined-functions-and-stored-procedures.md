---
title: Funciones definidas por el usuario y procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ADOMD.NET]
- ADOMD.NET, user defined functions
- user defined functions [ADOMD.NET]
- ADOMD.NET, UDFs
- ADOMD.NET, stored procedures
ms.assetid: 07e8aa47-37d4-4bbc-8bff-49e422d12897
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 719929ec255f29da6477788d4feff1162609f993
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253027"
---
# <a name="user-defined-functions-and-stored-procedures"></a>Funciones definidas por el usuario y procedimientos almacenados
  Con objetos de servidor ADOMD.NET, puede crear funciones definidas por el usuario (UDF) o procedimientos almacenados para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que interactúan con los metadatos y datos del servidor. Se llama a estos métodos incrustados a través de instrucciones de expresiones multidimensionales (MDX) o extensiones de minería de datos (DMX) para proporcionar una funcionalidad adicional sin las latencias asoció a las comunicaciones de red.  
  
## <a name="udf-examples"></a>Ejemplos de UDF  
 UDF es un método al que se puede llamar en el contexto de una instrucción MDX o DMX, admite cualquier número de parámetros y devuelve cualquier tipo de datos.  
  
 Un UDF que se crea mediante MDX es similar al que se crea para DMX. La diferencia principal reside en que ciertas propiedades del objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context>, como las propiedades <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentCube%2A> y <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentMiningModel%2A>, únicamente están disponibles para un lenguaje de scripting o para el otro.  
  
 En los ejemplos siguientes se muestra cómo usar un método UDF para devolver una descripción del nodo, filtrar tuplas y aplican un filtro a una tupla.  
  
### <a name="returning-a-node-description"></a>Devolver una descripción del nodo.  
 En el ejemplo siguiente se crea un UDF que devuelve la descripción del nodo para un nodo especificado. UDF usa el contexto actual en el que se ejecuta y utiliza una cláusula DMX FROM para recuperar el nodo del modelo de minería actual.  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 Una vez implementado, la expresión DMX siguiente puede llamar al ejemplo UDF anterior, que recupera el nodo de predicción más probable. La descripción contiene información que describe las condiciones que constituyen el nodo de predicción.  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>Devolver tuplas  
 En el ejemplo siguiente se establece un conjunto y un recuento del retorno, y se recuperan de forma aleatoria las tuplas del conjunto, devolviendo un subconjunto final:  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 Se llama al ejemplo anterior en el ejemplo MDX siguiente. En este ejemplo MDX, se recuperan cinco estados o provincias aleatorios de la **Adventure Works** base de datos.  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>Aplicar un filtro a una tupla  
 En el ejemplo siguiente, se define un UDF para que establezca un conjunto y aplique un filtro a cada tupla en el conjunto mediante el objeto Expression. Cualquier tupla que cumpla el filtro se agregará a un conjunto que se devuelve.  
  
 [!code-csharp[Adomd.NetServer#FilterSet](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#filterset)]  
  
 En el siguiente ejemplo MDX se llama al ejemplo anterior, que filtra el conjunto por ciudades con nombres que empiezan por 'A.'  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>Ejemplo de procedimiento almacenado  
 En el ejemplo siguiente, un procedimiento almacenado basado en MDX utiliza AMO para crear particiones para Internet Sales si es necesario.  
  
 [!code-csharp[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#createinternetsalesmeasuregrouppartitions)]  
  
  

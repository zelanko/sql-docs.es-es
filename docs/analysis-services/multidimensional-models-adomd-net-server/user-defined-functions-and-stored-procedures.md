---
title: Funciones definidas por el usuario y procedimientos almacenados | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f6bd4d0c6f768205f4b9d59e30cee15c173c345
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="user-defined-functions-and-stored-procedures"></a>Funciones definidas por el usuario y procedimientos almacenados
  Con objetos de servidor ADOMD.NET, puede crear una función definida por el usuario (UDF) o procedimientos almacenados para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que interactúa con metadatos y datos del servidor. Se llama a estos métodos incrustados a través de instrucciones de expresiones multidimensionales (MDX) o extensiones de minería de datos (DMX) para proporcionar una funcionalidad adicional sin las latencias asoció a las comunicaciones de red.  
  
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
  
 [!code-cs[Adomd.NetServer#FilterSet](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_1.cs)]  
  
 En el siguiente ejemplo MDX se llama al ejemplo anterior, que filtra el conjunto por ciudades con nombres que empiezan por 'A.'  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>Ejemplo de procedimiento almacenado  
 En el ejemplo siguiente, un procedimiento almacenado basado en MDX utiliza AMO para crear particiones para Internet Sales si es necesario.  
  
 [!code-cs[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_2.cs)]  
  
  

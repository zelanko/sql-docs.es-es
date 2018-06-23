---
title: Recuperar datos mediante el objeto CellSet | Documentos de Microsoft
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
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cda35dc6151d17e1dad2d341337d67ef39d9f839
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111674"
---
# <a name="retrieving-data-using-the-cellset"></a>Recuperar datos mediante el objeto CellSet
  Al recuperar datos analíticos, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> proporciona la máxima interactividad y flexibilidad. El objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> es una caché de datos y metadatos jerárquicos en memoria que conserva las dimensiones originales de los datos. El objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> también se puede recorrer en estado conectado o desconectado. Debido a la posibilidad de utilizarlo sin conexión, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> se puede usar para ver datos y metadatos en un orden cualquiera y proporciona el modelo de objetos más completo para la recuperación de datos. Dicha capacidad de uso sin conexión también hace que el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> tenga la máxima sobrecarga y sea el modelo de objetos de recuperación de datos de ADOMD.NET más lento de rellenar.  
  
## <a name="retrieving-data-in-a-connected-state"></a>Recuperar datos en estado conectado  
 Si desea utilizar el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> para recuperar datos, siga estos pasos:  
  
1.  **Crear una nueva instancia del objeto.**  
  
     Para crear una nueva instancia del objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, llame al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
2.  **Identificar los metadatos.**  
  
     Además de recuperar datos, ADOMD.NET también recupera metadatos para el objeto CellSet. Tan pronto como el comando haya ejecutado la consulta y devuelto un objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, puede recuperar los metadatos a través de varios objetos. Estos metadatos son necesarios para que las aplicaciones cliente puedan interactuar con los datos del objeto CellSet y mostrarlos. Por ejemplo, muchas aplicaciones cliente proporcionan funcionalidad para explorar en profundidad una posición especificada en un objeto CellSet o mostrar de forma jerárquica sus posiciones secundarias.  
  
     En ADOMD.NET, las propiedades <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> y <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> representan los metadatos de los ejes de consulta y segmentador, respectivamente, en el objeto CellSet devuelto. Ambas propiedades devuelven referencias a los objetos <xref:Microsoft.AnalysisServices.AdomdClient.Axis> que, a su vez, contienen las posiciones representadas en cada eje.  
  
     Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.Axis> contiene una colección de objetos <xref:Microsoft.AnalysisServices.AdomdClient.Position> que representan el conjunto de tuplas disponible para ese eje. Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.Position> representa una sola tupla que contiene uno o más miembros, representados por una colección de objetos <xref:Microsoft.AnalysisServices.AdomdClient.Member>.  
  
3.  **Recuperar datos de la colección de conjunto de celdas.**  
  
     Además de recuperar metadatos, ADOMD.NET también recupera datos para el objeto CellSet. Tan pronto como el comando haya ejecutado la consulta y devuelto un objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, puede recuperar los datos mediante la colección <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>. Esta colección contiene los valores que se calculan para la intersección de todos los ejes de la consulta. Por lo tanto, hay varios indizadores para obtener acceso a cada intersección o celda. Para obtener una lista de indizadores, vea <xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>.  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>Ejemplo de recuperación de datos en estado conectado  
 En el ejemplo siguiente se realiza una conexión con el servidor local y, a continuación, se ejecuta un comando en la conexión. En el ejemplo se analizan los resultados con el modelo de objetos `CellSet`: los títulos (metadatos) de las columnas se recuperan del primer eje y los títulos (metadatos) de cada fila se recuperan del segundo eje; los datos en intersección se recuperan mediante la colección <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A>.  
  
 [!code-csharp[Adomd.NetClient#ReturnCommandUsingCellSet](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#returncommandusingcellset)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>Recuperar datos en estado desconectado  
 Al cargar XML devuelto por una consulta anterior, puede utilizar el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> para proporcionar un completo método de exploración de datos analíticos sin necesidad de utilizar una conexión activa.  
  
> [!NOTE]  
>  En estado desconectado, no están disponibles todas las propiedades de los objetos disponibles en el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>. Para obtener más información, consulta <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>.  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>Ejemplo de recuperación de datos en estado desconectado  
 El ejemplo siguiente es similar al ejemplo de metadatos y datos que se muestra anteriormente en este tema. Sin embargo, el comando del ejemplo siguiente se ejecuta con una llamada a <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> y el resultado se devuelve como `System.Xml.XmlReader`. A continuación, el ejemplo rellena el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> utilizando `System.Xml.XmlReader` con el método <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>. Aunque este ejemplo carga `System.Xml.XmlReader` de forma inmediata, puede almacenar en caché el XML que contiene el lector en un disco duro o transportar dichos datos a otra aplicación a través de cualquier medio antes de cargar los datos en un objeto CellSet.  
  
 [!code-csharp[Adomd.NetClient#DemonstrateDisconnectedCellset](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#demonstratedisconnectedcellset)]  
  
## <a name="see-also"></a>Vea también  
 [Recuperar datos de un origen de datos analíticos](retrieving-data-from-an-analytical-data-source.md)   
 [Recuperar datos mediante AdomdDataReader](retrieving-data-using-the-adomddatareader.md)   
 [Recuperación de datos mediante XmlReader](retrieving-data-using-the-xmlreader.md)  
  
  
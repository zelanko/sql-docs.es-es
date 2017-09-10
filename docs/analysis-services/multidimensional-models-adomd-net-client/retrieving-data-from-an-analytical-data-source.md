---
title: "Recuperar datos de un origen de datos analíticos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556199fee738eae00a448ce09da07b6ab825d37a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Recuperar datos de un origen de datos analíticos
  Una vez que realiza una conexión y crea la consulta, puede recuperar cualquier dato. En ADOMD.NET, también puede recuperar los datos mediante tres objetos distintos (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, y <xref:System.Xml.XmlReader>) llamando a uno de los **Execute** métodos de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> objeto.  
  
 Cada uno de estos tres objetos equilibra la interactividad y la sobrecarga:  
  
-   *Interactividad* hace referencia a la facilidad de uso y la cantidad de información disponible a través del modelo de objeto.  
  
-   *Sobrecarga* hace referencia a la cantidad de tráfico que genera un modelo de objetos a través de la conexión de red al servidor, la cantidad de memoria necesaria para el modelo de objetos y la velocidad con la que el modelo de objetos recupera datos.  
  
 Para ayudarle a seleccionar el objeto de recuperación de datos que mejor se ajusta a las necesidades de su aplicación, en la tabla siguiente se resaltan las diferencias entre interactividad y sobrecarga para cada objeto.  
  
|Object|Interactividad|Sobrecarga|Conserva las dimensiones|Información de uso|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Máxima|Ligeramente elevada, lo que da como resultado una recuperación más lenta de los datos|Sí|[Recuperar datos mediante el conjunto de celdas](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|Moderada|Moderada|No|[Llenar un DataSet desde un DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|Moderada|Moderada|No|[Recuperar datos mediante AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Más bajo|Mínima, lo que da como resultado una recuperación más rápida de los datos|Sí|[Recuperar datos mediante XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  

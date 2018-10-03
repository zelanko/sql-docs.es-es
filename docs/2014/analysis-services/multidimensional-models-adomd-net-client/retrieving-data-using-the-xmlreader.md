---
title: Recuperar datos mediante XmlReader | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: caa8ef058839fb3c97a9e3dfdf6022dd91bc2053
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165695"
---
# <a name="retrieving-data-using-the-xmlreader"></a>Recuperar datos mediante XmlReader
  La clase `XmlReader`, parte del espacio de nombres `System.Xml` para la Biblioteca de clases de Microsoft .NET Framework, es similar a la clase <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> en que la clase `XmlReader` también proporciona acceso rápido, sin caché y de solo avance a los datos. Si no es necesaria una vista en memoria y analítica de los datos mediante el objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, el objeto `XmlReader` es perfecto para recuperar datos XML, especialmente grandes cantidades de datos. Dado que `XmlReader` transmite datos por secuencias, `XmlReader` no tiene que recuperar y almacenar en caché todos los datos antes de exponerlos al autor de las llamada, que sería el caso si se utilizara un objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> para convertir la respuesta de XML for Analysis en una representación de modelo de objetos analítico.  
  
 La clase `XmlReader` proporciona acceso directo a la respuesta de XML for Analysis que recibe ADOMD.NET cuando se llama al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>. Debido a que los datos recuperados son XML sin formato, debe analizar los datos y metadatos de forma manual. En cuanto se hayan recuperado los datos, se debería cerrar el objeto `XmlReader`.  
  
## <a name="retrieving-data-and-metadata"></a>Recuperar datos y metadatos  
 Si desea usar la clase `XmlReader` para recuperar datos, siga estos pasos:  
  
1.  **Crear una nueva instancia del objeto.**  
  
     Para crear una nueva instancia de la clase `XmlReader`, llame al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
2.  **Recuperar datos.**  
  
     Una vez que el comando ejecuta la consulta y devuelve `XmlReader`, debe analizar los datos y metadatos. Los datos y metadatos XML se presentan en el formato nativo que utiliza el proveedor XML for Analysis. Para la mayoría de los proveedores XML for Analysis, el formato nativo es el formato `MDDataSet`. El formato `MDDataSet` proporciona datos y metadatos para conjuntos de celdas en un formato estructurado. Para obtener más información acerca del formato `MDDataSet`, vea la especificación de XML for Analysis.  
  
3.  **Cierre el lector.**  
  
     Siempre se debe llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> cuando se haya terminado de utilizar el objeto `XmlReader`. Mientras `XmlReader` está abierto, `XmlReader` tiene uso exclusivo del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> que se utilizó para ejecutar el comando. No podrá ejecutar cualquier comando mediante <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, incluido crear otro `XmlReader` o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, hasta que cierre el `XmlReader`original.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>Ejemplo de recuperación de datos desde XmlReader  
 En el ejemplo siguiente se ejecuta un comando y se recuperan los datos como `XmlReader`, generando el contenido del archivo a la consola.  
  
 [!code-csharp[Adomd.NetClient#OutputDataWithXML](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#outputdatawithxml)]  
  
## <a name="see-also"></a>Vea también  
 [Recuperación de datos de origen de datos analíticos](retrieving-data-from-an-analytical-data-source.md)   
 [Recuperar datos mediante el objeto CellSet](retrieving-data-using-the-cellset.md)   
 [Recuperación de datos mediante AdomdDataReader](retrieving-data-using-the-adomddatareader.md)  
  
  

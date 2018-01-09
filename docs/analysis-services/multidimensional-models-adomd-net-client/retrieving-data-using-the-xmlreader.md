---
title: Recuperar datos mediante XmlReader | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 70b268a896a7acbbf515ac49a722eccb17afdfd8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="retrieving-data-using-the-xmlreader"></a>Recuperar datos mediante XmlReader
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]El **XmlReader** de la clase, parte de la **System.Xml** es similar al espacio de nombres para la biblioteca de clases de Microsoft .NET Framework, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> clase en que la **XmlReader**clase también proporciona un rápido, acceso a datos sin almacenamiento en caché y solo avance. Si no es necesario para obtener una vista en memoria y analítica de los datos mediante la <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto, el **XmlReader** objeto es perfecto para recuperar datos XML, especialmente para grandes cantidades de datos. Dado que **XmlReader** vierte los datos, **XmlReader** no tiene que recuperar y almacenar en caché todos los datos antes de exponerlos al llamador, como sería el caso cuando un <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto se usa para convertir el Respuesta de XML for Analysis en una representación del modelo de objetos analítico.  
  
 El **XmlReader** clase proporciona acceso directo al XML de respuesta de análisis recibida ADOMD.NET cuando la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> método de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> se denomina objeto. Debido a que los datos recuperados son XML sin formato, debe analizar los datos y metadatos de forma manual. Tan pronto como se ha recuperado los datos, el **XmlReader** debe cerrar el objeto.  
  
## <a name="retrieving-data-and-metadata"></a>Recuperar datos y metadatos  
 Para usar el **XmlReader** de clases para recuperar datos, siga estos pasos:  
  
1.  **Crear una nueva instancia del objeto.**  
  
     Para crear una nueva instancia de la **XmlReader** (clase), se llama a la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> método de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> objeto.  
  
2.  **Recuperar los datos.**  
  
     Después de que el comando se ejecuta la consulta y devuelve un **XmlReader**, debe analizar los datos y metadatos. Los datos y metadatos XML se presentan en el formato nativo que utiliza el proveedor XML for Analysis. En la mayoría del XML para los proveedores de análisis, el formato nativo es el **MDDataSet** formato. El **MDDataSet** formato proporciona datos y metadatos para conjuntos de celdas en un formato estructurado. Para obtener más información sobre la **MDDataSet** de formato, vea la especificación de XML for Analysis.  
  
3.  **Cierre el lector.**  
  
     Siempre debe llamar a la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método cuando haya terminado de utilizar el **XmlReader** objeto. Mientras un **XmlReader** está abierto, **XmlReader** tiene uso exclusivo de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto que se usó para ejecutar el comando. No será capaz de ejecutar cualquier comando mediante <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, incluida la creación de otro **XmlReader** o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, hasta que se cierra el original **XmlReader**.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>Ejemplo de recuperación de datos desde XmlReader  
 En el ejemplo siguiente se ejecuta un comando y recupera los datos como un **XmlReader**, generando el contenido del archivo en la consola.  
  
 [!code-cs[Adomd.NetClient#OutputDataWithXML](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_1_1.cs)]  
  
## <a name="see-also"></a>Vea también  
 [Recuperar datos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Recuperar datos mediante el conjunto de celdas](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [Recuperación de datos mediante AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)  
  
  

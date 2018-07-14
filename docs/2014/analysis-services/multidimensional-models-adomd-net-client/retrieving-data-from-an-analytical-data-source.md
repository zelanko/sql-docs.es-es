---
title: Recuperación de datos de origen de datos analíticos | Microsoft Docs
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
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e5595bd4e001b006cb1dfe62cba40cee3bbb30c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196425"
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Recuperar datos de un origen de datos analíticos
  Una vez que realiza una conexión y crea la consulta, puede recuperar cualquier dato. En ADOMD.NET puede recuperar datos mediante tres objetos distintos (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> y <xref:System.Xml.XmlReader>); para ello, llame a uno de los métodos `Execute` del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
 Cada uno de estos tres objetos equilibra la interactividad y la sobrecarga:  
  
-   *Interactividad* hace referencia a la facilidad de uso y la cantidad de información disponible a través del modelo de objetos.  
  
-   *Sobrecarga* hace referencia a la cantidad de tráfico que genera un modelo de objetos a través de la conexión de red al servidor, la cantidad de memoria necesaria para el modelo de objetos y la velocidad con que el modelo de objetos recupera datos.  
  
 Para ayudarle a seleccionar el objeto de recuperación de datos que mejor se ajusta a las necesidades de su aplicación, en la tabla siguiente se resaltan las diferencias entre interactividad y sobrecarga para cada objeto.  
  
|Objeto|Interactividad|Sobrecarga|Conserva las dimensiones|Información de uso|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Máxima|Ligeramente elevada, lo que da como resultado una recuperación más lenta de los datos|Sí|[Recuperación de datos mediante el objeto CellSet](retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|Moderada|Moderada|no|[Rellenar un conjunto de datos desde un objeto DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|Moderada|Moderada|no|[Recuperación de datos mediante AdomdDataReader](retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Más bajo|Mínima, lo que da como resultado una recuperación más rápida de los datos|Sí|[Recuperación de datos mediante XmlReader](retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente de ADOMD.NET](adomd-net-client-programming.md)  
  
  

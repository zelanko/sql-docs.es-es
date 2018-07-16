---
title: Ejecutar comandos en un origen de datos analíticos | Microsoft Docs
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
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36d94ba3ae75f2b3d59e0fb159ee639a5f2edb43
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202025"
---
# <a name="executing-commands-against-an-analytical-data-source"></a>Ejecutar comandos en un origen de datos analíticos
  Después de establecer una conexión a un origen de datos analíticos, puede usar un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para ejecutar con comandos y resultados devueltos de ese origen de datos. Estos comandos pueden recuperar datos mediante expresiones multidimensionales (MDX), extensiones de minería de datos (DMX), o incluso una sintaxis limitada de SQL. Además, puede usar los comandos ASSL (Analysis Services Scripting Language) para modificar la base de datos subyacente.  
  
## <a name="creating-a-command"></a>Crear un comando  
 Antes de ejecutar un comando, debe crearlo. Puede crear un comando mediante uno de los dos métodos siguientes:  
  
-   El primer método usa el constructor <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>, que puede tomar un comando para ejecutarlo en el origen de datos y un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> para ejecutar el comando.  
  
-   El segundo método usa el método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 El texto del comando para ejecutar se puede consultar y modificar mediante la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A>. Los comandos que crea no tienen que devolver los datos después de ejecutarse.  
  
## <a name="running-a-command"></a>Ejecutar un comando  
 Después de crear un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>, hay varios métodos <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> que el comando puede usar para realizar varias acciones. En la tabla siguiente se enumeran algunas de estas acciones.  
  
|A|Use este método|  
|--------|---------------------|  
|Devolver resultados como un flujo de datos|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> para devolver un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|  
|Devolver un objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|Ejecutar comandos que no devuelven filas|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|Devolver un objeto `XMLReader` que contiene los datos en un formato compatible de XML for Analysis (XMLA)|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>Ejemplo de cómo ejecutar un comando  
 En este ejemplo se usa <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para ejecutar un comando XMLA que procesará el cubo `Adventure Works DW` en el servidor local, sin devolver los datos.  
  
 [!code-csharp[Adomd.NetClient#ExecuteXMLAProcessCommand](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#executexmlaprocesscommand)]  
  
  

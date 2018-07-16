---
title: Programación del cliente ADOMD.NET | Microsoft Docs
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
- programming [ADOMD.NET]
- ADOMD.NET, programming
ms.assetid: 55156115-ecd1-4ed9-876e-23406af9bbf9
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd4884abb345f1254c3987acb06e83ced7bcf392
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332755"
---
# <a name="adomdnet-client-programming"></a>Programación del cliente ADOMD.NET
  Los componentes del cliente de ADOMD.NET residen dentro del espacio de nombres `Microsoft.AnalysisServices.AdomdClient` (en microsoft.analysisservices.adomdclient.dll). Estos componentes cliente proporcionan funcionalidad para el cliente y aplicaciones de nivel intermedio para consultar fácilmente los datos y metadatos de un almacén de datos analíticos, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="using-the-adomdnet-client-objects"></a>Usar los objetos de cliente de ADOMD.NET  
 Para consultar un origen de datos analíticos, se deben realizar un conjunto de tareas comunes. En la tabla siguiente se representan las tareas comunes en las que se usan los objetos de cliente de ADOMD.NET para realizar este tipo de consulta.  
  
|Tarea|Descripción|  
|----------|-----------------|  
|[Establecer conexiones en ADOMD.NET](connections-in-adomd-net.md)|En ADOMD.NET, se usa un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> para establecer conexiones con orígenes de datos analíticos, como las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede usar el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> para ejecutar comandos, recuperar datos y recuperar metadatos del origen de datos analíticos.|  
|[Recuperación de metadatos de un origen de datos analíticos](retrieving-metadata-from-an-analytical-data-source.md)|Una vez establecida una conexión, puede usar una gran variedad de objetos para recuperar información del origen de datos subyacente. Esta funcionalidad permite a las aplicaciones adaptarse al origen de datos al que se han conectado.|  
|[Ejecución de comandos en un origen de datos analíticos](executing-commands-against-an-analytical-data-source.md)|El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> proporciona las interfaces necesarias para ejecutar comandos en el origen de datos analíticos subyacente.|  
|[Recuperación de datos de un origen de datos analíticos](retrieving-data-from-an-analytical-data-source.md)|Una vez que se ejecuta un comando, los datos se pueden recuperar y analizar mediante los objetos <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> o `System.XmlReader`.|  
|[Realizar transacciones en ADOMD.NET](../../relational-databases/native-client-ole-db-transactions/transactions.md)|Todas las acciones enumeradas en las filas anteriores de esta tabla pueden tener lugar dentro de una transacción de lectura confirmada, que contiene los bloqueos compartidos mientras los datos se leen para evitar lecturas no actualizadas. Los datos se pueden cambiar antes de que finalice la transacción, lo que da como resultado lecturas no repetibles o datos fantasma. El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> proporciona la funcionalidad de la transacción en ADOMD.NET.|  
  
 La interacción con la jerarquía de objetos ADOMD.NET suele comenzar con uno o más de los objetos del nivel superior, como se describe en la tabla siguiente.  
  
|A|Utilice este objeto|  
|--------|---------------------|  
|Conectar al origen de datos analíticos|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> representa una conexión a un origen de datos y los metadatos del origen de datos. Por ejemplo, puede conectarse a un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo (.cub) de archivo y, a continuación, examine el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> propiedad para obtener metadatos sobre los cubos presentes en el origen de datos analíticos. Este objeto también representa la implementación de la interfaz `IDbConnection`, una interfaz que requieren todos los proveedores de datos de .NET Framework.|  
|Detectar las capacidades de la minería de datos del origen de datos|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> expone varias colecciones de minería de datos:<br /><br /> -El <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> contiene una lista de cada modelo de minería de datos del origen de datos.<br />-El <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> proporciona información acerca de los algoritmos de minería de datos disponibles.<br />-El <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> expone información sobre las estructuras de minería de datos en el servidor.|  
|Consultar el origen de datos|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> representa la instrucción o consulta que se enviará al servidor. Una vez establecida una conexión a un origen de datos, use un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para ejecutar instrucciones en el lenguaje compatible, como Expresiones multidimensionales (MDX) o Extensiones de minería de datos (DMX). También puede usar un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para devolver resultados como objetos <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.|  
|Recuperar datos de una manera rápida y eficaz|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> se puede crear con una llamada al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> de un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>. Este objeto implementa la interfaz `IDbDataReader` del espacio de nombres `System.Data` de la biblioteca de clases de.NET Framework.|  
|Recuperar datos analíticos con la máxima cantidad de metadatos|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> se puede crear con una llamada al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>. Cuando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> devuelve <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, puede examinar los datos analíticos que contiene <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>.|  
|Recuperar los metadatos sobre cubos, como dimensiones disponibles, medidas, conjuntos con nombre, etc.|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> representa los metadatos sobre un cubo. Hace referencia a <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> desde <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.|  
|Recuperar datos mediante la interfaz `System.Data.IDbDataAdapter`|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter> proporciona compatibilidad de solo lectura para las aplicaciones cliente de .NET Framework existentes.|  
  
## <a name="see-also"></a>Vea también  
 [Programación del servidor ADOMD.NET](../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [Desarrollo con ADOMD.NET](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  

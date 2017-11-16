---
title: La funcionalidad de cliente de ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: 0f5e16a1-dc2d-4c87-8551-985921bf069b
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 0a1047fbccf3e9437c3160891f502f9e2838c34a
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="adomdnet-client-functionality"></a>Funcionalidad de cliente de ADOMD.NET
  ADOMD.NET actúa como un puente entre una aplicación y un origen de datos, como ocurre con otros proveedores de datos de .NET Framework [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Sin embargo, ADOMD.NET, a diferencia de otros proveedores de datos de .NET Framework en ese ADOMD.NET, funciona con datos analíticos. Para funcionar con datos analíticos, ADOMD.NET admite una funcionalidad muy distinta de la funcionalidad de otros proveedores de datos de .NET Framework. ADOMD.NET no solo permite recuperar datos, sino también metadatos y cambiar la estructura del almacén de datos analíticos:  
  
 **Recuperación de metadatos**  
 Las aplicaciones pueden obtener más información sobre los datos que se pueden recuperar desde el origen de datos a través de la recuperación de metadatos, mediante conjuntos de filas de esquema o del modelo de objetos. Se reconoce toda la información, como los tipos disponibles de cada indicador clave de rendimiento (KPI), las dimensiones de un cubo y los parámetros que necesitan los modelos de minería de datos. Los metadatos son más importantes para *dinámica* las aplicaciones que requieren intervención del usuario para determinar el tipo, profundidad y ámbito de los datos que va a recuperar. En los ejemplos se incluye el Analizador de consultas, Microsoft Excel y otras herramientas para realizar consultas. Los metadatos son menos críticos para *estático* las aplicaciones que realizan un conjunto predefinido de acciones.  
  
 Para obtener más información: [recuperación de metadatos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md).  
  
 **Recuperación de datos**  
 La recuperación de datos es la recuperación real de la información almacenada en el origen de datos. La recuperación de datos es la función primaria de las aplicaciones "estáticas", que conocen la estructura del origen de datos. Además, la recuperación de datos es el resultado final de las aplicaciones "dinámicas". El valor del KPI para una hora determinada del día, el número de bicicletas vendidas en la última hora en cada almacén y los factores que rigen el rendimiento anual de los empleados, son ejemplos de datos que se pueden recuperar. Recuperar datos es vital para cualquier aplicación de consulta.  
  
 Para obtener más información: [recuperar datos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md).  
  
 **Cambiar la estructura de los datos analíticos**  
 ADOMD.NET también se pueden usar para cambiar realmente la estructura del almacén de datos analíticos. Aunque esto se realiza normalmente a través de AMO (Objetos de administración de análisis), puede usar ADOMD.NET para enviar comandos de ASSL (Analysis Services Scripting Language) para crear, modificar o eliminar objetos en el servidor.  
  
 Para obtener más información: [ejecutar comandos en un analíticos origen de datos](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md), [desarrollar con Analysis Management Objects &#40; AMO &#41; ](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md), [De analysis Services Scripting Language &#40; ASSL para XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 Cada recuperación de metadatos, recuperación de datos y cambio de la estructura de datos, se produce en un momento determinado del flujo de trabajo de una aplicación típica de ADOMD.NET.  
  
## <a name="typical-process-flow"></a>Flujo típico del proceso  
 Normalmente, las aplicaciones de ADOMD.NET tradicionales siguen el mismo flujo de trabajo cuando trabajan con una base de datos analítica:  
  
1.  Primero, se realiza una conexión a la base de datos, mediante el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Al abrir la conexión, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> expone los metadatos del servidor al que ha realizado la conexión. En una aplicación dinámica, normalmente parte de esta información se muestra al usuario de manera pueda realizar una selección, como qué cubo desea consultar. La aplicación puede volver a usar varias veces la conexión creada en este paso, reduciendo la sobrecarga.  
  
     Para obtener más información: [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  Una vez realizada una conexión, una aplicación dinámica realizaría una consulta al servidor acerca de metadatos más concretos. En una aplicación estática, el programador conoce de antemano los objetos que la aplicación consultará y así no necesitará recuperar estos metadatos. Tanto la aplicación como el usuario pueden usar los metadatos que se recuperan en el paso siguiente.  
  
     Para obtener más información: [recuperación de metadatos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  A continuación, la aplicación ejecuta un comando en el servidor. Este comando puede ser para recuperar metadatos adicionales, recuperar datos o modificar la estructura de base de datos. Para cualquiera de estas tareas, la aplicación podría usar una consulta previamente determinada o hacer uso de los metadatos recién recuperados para crear consultas adicionales.  
  
     Para obtener más información: [recuperación de metadatos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [recuperar datos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), [ejecuta comandos contra un analíticos origen de datos](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  Una vez enviado el comando al servidor, éste inicia la devolución de los metadatos o datos al cliente. Esta información puede verse mediante el uso de un <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto, un <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> objeto, o un **System.XmlReader** objeto.  
  
 Para ilustrar este flujo de trabajo tradicional, en el ejemplo siguiente se incluye un método que abre una conexión a la base de datos, ejecuta un comando con un cubo conocido y recupera los resultados en un conjunto de celdas. A continuación, el conjunto de celdas devuelve una cadena delimitada por tabuladores que contiene encabezados de columna, encabezados de fila y datos de celda.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente de ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  


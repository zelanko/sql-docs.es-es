---
title: Para establecer conexiones en ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- opening connections
- closing connections
- connections [ADOMD.NET]
- ADOMD.NET, connections
ms.assetid: 7b9610f5-6641-42cc-af4e-bd35771913d1
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7c3555be8e304add34cba3a8dd9f0bac4264216
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="connections-in-adomdnet"></a>Conexiones en ADOMD.NET
  En ADOMD.NET, usa el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto para abrir conexiones con orígenes de datos analíticos, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bases de datos. Cuando la conexión ya no sea necesaria, deberá cerrarla explícitamente.  
  
## <a name="opening-a-connection"></a>Abrir una conexión  
 Para abrir una conexión en ADOMD.NET, primero debe especificar una cadena de conexión a una base de datos y un origen de datos analíticos válidos. A continuación, debe abrir explícitamente la conexión a ese origen de datos.  
  
### <a name="specifying-a-multidimensional-data-source"></a>Especificar un origen de datos multidimensionales  
 Para especificar una base de datos y un origen de datos analíticos, establezca la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. La cadena de conexión especificada para la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> es una cadena compatible con OLE DB. ADOMD.NET utiliza la cadena de conexión especificada para determinar cómo conectarse al servidor.  
  
 La propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> se puede establecer en un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> existente o durante la creación de una instancia de un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. En el código siguiente se muestra cómo establecer la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> al crear una conexión ADOMD:  
  
```vb  
Dim advwrksConnection As New AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS")  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString)  
```  
  
```csharp  
AdomdConnection advwrksConnection = new AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS");  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString);  
```  
  
### <a name="opening-a-connection-to-the-data-source"></a>Abrir una conexión con el origen de datos.  
 Una vez especificada la cadena de conexión, debe utilizar el método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> para abrir la conexión. Al abrir un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, puede establecer varios niveles de seguridad para la conexión. El nivel de seguridad que se usa para la conexión depende del valor de la **ProtectionLevel** configuración de la cadena de conexión. Para obtener más información acerca de cómo abrir conexiones seguras en ADOMD.NET, consulte [establecer conexiones seguras en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md).  
  
## <a name="working-with-a-connection"></a>Trabajar con una conexión  
 Cada conexión abierta tiene lugar en una sesión, lo que proporciona compatibilidad con las operaciones con estado. Una sesión puede compartirse entre varias conexiones abiertas. Compartir una sesión permite que más de un cliente comparta el mismo contexto. Para obtener más información, consulte [trabajar con conexiones y sesiones en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md).  
  
 Puede utilizar una conexión abierta para recuperar metadatos y datos y ejecutar comandos. Para obtener más información, consulte [recuperación de metadatos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [recuperar datos de un origen de datos analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), y [ejecutar comandos en un datos analíticos Origen](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md).  
  
 Cuando la conexión está abierta, puede recuperar datos y metadatos y ejecutar comandos desde una transacción de lectura confirmada, en la que se mantienen los bloqueos compartidos mientras se leen los datos para evitar la lectura de datos sucios. Los datos se pueden cambiar antes de que finalice la transacción, lo que da como resultado lecturas no repetibles o datos fantasma. Para obtener más información, consulte [realizar transacciones en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md).  
  
## <a name="closing-a-connection"></a>Cerrar una conexión  
 Se recomienda que cierre explícitamente un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tan pronto como la conexión deje de ser necesaria. Para cerrar la conexión explícitamente, utilice la **cerrar** y **Dispose** métodos de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto.  
  
 Es posible que una conexión que no se cierra explícitamente, pero a la que se le permite salir de su ámbito, no pueda liberar los recursos del servidor lo suficientemente rápido como para permitir que las aplicaciones cliente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con simultaneidad elevada abran nuevas conexiones de forma eficaz. En función de cómo haya creado la conexión, la sesión utilizada por el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> puede permanecer activa si no se cierra la conexión explícitamente.  
  
 Para obtener más información acerca de las sesiones, consulte [trabajar con conexiones y sesiones en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md).  
  
> [!IMPORTANT]  
>  En el **Finalize** método de cualquier clase implementada, no llame a la **cerrar** o **Dispose** métodos de un <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> objeto, o cualquier otra objeto administrado. En un finalizador, libere solamente los recursos no administrados que pertenezcan directamente a la clase implementada. Si la clase implementada no dispone de recursos no administrados, no incluya un **Finalize** método en la definición de clase.  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  

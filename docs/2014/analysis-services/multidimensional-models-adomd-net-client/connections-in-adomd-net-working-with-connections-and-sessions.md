---
title: Trabajar con conexiones y sesiones en ADOMD.NET | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 07c17333b58d34a99e8d393a1dbc8ec00d75f60e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197046"
---
# <a name="working-with-connections-and-sessions-in-adomdnet"></a>Trabajar con conexiones y sesiones en ADOMD.NET
  En XML for Analysis (XMLA), las sesiones proporcionan compatibilidad para las operaciones con estado durante el acceso a datos analíticos. Las sesiones enmarcan el ámbito y contexto de comandos y transacciones para un origen de datos analíticos. Los elementos XMLA utilizados para administrar sesiones son [BeginSession](../xmla/xml-elements-headers/beginsession-element-xmla.md), [Session](../xmla/xml-elements-headers/session-element-xmla.md)y [EndSession](../xmla/xml-elements-headers/endsession-element-xmla.md).  
  
 ADOMD.NET usa estos tres elementos de sesión XMLA cuando se inicia una sesión, se realizan consultas o se recuperan datos durante la sesión, además de cerrar una sesión.  
  
## <a name="starting-a-session"></a>Iniciar un sesión  
 La propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> contiene el identificador de la sesión activa asociada al objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Utilizando correctamente esta propiedad, puede controlar eficazmente la disponibilidad de estados de cliente y de servidor en su aplicación:  
  
-   Si la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> no está establecida en un identificador de sesión válido cuando se llama al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A>, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> solicita un nuevo identificador de sesión del proveedor. ADOMD.NET inicia una sesión enviando un encabezado `BeginSession` de XMLA al proveedor. Si ADOMD.NET inicia una sesión correctamente, ADOMD.NET establece el valor de la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> en el identificador de sesión de la sesión recién creada.  
  
-   Si la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> está establecida en un identificador de sesión válido cuando se llama al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A>, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> intenta realizar la conexión a la sesión especificada.  
  
 Si el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> no se puede conectar a la sesión especificada, o si el proveedor no admite sesiones, se produce una excepción.  
  
> [!NOTE]  
>  Después de que ADOMD.NET haya creado una sesión, puede conectar varios objetos <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> a esa única sesión activa o bien puede desconectar un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> único de esa sesión y volver a conectar ese objeto a otra sesión.  
  
## <a name="working-in-a-session"></a>Trabajar en una sesión  
 Después de que ADOMD.NET conecta el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> a una sesión válida, ADOMD.NET enviará un encabezado `Session` de XMLA al proveedor con cada solicitud de datos o metadatos realizada por una aplicación. Cada solicitud tendrá el identificador de sesión establecido en el valor de la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>.  
  
 Un identificador de sesión no garantiza que una sesión siga siendo válida. Si la sesión expira (por ejemplo, se agota el tiempo de espera de la sesión o se pierde la conexión), el proveedor puede optar por finalizar y revertir las acciones de esa sesión. Si esto se produce, todas las llamadas subsiguientes al método del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> producirán una excepción. Dado que solo se producen las excepciones cuando la solicitud siguiente se envía al proveedor, no cuando la sesión expira, su aplicación debe ser capaz de manejar estas excepciones cada vez que recupere datos o metadatos del proveedor.  
  
## <a name="closing-a-session"></a>Cerrar una sesión  
 Si el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método se llama sin especificar el valor de la *endSession* parámetro, o si la *endSession* parámetro está establecido en True, tanto la conexión a la sesión y la sesión asociado con el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se cierra el objeto. Para cerrar una sesión, ADOMD.NET envía un encabezado `EndSession` de XMLA al proveedor, con el identificador de sesión establecido en el valor de la propiedad <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>.  
  
 Si el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método se llama con la *endSession* parámetro establecido en False, la sesión asociada con el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto permanece activo pero se cierra la conexión a la sesión.  
  
## <a name="example-of-managing-a-session"></a>Ejemplo de administración de una sesión  
 En el ejemplo siguiente se muestra cómo abrir una conexión, crear una sesión y cerrar la conexión manteniendo la sesión abierta en ADOMD.NET:  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Para establecer conexiones en ADOMD.NET](connections-in-adomd-net.md)  
  
  
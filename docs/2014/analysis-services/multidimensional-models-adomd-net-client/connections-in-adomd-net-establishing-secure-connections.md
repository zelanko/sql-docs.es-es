---
title: Establecer conexiones seguras en ADOMD.NET | Microsoft Docs
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
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d97079ca400d92502cf3ff217137eb6f32d1920d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180862"
---
# <a name="establishing-secure-connections-in-adomdnet"></a>Establecer conexiones seguras en ADOMD.NET
  Al utilizar una conexión en ADOMD.NET, el método de seguridad que se utiliza para la conexión depende del valor de la propiedad `ProtectionLevel` de la cadena de conexión utilizada al llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 La propiedad `ProtectionLevel` proporciona cuatro niveles de seguridad: no autenticada, autenticada, firmada y cifrada. En la tabla siguiente se describen estos distintos niveles de seguridad.  
  
> [!NOTE]  
>  Si elige utilizar una agrupación de conexiones de bases de datos, no se podrá administrar la seguridad en la base de datos. Esto se debe a que la agrupación de conexiones de bases de datos requiere que la cadena de conexión sea idéntica para agrupar las conexiones. Por lo tanto, deberá administrar la seguridad en otra parte.  
  
|Nivel de seguridad|Valor de ProtectionLevel|  
|--------------------|---------------------------|  
|*conexión no autenticada*<br /> Una conexión no autenticada no realiza ninguna forma de autenticación. Este tipo de conexión es la forma de conexión con mayor grado de compatibilidad, pero menos segura.|`None`|  
|*conexión autenticada*<br /> Una conexión autenticada realiza la autenticación del usuario que establece la conexión, pero no protege las comunicaciones adicionales. Este tipo de conexión es útil porque puede establecer la identidad del usuario o la aplicación que se conecta a un origen de datos analíticos.|`Connect`|  
|*conexión firmada*<br /> Una conexión firmada autentica al usuario que solicita la conexión y, a continuación, se asegura de que no se modifican las transmisiones. Este tipo de conexión es útil cuando debe comprobarse la autenticidad de los datos transferidos. Sin embargo, una conexión firmada solo impide que se pueda modificar el contenido del paquete de datos, pero dicho contenido se puede ver durante el tránsito. **Nota:** una conexión firmada solo es compatible con el proveedor XML for Analysis proporcionado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|`Pkt Integrity` o `PktIntegrity`|  
|*conexión cifrada*<br /> Una conexión cifrada es el tipo de conexión predeterminada que utiliza ADOMD.NET. Este tipo de conexión autentica al usuario que solicita la conexión y, a continuación, también cifra los datos que se transmiten. Una conexión cifrada es la forma de conexión más segura que puede crearse con ADOMD.NET. El contenido del paquete de datos no se puede ver ni modificar, lo que protege los datos durante el tránsito. **Nota:** una conexión cifrada solo es compatible con el proveedor XML for Analysis proporcionado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|`Pkt Privacy` o `PktPrivacy`|  
  
 Sin embargo, no todos los niveles de seguridad están disponibles para todos los tipos de conexiones:  
  
-   Una conexión TCP puede utilizar cualquiera de los cuatro niveles de seguridad. De hecho, una conexión TCP que se utiliza con la seguridad integrada de Windows, ofrece el método más seguro de conexión con un origen de datos analíticos.  
  
-   Una conexión HTTP solo puede ser una conexión autenticada. Por lo tanto, la propiedad `ProtectionLevel` debe establecerse en `Connect`.  
  
-   Una conexión HTTPS solo puede ser una conexión cifrada. Por lo tanto, la propiedad `ProtectionLevel` debe establecerse en `Pkt Privacy` o `PktPrivacy`.  
  
## <a name="securing-tcp-connections"></a>Proteger las conexiones TCP  
 En una conexión TCP, la propiedad `ProtectionLevel` admite los cuatros niveles de seguridad, como se muestra en la tabla siguiente.  
  
|Valor de ProtectionLevel|¿Usar con conexión TCP?|Resultado|  
|---------------------------|------------------------------|-------------|  
|`None`|Sí|Especifica una conexión no autenticada.<br /><br /> Se solicita un flujo TCP del proveedor, pero no se realiza ningún tipo de autenticación del usuario que solicita el flujo.|  
|`Connect`|Sí|Especifica una conexión autenticada.<br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, el contexto de seguridad del usuario que solicita el flujo se autentica en el servidor:<br /><br /> -Si la autenticación se realiza correctamente, se realiza ninguna otra acción.<br />-Si se produce un error de autenticación, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto se desconecta del origen de datos multidimensionales y se produce una excepción.<br /><br /> Una vez realizada la autenticación correctamente o con error, se elimina el contexto de seguridad utilizado para autenticar la conexión.|  
|`Pkt Integrity` o `PktIntegrity`|Sí|Especifica una conexión firmada.<br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, el contexto de seguridad del usuario que solicita el flujo se autentica en el servidor:<br /><br /> -Si la autenticación se realiza correctamente, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto cierra el flujo TCP existente y abre un flujo TCP firmado para controlar todas las solicitudes. Para autenticar cada solicitud de datos o metadatos se utiliza el contexto de seguridad empleado para abrir la conexión. Además, cada paquete se firma digitalmente para asegurarse de que la carga del paquete TCP no se ha cambiado en modo alguno.<br />-Si se produce un error de autenticación, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto se desconecta del origen de datos multidimensionales y se produce una excepción.|  
|`Pkt Privacy` o `PktPrivacy`|Sí|Especifica una conexión cifrada. **Nota:** también puede especificar una conexión cifrada si no establece la `ProtectionLevel` propiedad en la cadena de conexión. <br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, se autentica en el servidor el contexto de seguridad del usuario que solicita el flujo:<br /><br /> -Si la autenticación se realiza correctamente, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto cierra el flujo TCP existente y abre un flujo TCP cifrado para controlar todas las solicitudes. Para autenticar cada solicitud de datos o metadatos se utiliza el contexto de seguridad empleado para abrir la conexión. Además, la carga de cada paquete TCP se cifra mediante el método de cifrado de mayor nivel admitido por el proveedor y el origen de datos multidimensionales.<br />-Si se produce un error de autenticación, el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto se desconecta del origen de datos multidimensionales y se produce una excepción.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>Utilizar la seguridad integrada de Windows para la conexión  
 La seguridad integrada de Windows es la forma más segura de establecer y proteger una conexión con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La seguridad integrada de Windows no revela credenciales de seguridad (como el nombre de usuario o la contraseña) durante el proceso de autenticación, sino que utiliza el identificador de seguridad del proceso que se ejecuta actualmente para establecer la identidad. Para la mayoría de las aplicaciones cliente, este identificador de seguridad representa la identidad del usuario actualmente conectado.  
  
 Para utilizar la seguridad integrada de Windows, la cadena de conexión requiere la siguiente configuración:  
  
-   La propiedad `Integrated Security` no debe establecerse o bien debe establecerse en `SSPI`.  
  
    > [!NOTE]  
    >  La seguridad integrada de Windows solo está disponible para las conexiones TCP, ya que las conexiones HTTP deben utilizar el valor `Basic` para la propiedad `Integrated Security`.  
  
-   Para la propiedad `ProtectionLevel`, establezca esta propiedad en `Connect`, `Pkt Integrity` o `Pkt Privacy`.  
  
## <a name="securing-http-connections"></a>Proteger las conexiones HTTP  
 HTTPS y SSL (Capa de sockets seguros) se pueden utilizar para proteger las comunicaciones HTTP con un origen de datos analíticos externamente.  
  
 Dado que un proveedor XMLA solamente utiliza HTTP seguro, una conexión HTTP en ADOMD.NET debe ser una conexión firmada, como se muestra en la tabla siguiente.  
  
|Valor de ProtectionLevel|Usar con HTTP o HTTPS|  
|---------------------------|----------------------------|  
|`None`|no|  
|`Connect`|HTTP|  
|`Pkt Integrity` o `PktIntegrity`|no|  
|`Pkt Privacy` o `PktPrivacy`|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>Abrir una conexión HTTP segura  
 En el ejemplo siguiente se muestra cómo utilizar ADOMD.NET para abrir una conexión HTTP para la base de datos de ejemplo `AdventureWorksAS` de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Establecer conexiones en ADOMD.NET](connections-in-adomd-net.md)  
  
  

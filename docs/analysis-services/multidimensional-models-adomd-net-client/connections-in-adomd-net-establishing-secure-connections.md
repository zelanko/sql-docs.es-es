---
title: Establecer conexiones seguras en ADOMD.NET | Documentos de Microsoft
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7a4545dc84372ae73ba90ac0c90a8586e92afe8f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="connections-in-adomdnet---establishing-secure-connections"></a>Conexiones en ADOMD.NET - establecer conexiones seguras
  Cuando se usa una conexión en ADOMD.NET, el método de seguridad que se usa para la conexión depende del valor de la **ProtectionLevel** propiedad de cadena de conexión utilizada cuando se llama a la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> método de la <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 El **ProtectionLevel** propiedad ofrece cuatro niveles de seguridad: no autenticado, autenticado, firmados y cifrados. En la tabla siguiente se describen estos distintos niveles de seguridad.  
  
> [!NOTE]  
>  Si elige utilizar una agrupación de conexiones de bases de datos, no se podrá administrar la seguridad en la base de datos. Esto se debe a que la agrupación de conexiones de bases de datos requiere que la cadena de conexión sea idéntica para agrupar las conexiones. Por lo tanto, deberá administrar la seguridad en otra parte.  
  
|Nivel de seguridad|Valor de ProtectionLevel|  
|--------------------|---------------------------|  
|*conexión no autenticada*<br /> Una conexión no autenticada no realiza ninguna forma de autenticación. Este tipo de conexión es la forma de conexión con mayor grado de compatibilidad, pero menos segura.|**Ninguno**|  
|*conexión autenticada*<br /> Una conexión autenticada realiza la autenticación del usuario que establece la conexión, pero no protege las comunicaciones adicionales. Este tipo de conexión es útil porque puede establecer la identidad del usuario o la aplicación que se conecta a un origen de datos analíticos.|**Conectar**|  
|*conexión firmada*<br /> Una conexión firmada autentica al usuario que solicita la conexión y, a continuación, se asegura de que no se modifican las transmisiones. Este tipo de conexión es útil cuando debe comprobarse la autenticidad de los datos transferidos. Sin embargo, una conexión firmada solo impide que se pueda modificar el contenido del paquete de datos, pero dicho contenido se puede ver durante el tránsito.<br /><br /><br /><br /> Tenga en cuenta que una conexión firmada solo es compatible con el proveedor XML for Analysis proporcionado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|**Integridad Pkt** o **PktIntegrity**|  
|*conexión cifrada*<br /> Una conexión cifrada es el tipo de conexión predeterminada que utiliza ADOMD.NET. Este tipo de conexión autentica al usuario que solicita la conexión y, a continuación, también cifra los datos que se transmiten. Una conexión cifrada es la forma de conexión más segura que puede crearse con ADOMD.NET. El contenido del paquete de datos no se puede ver ni modificar, lo que protege los datos durante el tránsito.<br /><br /><br /><br /> Una conexión cifrada solo es compatible con el proveedor XML for Analysis proporcionado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|**Privacidad Pkt** o **PktPrivacy**|  
  
 Sin embargo, no todos los niveles de seguridad están disponibles para todos los tipos de conexiones:  
  
-   Una conexión TCP puede utilizar cualquiera de los cuatro niveles de seguridad. De hecho, una conexión TCP que se utiliza con la seguridad integrada de Windows, ofrece el método más seguro de conexión con un origen de datos analíticos.  
  
-   Una conexión HTTP solo puede ser una conexión autenticada. Por lo tanto, la **ProtectionLevel** propiedad debe establecerse en **conectar**.  
  
-   Una conexión HTTPS solo puede ser una conexión cifrada. Por lo tanto, la **ProtectionLevel** propiedad debe establecerse en **Privacidad Pkt** o **PktPrivacy**.  
  
## <a name="securing-tcp-connections"></a>Proteger las conexiones TCP  
 Para una conexión TCP, el **ProtectionLevel** propiedad es compatible con los cuatro niveles de seguridad, como se muestra en la tabla siguiente.  
  
|Valor de ProtectionLevel|¿Usar con conexión TCP?|Resultado|  
|---------------------------|------------------------------|-------------|  
|**Ninguno**|Sí|Especifica una conexión no autenticada.<br /><br /> Se solicita un flujo TCP del proveedor, pero no se realiza ningún tipo de autenticación del usuario que solicita el flujo.|  
|**Conectar**|Sí|Especifica una conexión autenticada.<br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, el contexto de seguridad del usuario que solicita el flujo se autentica en el servidor: si la autenticación se realiza correctamente, se realiza ninguna otra acción. Si la autenticación no se realiza correctamente, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se desconecta del origen de datos multidimensionales y se produce una excepción.<br /><br /> Una vez realizada la autenticación correctamente o con error, se elimina el contexto de seguridad utilizado para autenticar la conexión.|  
|**Integridad Pkt** o **PktIntegrity**|Sí|Especifica una conexión firmada.<br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, el contexto de seguridad del usuario que solicita el flujo se autentica en el servidor:<br /><br /> <br /><br /> Si la autenticación se realiza correctamente, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> cierra el flujo TCP existente y abre un flujo TCP firmado para controlar todas las solicitudes. Para autenticar cada solicitud de datos o metadatos se utiliza el contexto de seguridad empleado para abrir la conexión. Además, cada paquete se firma digitalmente para asegurarse de que la carga del paquete TCP no se ha cambiado en modo alguno.<br /><br /> <br /><br /> Si la autenticación no se realiza correctamente, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se desconecta del origen de datos multidimensionales y se produce una excepción.|  
|**Privacidad Pkt** o **PktPrivacy**|Sí|Especifica una conexión cifrada.<br /><br /> <br /><br /> Tenga en cuenta que también puede especificar una conexión cifrada si no establece la **ProtectionLevel** propiedad en la cadena de conexión.<br /><br /> <br /><br /> Se solicita un flujo TCP del proveedor y, a continuación, se autentica en el servidor el contexto de seguridad del usuario que solicita el flujo:<br /><br /> <br /><br /> Si la autenticación se realiza correctamente, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> cierra el flujo TCP existente y abre un flujo TCP cifrado para controlar todas las solicitudes. Para autenticar cada solicitud de datos o metadatos se utiliza el contexto de seguridad empleado para abrir la conexión. Además, la carga de cada paquete TCP se cifra mediante el método de cifrado de mayor nivel admitido por el proveedor y el origen de datos multidimensionales.<br /><br /> <br /><br /> Si la autenticación no se realiza correctamente, el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se desconecta del origen de datos multidimensionales y se produce una excepción.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>Utilizar la seguridad integrada de Windows para la conexión  
 La seguridad integrada de Windows es la forma más segura de establecer y proteger una conexión con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La seguridad integrada de Windows no revela credenciales de seguridad (como el nombre de usuario o la contraseña) durante el proceso de autenticación, sino que utiliza el identificador de seguridad del proceso que se ejecuta actualmente para establecer la identidad. Para la mayoría de las aplicaciones cliente, este identificador de seguridad representa la identidad del usuario actualmente conectado.  
  
 Para utilizar la seguridad integrada de Windows, la cadena de conexión requiere la siguiente configuración:  
  
-   Para el **Integrated Security** propiedad, no establezca esta propiedad o establecer esta propiedad hacer **SSPI**.  
  
    > [!NOTE]  
    >  Seguridad integrada de Windows sólo está disponible para las conexiones TCP porque las conexiones HTTP deben utilizar el **básica** para el **la seguridad integrada de** propiedad.  
  
-   Para el **ProtectionLevel** propiedad, establezca esta propiedad en **conectar**, **Pkt integridad**, o **Privacidad Pkt**.  
  
## <a name="securing-http-connections"></a>Proteger las conexiones HTTP  
 HTTPS y SSL (Capa de sockets seguros) se pueden utilizar para proteger las comunicaciones HTTP con un origen de datos analíticos externamente.  
  
 Dado que un proveedor XMLA solamente utiliza HTTP seguro, una conexión HTTP en ADOMD.NET debe ser una conexión firmada, como se muestra en la tabla siguiente.  
  
|Valor de ProtectionLevel|Usar con HTTP o HTTPS|  
|---------------------------|----------------------------|  
|**Ninguno**|No|  
|**Conectar**|HTTP|  
|**Integridad Pkt** o **PktIntegrity**|No|  
|**Privacidad Pkt** o **PktPrivacy**|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>Abrir una conexión HTTP segura  
 En el ejemplo siguiente se muestra cómo utilizar ADOMD.NET para abrir una conexión HTTP para el **AdventureWorksAS** ejemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos:  
  
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
 [Para establecer conexiones en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  

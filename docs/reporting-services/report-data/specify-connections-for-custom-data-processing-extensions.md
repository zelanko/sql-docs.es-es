---
title: Especificar conexiones para extensiones de procesamiento de datos personalizadas | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fc98f8394e637ea9a627cffd8e40887484462df5
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="specify-connections-for-custom-data-processing-extensions"></a>Especificar conexiones para extensiones de procesamiento de datos personalizadas
  Puede crear o usar extensiones de procesamiento de datos personalizadas de otros fabricantes en un servidor de informes con el fin de mejorar la capacidad de procesamiento de datos de orígenes de datos admitidos o proporcionar compatibilidad con orígenes de datos adicionales que no estén disponibles en una instalación predeterminada de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las conexiones se tratan de forma diferente en función de la implementación. Las implementaciones siguientes están disponibles para extensiones de procesamiento de datos:  
  
-   Proveedores de datos personalizados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (si tiene acceso a datos de orígenes de datos DB2.NET, Oracle, ODP.NET o Teradata, puede que use un proveedor de datos .NET personalizado)  
  
-   Extensiones de procesamiento de datos personalizadas compatibles con <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>  
  
-   Extensiones de procesamiento de datos personalizadas compatibles con <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>  
  
> [!NOTE]  
>  Consulte a su proveedor cómo se implementa la extensión de procesamiento de datos personalizada.  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a>Suplantación y extensiones de procesamiento de datos personalizadas  
 Si la extensión de procesamiento de datos personalizado se conecta a orígenes de datos con la suplantación, debe utilizar el método Open en cualquier el <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> o <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> interfaces para realizar la solicitud. Como alternativa, puede almacenar el objeto de identidad de usuario (System.Security.Principal.WindowsIdentity) y, después, reutilizarlo en el resto de las API de extensión de procesamiento de datos.  
  
 En versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], se llamaba a todas las extensiones de procesamiento de datos personalizadas mediante la suplantación de usuarios. En esta versión, la suplantación de usuarios solo se usa para llamar al método Open. Si tiene una extensión de procesamiento de datos que necesite seguridad integrada, es necesario que modifique el código para que use el método Open o que almacene el objeto de identidad de usuario.  
  
## <a name="connections-for-custom-net-framework-data-providers"></a>Conexiones para proveedores de datos personalizados de .NET Framework  
 Al configurar un informe para que utilice un origen de datos concreto, se establecen propiedades que determinan el tipo de origen de datos, la cadena de conexión y las credenciales que se utilizarán para tener acceso al origen de datos. La tabla siguiente describe los tipos de credenciales compatibles con proveedores de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Para más información sobre cómo configurar propiedades de orígenes de datos de informe, vea [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
|Credenciales|Conexiones|  
|-----------------|-----------------|  
|Seguridad integrada|Si su proveedor de datos lo admite, puede utilizar la seguridad integrada de Windows. La solicitud se envía utilizando las credenciales del usuario actual.<br /><br /> Al definir la cadena de conexión, asegúrese de usar argumentos que especifiquen la seguridad integrada (por ejemplo, en una conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluirse **Integrated Security=SSPI** en la cadena de conexión).|  
|Autenticación de Windows|Si su proveedor de datos lo admite, puede utilizar una cuenta de usuario de dominio de Windows. El servidor de informes suplantará la cuenta de usuario antes de que se llame a la extensión de procesamiento de datos.<br /><br /> Al definir la cadena de conexión, asegúrese de usar argumentos que especifiquen la seguridad integrada (por ejemplo, en una conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluirse **Integrated Security=SSPI** en la cadena de conexión).|  
|Credenciales de base de datos|La autenticación de base de datos no admite conexiones realizadas a través de un proveedor de datos personalizado de .NET. El servidor de informes generará un error de conexión en todos los casos.|  
|Sin credenciales|Puede utilizar la opción Sin credenciales con proveedores de datos personalizados de .NET. Si especifica una cuenta de ejecución desatendida, la cadena de conexión determinará las credenciales que se utilizarán. El servidor de informes suplantará la cuenta de ejecución desatendida para realizar la conexión.<br /><br /> Si no se ha definido la cuenta de ejecución desatendida, el servidor de informes generará un error de conexión. Para más información sobre cómo definir la cuenta, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).|  
  
## <a name="connections-for-idbconnection"></a>Conexiones para IDbConnection  
 Si está utilizando una extensión de procesamiento de datos personalizadas que sólo admite <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>, debe especificar la conexión de la manera siguiente:  
  
1.  Configurar la cuenta de ejecución desatendida La configuración de esta cuenta es necesaria para las conexiones realizadas mediante **IDbConnection**. El servidor de informes suplantará la cuenta al realizar la conexión.  
  
2.  Configure las propiedades de orígenes de datos del informe para utilizar **Sin credenciales**.  
  
3.  Incluya las credenciales utilizadas para conectarse al origen de datos en la cadena de conexión.  
  
 Al usar **IDbConnection**, no se admiten los tipos de credencial siguientes: la seguridad integrada, las cuentas de usuario de Windows y las credenciales de la base de datos. Si alguna conexión del origen de datos utiliza estas opciones, generará error en el servidor de informes.  
  
## <a name="connections-for-idbconnectionextension"></a>Conexiones para IDbConnectionExtension  
 Si utilizas una admite, extensión de procesamiento de datos personalizada <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>, puede especificar la conexión de las maneras siguientes:  
  
|Credenciales|Conexiones|  
|-----------------|-----------------|  
|Seguridad integrada|Si su proveedor de datos lo admite, puede utilizar la seguridad integrada de Windows con extensiones de procesamiento de datos personalizadas que utilicen **IDbConnectionExtension**.<br /><br /> Al definir la cadena de conexión, asegúrese de usar argumentos que especifiquen la seguridad integrada (por ejemplo, en una conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluirse **Integrated Security=SSPI** en la cadena de conexión).|  
|Autenticación de Windows|Si su proveedor de datos lo admite, puede utilizar una cuenta de usuario de dominio de Windows para extensiones de procesamiento de datos personalizadas que utilicen **IDbConnectionExtension**.<br /><br /> El servidor de informes suplantará la cuenta de usuario antes de que se llame a la extensión de procesamiento de datos. Al definir la cadena de conexión, asegúrese de usar argumentos que especifiquen la seguridad integrada (por ejemplo, en una conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluirse **Integrated Security=SSPI** en la cadena de conexión).|  
|Credenciales de base de datos|Puede utilizar la autenticación de base de datos para configurar conexiones para extensiones de procesamiento de datos personalizadas que utilicen **IDbConnectionExtension**.|  
|Sin credenciales|Si especifica una cuenta de ejecución desatendida, la cadena de conexión determinará las credenciales que se utilizarán.<br /><br /> Si no se ha definido la cuenta de ejecución desatendida, el servidor de informes generará un error de conexión.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Implementar una extensión de procesamiento de datos](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Configurar propiedades de origen de datos para un informe &#40;Administrador de informes&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  

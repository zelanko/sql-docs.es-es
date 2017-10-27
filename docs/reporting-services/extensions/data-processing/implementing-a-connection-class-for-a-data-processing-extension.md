---
title: "Implementar una clase de conexión para una extensión de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 19f059c0041cc9effc48e0db9c4b5ef1a504d020
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>Implementar una clase Connection para una extensión de procesamiento de datos
  El **conexión** objeto representa una conexión de base de datos u otro recurso similar y es el punto de partida para los usuarios de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de procesamiento de datos. Representa las conexiones a servidores de base de datos, aunque cualquier entidad con un comportamiento similar puede exponerse como un **conexión**.  
  
 Para implementar un **conexión** , cree una clase que implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> y, opcionalmente, implementa <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>.  
  
 En la implementación debe asegurarse de que se crea y se abre una conexión para que se puedan ejecutar los comandos. Asegúrese de que la implementación requiere que los clientes abran y cierren las conexiones explícitamente, en lugar de hacer que abra y cierre las conexiones para el cliente de forma implícita. Realice comprobaciones de seguridad cuando se obtenga la conexión. Al requerir una conexión existente para las otras clases en la extensión de procesamiento de datos de [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], se asegurará de que las comprobaciones de seguridad se realicen siempre al trabajar con el origen de datos.  
  
 Las propiedades de la conexión deseada se representan como una cadena de conexión. Se recomienda encarecidamente que las extensiones de procesamiento de datos de [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] admitan la propiedad <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> mediante el conocido sistema de par de nombre y valor definido por OLE DB.  
  
> [!NOTE]  
>  **Conexión** objetos suelen ser gran cantidad de recursos para obtener, por lo que puede tener en cuenta la agrupación de conexiones u otras técnicas para mitigar este riesgo.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> hereda de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Debe implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.IExtension> como parte de la implementación de la clase de conexión. La interfaz <xref:Microsoft.ReportingServices.Interfaces.IExtension> permite a una clase implementar un nombre de extensión localizado y procesar la información de configuración específica de la extensión que se almacena en el archivo de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Su **conexión** objeto contiene la <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> propiedad a través de su implementación de <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Se recomienda encarecidamente que las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admitan la propiedad <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A>, de forma que los usuarios encuentren un nombre traducido y conocido para la extensión en una interfaz de usuario, como el Administrador de informes.  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension>También permite la **conexión** objeto para recuperar y procesar los datos de configuración personalizados almacenados en el archivo RSReportServer.config. Para obtener más información acerca de cómo procesar los datos de configuración personalizados, vea el método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 La clase que implementa <xref:Microsoft.ReportingServices.Interfaces.IExtension> no se descarga de la memoria cuando se descarga el resto de las clases de extensión de procesamiento de datos. Por este motivo, puede usar el **extensión** clase para almacenar información de estado de la conexión cruzada o para almacenar los datos que pueden almacenarse en caché en memoria. Su **extensión** clase permanece en memoria mientras se esté ejecutando el servidor de informes.  
  
 Puede ampliar su **conexión** clase para incluir compatibilidad con las credenciales en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] implementando <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>. Cuando se implementa el <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>, <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>, y <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> propiedades de la <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> interfaz, se habilita la **Integrated Security** casilla de verificación y **nombre de usuario** y **contraseña** cuadros de texto de la **origen de datos** cuadro de diálogo en el Diseñador de informes. Esto permite al Diseñador de informes almacenar y recuperar las credenciales de los orígenes de datos que admitan la autenticación. Las credenciales se almacenan seguras y se utilizan al representar los informes en el modo de vista previa.  
  
> [!NOTE]  
>  Implementar de forma implícita <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> le exige que implemente los miembros de las interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> y <xref:Microsoft.ReportingServices.Interfaces.IExtension>.  
>   
>  Para obtener un ejemplo **conexión** implementación de la clase, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  


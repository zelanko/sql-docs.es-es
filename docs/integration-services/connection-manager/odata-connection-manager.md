---
title: Administrador de conexiones OData | Documentos de Microsoft
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>Administrador de conexiones OData
 Conectarse a un origen de datos de OData con un administrador de conexiones OData. Un componente de origen OData usa un administrador de conexiones OData para conectarse a un origen de datos de OData y consumir datos desde el servicio. Para obtener más información, vea [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Agregar un administrador de conexiones ODATA a un paquete SSIS  
 Puede agregar un nuevo administrador de conexiones OData a un paquete SSIS de tres maneras:  
  
-   Haga clic en el botón **Nuevo...** en el **Editor de origen OData**  
  
-   Haga clic con el botón derecho en la carpeta **Administradores de conexiones** en el **Explorador de soluciones**y, después, haga clic en **Nuevo administrador de conexiones**. Seleccione **ODATA** en **Tipo de administrador de conexión**.  
  
-   Pulse el botón derecho en el **administradores de conexión** panel en la parte inferior del paquete y, a continuación, seleccione **nueva conexión**. Seleccione **ODATA** en **Tipo de administrador de conexión**.  
  
## <a name="connection-manager-authentication"></a>Autenticación del administrador de conexiones  
 El Administrador de conexiones OData admite cinco modos de autenticación.  
  
-   Autenticación de Windows  
  
-   Autenticación básica (con el nombre de usuario y contraseña)  

-   Microsoft Dynamics AX Online (con nombre de usuario y contraseña)
  
-   Microsoft Dynamics CRM Online (con nombre de usuario y contraseña)
  
-   Microsoft Online Services (con nombre de usuario y contraseña)  
  
Para el acceso anónimo, seleccione la opción Autenticación de Windows.  

Para conectar a Microsoft Dynamics AX Online o Microsoft Dynamics CRM online, no se puede utilizar el **Microsoft Online Services** opción de autenticación. No se puede utilizar cualquier opción que está configurada para la autenticación multifactor.
  
### <a name="specifying-and-securing-credentials"></a>Especificar y proteger las credenciales  
 Si el servicio OData requiere autenticación básica, puede especificar un nombre de usuario y una contraseña en el [Editor del administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager-editor.md). Los valores que especifica en el editor se conservan en el paquete. El valor de contraseña se cifra según el nivel de protección del paquete.  
  
 Hay varias maneras de parametrizar los valores de nombre de usuario y contraseña o almacenarlos fuera del paquete. Por ejemplo, puede utilizar parámetros, o establecer propiedades del Administrador de la conexión directamente al ejecutar el paquete de SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Propiedades del administrador de conexiones OData  
 En la lista siguiente se describe las propiedades del Administrador de conexiones OData.  
  
|||  
|-|-|  
|Propiedad|Description|  
|Url|Dirección URL al documento de servicio.|  
|UserName|Nombre de usuario que se utilizará para la autenticación, si es necesario.|  
|Contraseña|Contraseña que se utilizará para la autenticación, si es necesario.|  
|ConnectionString|Incluye otras propiedades del Administrador de conexiones.|  
  
## <a name="odata-connection-manager-editor"></a>Editor del administrador de conexiones OData
  Use la **OData Connection Manager Editor** cuadro de diálogo para agregar una conexión o editar una conexión existente a un origen de datos de OData.  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Nombre del administrador de conexiones.  
  
 **Ubicación de documento de servicio**  
 Dirección URL del servicio OData. Por ejemplo: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticación**  
Seleccione una de las siguientes opciones:
-   **Autenticación de Windows**. Para el acceso anónimo, seleccione esta opción.
-   **Autenticación básica** 
-   **En línea de Microsoft Dynamics AX** de Dynamics AX en línea
-   **Microsoft Dynamics CRM Online** de Dynamics CRM Online
-   **Servicios en línea de Microsoft** de Microsoft Online Services

Si selecciona una opción distinta de la autenticación de Windows, escriba la **nombre de usuario** y **contraseña**. 

Para conectar a Microsoft Dynamics AX Online o Microsoft Dynamics CRM online, no se puede utilizar el **Microsoft Online Services** opción de autenticación. No se puede utilizar cualquier opción que está configurada para la autenticación multifactor.

 **Probar conexión**  
 Haga clic en este botón para probar la conexión con el origen OData.  


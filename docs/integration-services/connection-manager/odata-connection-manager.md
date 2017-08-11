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
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: b23a158bff546fd6ffb4208638c039d690379ce1
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="odata-connection-manager"></a>Administrador de conexiones OData
  Use un administrador de conexiones OData permite para conectarse a un origen OData. Un componente de origen OData se conecta a un origen OData mediante un administrador de conexiones OData y usa datos del servicio. Para obtener más información, vea [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Agregar un administrador de conexiones ODATA a un paquete SSIS  
 Hay tres formas de agregar un nuevo administrador de conexiones OData a un paquete SSIS:  
  
-   Haga clic en el botón **Nuevo...** en el **Editor de origen OData**  
  
-   Haga clic con el botón derecho en la carpeta **Administradores de conexiones** en el **Explorador de soluciones**y, después, haga clic en **Nuevo administrador de conexiones**. Seleccione **ODATA** en **Tipo de administrador de conexión**.  
  
-   Haga clic con el botón derecho en el panel **Administradores de conexiones** en la parte inferior del diseñador de paquetes y seleccione **Nueva conexión...**. Seleccione **ODATA** en **Tipo de administrador de conexión**.  
  
## <a name="connection-manager-authentication"></a>Autenticación del administrador de conexiones  
 El administrador de conexiones OData admite cinco modos de autenticación.  
  
-   Autenticación de Windows  
  
-   Autenticación básica (con el nombre de usuario y contraseña)  

-   Microsoft Dynamics AX Online (con nombre de usuario y contraseña)
  
-   Microsoft Dynamics CRM Online (con nombre de usuario y contraseña)
  
-   Microsoft Online Services (con nombre de usuario y contraseña)  
  
 Para el acceso anónimo, seleccione la opción Autenticación de Windows.  
  
### <a name="specifying-and-securing-credentials"></a>Especificar y proteger las credenciales  
 Si el servicio OData requiere autenticación básica, puede especificar un nombre de usuario y una contraseña en el [Editor del administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager-editor.md). Los valores que especifica en el editor se conservan en el paquete. El valor de contraseña se cifra según el nivel de protección del paquete.  
  
 Hay varias maneras de parametrizar los valores de nombre de usuario y contraseña o almacenarlos fuera del paquete. Por ejemplo, puede hacerlo mediante parámetros o estableciendo las propiedades del administrador de conexiones directamente al ejecutar el paquete con SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Propiedades del administrador de conexiones OData  
 En la lista siguiente se describen algunas de las propiedades del administrador de conexiones OData.  
  
|||  
|-|-|  
|Propiedad|Description|  
|Url|Dirección URL al documento de servicio.|  
|UserName|Nombre de usuario que se va a usar para la autenticación básica.|  
|Contraseña|Contraseña que se va a usar para la autenticación básica.|  
|ConnectionString|Refleja otras propiedades del administrador de conexiones.|  
  
## <a name="odata-connection-manager-editor"></a>Editor del administrador de conexiones OData
  Use el cuadro de diálogo **Editor del administrador de conexiones OData** para agregar una conexión o editar una conexión existente con un origen OData.  
  
### <a name="options"></a>Opciones  
 **Nombre del administrador de conexiones**  
 Nombre del administrador de conexiones.  
  
 **Ubicación de documento de servicio**  
 Dirección URL del servicio OData. Por ejemplo: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticación**  
 Seleccione **Autenticación de Windows** o use **este nombre de usuario y contraseña** para **Autenticación básica**. Si selecciona la segunda opción, escriba el **nombre de usuario** y la **contraseña**. 
 
 Ahora hay tres opciones más. Seleccione **Microsoft Dynamics AX Online** para Dynamics AX Online, seleccione **Microsoft Dynamics CRM Online** para Dynamics CRM Online y seleccione **Microsoft Online Services** para Microsoft Online Services. Si selecciona una de estas tres opciones, escriba el **nombre de usuario** y la **contraseña**.
  
 **Probar conexión**  
 Haga clic en este botón para probar la conexión con el origen OData.  
  
## <a name="see-also"></a>Vea también  
 [Editor del administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  

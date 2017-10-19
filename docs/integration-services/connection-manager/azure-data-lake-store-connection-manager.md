---
title: "Administrador de conexiones de almacén de Azure Data Lake | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 0a84b10114d785c9216a0902b2eefbcb0bd3f4c8
ms.contentlocale: es-es
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Administrador de conexiones de Azure Data Lake Store
Un paquete de SQL Server Integration Services (SSIS) puede utilizar el Administrador de conexiones de almacén de Azure Data Lake para conectarse a un servicio de almacén de Azure Data Lake con uno de los dos tipos de autenticación siguientes:
-   Identidad de usuario de Azure AD
-   Identidad de servicio de Azure AD 

El Administrador de conexiones de almacén de Azure Data Lake es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Para garantizar que el Administrador de conexiones de Azure Data Lake Store y los componentes que lo utilizan (es decir, Origen de Data Lake Store y Destino de Azure Data Lake Store) se puedan conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar el administrador de conexiones de Azure Data Lake Store

1.  En el **Agregar administrador de conexiones SSIS** cuadro de diálogo, seleccione **AzureDataLake**y, a continuación, seleccione **agregar**. El **Azure datos Lake almacén Connection Manager Editor** abre el cuadro de diálogo.
  
2.  En el **Azure datos Lake almacén Connection Manager Editor** cuadro de diálogo, en la **ADLS Host** campo, escriba la URL del host de almacén de Azure Data Lake. Por ejemplo: `https://test.azuredatalakestore.net` o `test.azuredatalakestore.net`.
  
3.  En el **autenticación** , a continuación, elija el tipo de autenticación adecuado para tener acceso a los datos de almacén de Azure Data Lake.

    1.  Si selecciona el **identidad de usuario de Azure AD** autenticación opción, haga lo siguiente:
        1. Proporcione los valores de la **nombre de usuario** y **contraseña** campos. 
    
        2. Para probar la conexión, seleccione **Probar conexión**. Si usted o el Administrador de inquilinos anteriormente no consentir y permitir que SSIS acceder a los datos de almacén de Data Lake de Azure, seleccione **Accept** cuando se le solicite. Para obtener más información sobre esta experiencia del consentimiento, consulte [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Cuando se selecciona el **identidad de usuario de Azure AD** no se admiten la opción de autenticación, la autenticación multifactor y autenticación de cuentas de Microsoft.
    
    2. Si selecciona el **identidad de servicio de Azure AD** autenticación opción, haga lo siguiente:
        1. Crear una aplicación de Azure Active Directory (AAD) y el servicio principal para tener acceso a los datos de Azure Data Lake.
    
        2. Asigne los permisos adecuados para permitir que esta aplicación AAD acceder a los recursos de Azure Data Lake. Para obtener más información sobre esta opción de autenticación, consulte [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(Utilizar el portal para crear una aplicación de Active Directory y una entidad de servicio que puedan tener acceso a los recursos).
    
        3. Proporcione los valores de la **Id. de cliente**, **clave secreta**, y **nombre del inquilino** campos.
    
        4. Para probar la conexión, seleccione **Probar conexión**.  
  
6.  Seleccione **Aceptar** para cerrar el **Azure datos Lake almacén Connection Manager Editor** cuadro de diálogo.  

## <a name="view-the-properties-of-the-connection-manager"></a>Ver las propiedades del Administrador de conexiones
Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

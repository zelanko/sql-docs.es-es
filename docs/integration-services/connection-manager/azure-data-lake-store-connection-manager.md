---
title: "Administrador de conexiones de almacén de Azure Data Lake | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 39630087acdb2ade2e77d4364e4467f8d740d8d4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Administrador de conexiones de Azure Data Lake Store
  El **administrador de conexiones de Azure Data Lake Store** habilita un paquete SSIS para conectarse a un servicio de Azure Data Lake Store mediante dos tipos de autenticación: la identidad de usuario de Azure AD y la identidad de servicio de Azure AD.  
  
 El **Administrador de conexiones de almacén de Azure Data Lake** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Para garantizar que el Administrador de conexiones de Azure Data Lake Store y los componentes que lo utilizan (es decir, Origen de Data Lake Store y Destino de Azure Data Lake Store) se puedan conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar el administrador de conexiones de Azure Data Lake Store

 
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureDataLake**y haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo Editor de administrador de conexiones de AzureDataLake, escriba la dirección URL de Azure Data Lake Store en el campo **Host ADLS** . Por ejemplo: `https://test.azuredatalakestore.net` o `test.azuredatalakestore.net`.
  
3.  Elija el tipo de autenticación correspondiente para tener acceso a datos de Azure Data Lake Store.

    1.  Si ha seleccionado la opción de autenticación **Identidad de usuario de Azure AD** , realice lo siguiente:
        1. Especifique los valores para los campos **Nombre de usuario** y **Contraseña** . 
    
        2. Haga clic en el botón **Probar conexión** para probar la conexión. Si usted y el administrador de inquilinos no otorgan antes su consentimiento a SSIS para tener acceso a los datos de Azure Data Lake Store, deberá hacer clic en el botón **Aceptar** para permitir que SSIS tenga acceso a los datos de Azure Data Lake Store en el cuadro de diálogo emergente. Para obtener más información sobre esta experiencia del consentimiento, consulte [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Para la opción de autenticación Identidad de usuario de Azure AD, NO se admiten cuentas de Microsoft ni Multi-Factor Authentication.
    
    2. Si ha seleccionado la opción de autenticación **Identidad de servicio de Azure AD** , realice lo siguiente:
        1. Cree una aplicación de AAD y la entidad de servicio que pueden tener acceso a recursos de Azure Data Lake.
    
        2. Asigne a esta aplicación de AAD los permisos correspondientes para tener acceso a los recursos de Azure Data Lake. Para obtener más información sobre esta opción de autenticación, consulte [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(Utilizar el portal para crear una aplicación de Active Directory y una entidad de servicio que puedan tener acceso a los recursos).
    
        3. Especifique los valores para los campos **Id. de cliente**, **Clave secreta** y **Nombre de inquilino** .
    
        4. Haga clic en el botón **Probar conexión** para probar la conexión.  
  
6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
    Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

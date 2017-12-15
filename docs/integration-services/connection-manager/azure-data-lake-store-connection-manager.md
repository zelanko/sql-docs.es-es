---
title: Administrador de conexiones de Azure Data Lake Store | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: "7"
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 556f0efa1ce15ee23acc190e547e3700e64eca4d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="azure-data-lake-store-connection-manager"></a>Administrador de conexiones de Azure Data Lake Store
Un paquete de SQL Server Integration Services (SSIS) puede usar el administrador de conexiones de Azure Data Lake Store para conectarse a un servicio de Azure Data Lake Store con uno de los dos tipos de autenticación siguientes:
-   Identidad de usuario de Azure AD
-   Identidad de servicio de Azure AD 

El administrador de conexiones de Azure Data Lake Store es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Para garantizar que el Administrador de conexiones de Azure Data Lake Store y los componentes que lo utilizan (es decir, Origen de Data Lake Store y Destino de Azure Data Lake Store) se puedan conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar el administrador de conexiones de Azure Data Lake Store

1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureDataLake** y, después, haga clic en **Agregar**. Se abrirá el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store).
  
2.  En el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store), en el campo **ADLS Host** (Host de ADLS), proporcione la URL del host de Azure Data Lake Store. Por ejemplo, `https://test.azuredatalakestore.net` o `test.azuredatalakestore.net`.
  
3.  En el campo **Autenticación**, elija el tipo de autenticación adecuado para tener acceso a los datos de Azure Data Lake Store.

    1.  Si seleccionó la opción de autenticación **Identidad de usuario de Azure AD**, realice lo siguiente:
        1. Proporcione los valores para los campos **Nombre de usuario** y **Contraseña**. 
    
        2. Seleccione **Probar conexión** para probar la conexión. Si usted o el administrador de inquilinos no permitió previamente que SSIS obtuviera acceso a los datos de Azure Data Lake Store, seleccione **Aceptar** cuando se le solicite. Para obtener más información sobre esta experiencia del consentimiento, consulte [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Al seleccionar la opción de autenticación **Identidad de usuario de Azure AD**, no se admitirá la autenticación multifactor ni la autenticación de la cuenta de Microsoft.
    
    2. Si seleccionó la opción de autenticación **Azure AD Service Identity** (Identidad de servicio de Azure AD), realice lo siguiente:
        1. Cree una entidad de servicio y una aplicación de Azure Active Directory (AAD) para tener acceso a los datos de Azure Data Lake.
    
        2. Asigne los permisos adecuados para permitir que esta aplicación de AAD tenga acceso a los recursos de Azure Data Lake. Para obtener más información sobre esta opción de autenticación, consulte [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (Utilizar el portal para crear una aplicación de Active Directory y una entidad de servicio que puedan tener acceso a los recursos).
    
        3. Proporcione los valores para los campos **Id. de cliente**, **Clave secreta** y **Nombre de inquilino**.
    
        4. Seleccione **Probar conexión** para probar la conexión.  
  
6.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store).  

## <a name="view-the-properties-of-the-connection-manager"></a>Ver las propiedades del administrador de conexiones
Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

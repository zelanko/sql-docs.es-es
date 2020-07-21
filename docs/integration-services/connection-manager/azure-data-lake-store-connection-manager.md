---
title: Administrador de conexiones de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: Lingxi-Li
ms.author: lingxl
ms.reviewer: maghan
ms.openlocfilehash: 985c582b6b04f03a77686d6ad3697a565100ead0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762706"
---
# <a name="azure-data-lake-store-connection-manager"></a>Administrador de conexiones de Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Un paquete de SQL Server Integration Services (SSIS) puede usar el Administrador de conexiones de Azure Data Lake Store para conectarse a una cuenta de Azure Data Lake Storage Gen1 con uno de los dos tipos de autenticación siguientes:
-   Identidad de usuario de Azure AD
-   Identidad de servicio de Azure AD 

El administrador de conexiones de Azure Data Lake Store es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

> [!NOTE]
> Para garantizar que el administrador de conexiones de Azure Data Lake Store y los componentes que lo usan (es decir, el origen y el destino de Data Lake Storage Gen1) se pueden conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar el administrador de conexiones de Azure Data Lake Store

1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **AzureDataLake** y, después, haga clic en **Agregar**. Se abrirá el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store).
  
2.  En el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store), en el campo **ADLS Host** (Host de ADLS), proporcione la dirección URL del host de Data Lake Storage Gen1. Por ejemplo, `https://test.azuredatalakestore.net` o `test.azuredatalakestore.net`.
  
3.  En el campo **Autenticación**, elija el tipo de autenticación adecuado para acceder a los datos de Data Lake Storage Gen1.

    1.  Si seleccionó la opción de autenticación **Identidad de usuario de Azure AD**, realice lo siguiente:
        1. Proporcione los valores para los campos **Nombre de usuario** y **Contraseña**. 
    
        2. Seleccione **Probar conexión** para probar la conexión. Si usted o el administrador de inquilinos no ha permitido previamente que SSIS accediera a los datos de Data Lake Storage Gen1, seleccione **Aceptar** cuando se le solicite. Para obtener más información sobre esta experiencia del consentimiento, consulte [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad).
    
        > [!NOTE] 
        > Al seleccionar la opción de autenticación **Identidad de usuario de Azure AD**, no se admitirá la autenticación multifactor ni la autenticación de la cuenta de Microsoft.
    
    2. Si seleccionó la opción de autenticación **Azure AD Service Identity** (Identidad de servicio de Azure AD), realice lo siguiente:
        1. Cree una entidad de servicio y una aplicación de Azure Active Directory (AAD) para acceder a los datos de Data Lake Storage Gen1.
    
        2. Asigne los permisos adecuados para permitir que esta aplicación de AAD acceda a los recursos de Data Lake Storage Gen1. Para obtener más información sobre esta opción de autenticación, consulte [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(Utilizar el portal para crear una aplicación de Active Directory y una entidad de servicio que puedan tener acceso a los recursos).
    
        3. Proporcione los valores para los campos **Id. de cliente**, **Clave secreta** y **Nombre de inquilino**.
    
        4. Seleccione **Probar conexión** para probar la conexión.  
  
6.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Azure Data Lake Store Connection Manager Editor** (Editor del administrador de conexiones de Azure Data Lake Store).  

## <a name="view-the-properties-of-the-connection-manager"></a>Ver las propiedades del administrador de conexiones
Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

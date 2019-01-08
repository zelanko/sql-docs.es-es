---
title: Administrador de conexiones de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSCM.F1
- SQL11.DTS.DESIGNER.AFPADLSCM.F1
ms.assetid: 7f1323f9-9dc3-4378-9c70-bbc65bfeabfd
author: yualan
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a462b44137c59f92a4bb9dc38a13318d71a32043
ms.sourcegitcommit: 85fd3e1751de97a16399575397ab72ebd977c8e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/17/2018
ms.locfileid: "53531040"
---
# <a name="azure-data-lake-store-connection-manager"></a>Administrador de conexiones de Azure Data Lake Store
  El **Administrador de conexiones de Azure Data Lake Store** habilita un paquete SSIS para conectarse a un servicio de Azure Data Lake Store mediante dos tipos de autenticación: Identidad de usuario de Azure AD y la identidad de servicio de Azure AD.  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar el administrador de conexiones de Azure Data Lake Store 
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureDataLake**y haga clic en **Agregar**.   
  
2.  En el cuadro de diálogo Editor de administrador de conexiones de AzureDataLake, escriba la dirección URL de Azure Data Lake Store en el campo **Host ADLS** . Por ejemplo: https://test.azuredatalakestore.net o test.azuredatalakestore.net.
  
3.  Elija el tipo de autenticación correspondiente para tener acceso a datos de Azure Data Lake Store.

    1.  Si ha seleccionado la opción de autenticación **Identidad de usuario de Azure AD** , realice lo siguiente:

        1. Especifique los valores para los campos **Nombre de usuario** y **Contraseña** . 
    
        2. Haga clic en el botón **Probar conexión** para probar la conexión. Si usted y el administrador de inquilinos no otorgan antes su consentimiento a SSIS para tener acceso a los datos de Azure Data Lake Store, deberá hacer clic en el botón **Aceptar** para permitir que SSIS tenga acceso a los datos de Azure Data Lake Store en el cuadro de diálogo emergente. Para obtener más información sobre esta experiencia del consentimiento, consulte [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        > [!NOTE] 
        > Para la opción de autenticación Identidad de usuario de Azure AD, NO se admiten cuentas de Microsoft ni Multi-Factor Authentication.
    
    2.  Si ha seleccionado la opción de autenticación **Identidad de servicio de Azure AD** , realice lo siguiente:
        1. Cree una aplicación de AAD y la entidad de servicio que pueden tener acceso a recursos de Azure Data Lake.
    
        2. Asigne a esta aplicación de AAD los permisos correspondientes para tener acceso a los recursos de Azure Data Lake. Para obtener más información sobre esta opción de autenticación, consulte [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (Utilizar el portal para crear una aplicación de Active Directory y una entidad de servicio que puedan tener acceso a los recursos).
    
        3. Especifique los valores para los campos **Id. de cliente**, **Clave secreta** y **Nombre de inquilino** .
    
        4. Haga clic en el botón **Probar conexión** para probar la conexión.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
    Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

---
title: Administrador de conexiones de Azure Storage | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f171499471f8f94ad970446d31cf796f4ab55fb7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028768"
---
# <a name="azure-storage-connection-manager"></a>Administrador de conexiones de Almacenamiento de Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  El **Administrador de conexiones de Azure Storage** permite que un paquete SSIS se conecte a una cuenta de Azure Storage.
   
 El **Administrador de conexiones de Azure Storage** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureStorage**y haga clic en **Agregar**.  
  
Están disponibles las propiedades siguientes.

- **Servicio:** especifica el servicio de almacenamiento al que conectarse.
- **Nombre de cuenta:** especifica el nombre de la cuenta de almacenamiento.
- **Autenticación:** especifica el método de autenticación que se va a utilizar. Se admite la autenticación **AccessKey** y **ServicePrincipal**.
    - **AccessKey:** con este método de autenticación, especifique el valor de **Clave de cuenta**.
    - **ServicePrincipal:** con este método de autenticación, especifique los valores de **Id. de la aplicación**, **Clave de aplicación** e **Id. de inquilino** de la entidad de servicio.
      Para que la **conexión de prueba** funcione, se debe asignar al menos el rol **Lector de datos de Storage Blob** a la entidad de servicio en la cuenta de almacenamiento.
      Consulte [esta](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) página para obtener más información.
- **Entorno:** especifica el entorno de nube que hospeda la cuenta de almacenamiento.

## <a name="managed-identities-for-azure-resources-authentication"></a>Identidades administradas para la autenticación de los recursos de Azure
Al ejecutar paquetes SSIS en el [entorno de ejecución de integración de Azure-SSIS en Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), puede usar la [identidad administrada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) asociada a su factoría de datos para la autenticación de Azure Storage. Puede acceder a la factoría designada y copiar datos desde la cuenta de almacenamiento o en la cuenta de almacenamiento con esta identidad.

Consulte [Autenticación del acceso a Azure Storage mediante Azure Active Directory](https://docs.microsoft.com/azure/storage/common/storage-auth-aad) para la autenticación de Azure Storage en general. Para usar la autenticación de la identidad administrada en Azure Storage, siga estos pasos para configurar la cuenta de almacenamiento:

1. **[Busque la identidad administrada de la factoría de datos en Azure Portal](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Vaya a **Propiedades** en la factoría de datos. Copie el **Id. de la aplicación de identidad administrada** (NO el **Id. del objeto de identidad administrada**).

1. **Conceda a la identidad administrada el permiso adecuado en la cuenta de almacenamiento**. Consulte [Administración de los derechos de acceso a los datos de Azure Storage con RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal) para ver más detalles sobre los roles.

    - **Como origen**, en Control de acceso (IAM), conceda al menos el rol **Lector de datos de Storage Blob**.
    - **Como destino**, en Control de acceso (IAM), conceda al menos el rol **Colaborador de datos de Storage Blob**.

Luego, **configure la autenticación de la identidad administrada** para el administrador de conexiones de Azure Storage. Tiene dos opciones para hacerlo:

1. Configurarla durante su diseño. En el Diseñador SSIS, haga doble clic en el administrador de conexiones de Azure Storage para abrir el **Editor del Administrador de conexiones de Azure Storage** y active **Use managed identity to authenticate on Azure** (Usar identidad administrada para autenticarse en Azure).
    > [!NOTE]
    >  Actualmente, esta opción NO surte efecto (lo que indica que la autenticación de la identidad administrada no funciona) cuando ejecuta un paquete SSIS en el Diseñador SSIS o en [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.
    
1. Configurarla durante su ejecución. Al ejecutar el paquete a través de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) o de la [actividad de un paquete SSIS en Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), busque el administrador de conexiones de Azure Storage y actualice su propiedad **ConnectUsingManagedIdentity** en **True**.
    > [!NOTE]
    >  En el entorno de ejecución de integración de Azure-SSIS, todos los demás métodos de autenticación (por ejemplo, clave de acceso, entidad de servicio) configurados previamente en el administrador de conexiones de Azure Storage se **invalidarán** cuando la autenticación de la identidad administrada se usa para las operaciones de almacenamiento.

> [!NOTE]
>  Para configurar la autenticación de la identidad administrada en los paquetes existentes, la manera preferida es recompilar el proyecto de SSIS con el [Diseñador SSIS más reciente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) al menos una vez, e implemente de nuevo ese proyecto SSIS en su entorno de ejecución de integración de Azure-SSIS de modo que la nueva propiedad del administrador de conexiones **ConnectUsingManagedIdentity** se agregue automáticamente a todos los administradores de conexiones ADO.NET del proyecto de SSIS. La manera alternativa es usar directamente la invalidación de propiedad con la ruta de acceso a la propiedad **\Package.Connections[{el nombre del administrador de conexiones}].Properties[ConnectUsingManagedIdentity]** en tiempo de ejecución.

## <a name="see-also"></a>Consulte también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)

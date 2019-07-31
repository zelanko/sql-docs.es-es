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
ms.openlocfilehash: 8a115dafb386323bc1f4738720e7576657d22543
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316688"
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

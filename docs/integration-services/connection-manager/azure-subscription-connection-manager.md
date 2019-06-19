---
title: Administrador de conexiones de suscripciones de Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b3dec7a683bcebc28f9bfe90e4b4091a70892f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728342"
---
# <a name="azure-subscription-connection-manager"></a>Azure Subscription Connection Manager (Administrador de conexiones de suscripciones de Azure)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El **administrador de conexiones de suscripciones de Azure** permite que un paquete SSIS se conecte a una suscripción de Azure mediante los valores que especifique para las propiedades: Id. de suscripción de Azure y Certificado de administración.  
  
 El **Administrador de conexiones de suscripciones de Azure** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** que se muestra arriba, seleccione **Suscripción de Azure**y haga clic en **Agregar**.  Debería aparecer el cuadro de diálogo **Azure Subscription Connection Manager Editor** (Editor de administrador de conexiones de suscripciones de Azure).  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Escriba el id. de suscripción de Azure, que identifica una suscripción de Azure de manera única, para el **id. de suscripción de Azure**.  Se puede encontrar el valor en el [Portal de administración de Azure](https://manage.windowsazure.com) en la página **Configuración** :  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  Elija **Management certificate store location** (Ubicación de almacén de certificados de administración) y **Management certificate store name** (Nombre de almacén de certificados de administración) en las listas desplegables.  
  
4.  Escriba **Management certificate thumbprint** (Huella digital de certificado de administración) o haga clic en **Examinar…** para elegir un certificado en el almacén seleccionado. El certificado se debe cargar como un certificado de administración para la suscripción. Para hacerlo, haga clic en **Cargar** en la página siguiente del Portal de Azure (consulte esta [publicación de MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) para obtener más detalles).  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Haga clic en **Probar conexión** para probar la conexión.  
  
6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
  

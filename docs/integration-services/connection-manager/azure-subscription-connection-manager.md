---
title: "Administrador de conexiones de suscripción de Azure | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f34ac8d5c1b6bd117a83d287db1d46ff6f786aab
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-subscription-connection-manager"></a>Azure Subscription Connection Manager (Administrador de conexiones de suscripciones de Azure)
  El **administrador de conexiones de suscripciones de Azure** permite que un paquete de SSIS se conecte con una suscripción de Azure a través de los valores que especifica para las propiedades: identificador de suscripción de Azure y certificado de administración.  
  
 El **Administrador de conexiones de suscripción de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** que se muestra arriba, seleccione **Suscripción de Azure**y haga clic en **Agregar**.  Debería aparecer el cuadro de diálogo **Azure Subscription Connection Manager Editor** (Editor de administrador de conexiones de suscripciones de Azure).  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Escriba el id. de suscripción de Azure, que identifica una suscripción de Azure de manera única, para el **id. de suscripción de Azure**.  Se puede encontrar el valor en el [Portal de administración de Azure](https://manage.windowsazure.com) en la página **Configuración** :  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-Id. de suscripción")  
  
3.  Elija **Management certificate store location** (Ubicación de almacén de certificados de administración) y **Management certificate store name** (Nombre de almacén de certificados de administración) en las listas desplegables.  
  
4.  Escriba **Management certificate thumbprint** (Huella digital de certificado de administración) o haga clic en **Examinar…** para elegir un certificado en el almacén seleccionado. El certificado se debe cargar como un certificado de administración para la suscripción. Para hacerlo, haga clic en **Cargar** en la página siguiente del Portal de Azure (consulte esta [publicación de MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) para obtener más detalles).  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "ManagementCertificate de AzureSettings de SSIS")  
  
5.  Haga clic en **Probar conexión** para probar la conexión.  
  
6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
  


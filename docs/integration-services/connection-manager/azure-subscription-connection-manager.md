---
description: Azure Subscription Connection Manager (Administrador de conexiones de suscripciones de Azure)
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 277e92a906acb89960e16c941fbd71df023ddb23
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678994"
---
# <a name="azure-subscription-connection-manager"></a>Azure Subscription Connection Manager (Administrador de conexiones de suscripciones de Azure)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El **administrador de conexiones de suscripciones de Azure** permite que un paquete de SSIS se conecte con una suscripción de Azure a través de los valores que especifica para las propiedades: identificador de suscripción de Azure y certificado de administración.  
  
 El **Administrador de conexiones de suscripciones de Azure** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** que se muestra arriba, seleccione **Suscripción de Azure** y haga clic en **Agregar** .  Debería aparecer el cuadro de diálogo **Azure Subscription Connection Manager Editor** (Editor de administrador de conexiones de suscripciones de Azure).  
  
    ![Captura de pantalla en la que se muestra el cuadro de diálogo Azure Subscription Connection Manager Editor (Editor de administrador de conexiones de suscripciones de Azure).](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Escriba el id. de suscripción de Azure, que identifica una suscripción de Azure de manera única, para el **id. de suscripción de Azure** .  Se puede encontrar el valor en el [Portal de administración de Azure](https://manage.windowsazure.com) en la página **Configuración** :  
  
    ![Captura de pantalla del Portal de administración de Azure en la que se muestra la pestaña SUSCRIPCIONES de la página Configuración.](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  Elija **Management certificate store location** (Ubicación de almacén de certificados de administración) y **Management certificate store name** (Nombre de almacén de certificados de administración) en las listas desplegables.  
  
4.  Escriba **Management certificate thumbprint** (Huella digital de certificado de administración) o haga clic en **Examinar…** para elegir un certificado en el almacén seleccionado. El certificado se debe cargar como un certificado de administración para la suscripción. Para hacerlo, haga clic en **Cargar** en la página siguiente de Azure Portal (consulte esta [publicación de MSDN](/previous-versions/azure/gg551722(v=azure.100)) para obtener más detalles).  
  
     ![Captura de pantalla del Portal de administración de Azure en la que se muestra la pestaña CERTIFICADOS DE ADMINISTRACIÓN de la página Configuración.](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Haga clic en **Probar conexión** para probar la conexión.  
  
6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  

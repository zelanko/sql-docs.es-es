---
title: Administrador de conexiones de Azure Storage | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
manager: craigg
ms.openlocfilehash: a46945b7c7725d680fb303a451327dc2733642aa
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277834"
---
# <a name="azure-storage-connection-manager"></a>Administrador de conexiones de Almacenamiento de Azure
  El **administrador de conexiones de Azure Storage** permite que un paquete SSIS se conecte a una cuenta de Azure Storage mediante los valores especificados para las propiedades: Nombre de la cuenta de almacenamiento y Clave de la cuenta.  
   
 El **Administrador de conexiones de Azure Storage** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureStorage**y haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo Azure Storage Connection Manager Editor (Editor del administrador de conexiones de Almacenamiento de Azure), elija **Use Azure account** (Usar cuenta de Azure) para conectarse a un servicio de Almacenamiento de Azure a través de Internet o elija **Use local developer account** (Usar cuenta de desarrollador local) para conectarse al servicio local hospedado en el Emulador de almacenamiento de Azure.  
  
3.  Si ha seleccionado la opción **Use Azure account** (Usar cuenta de Azure), realice lo siguiente:  
  
    1.  Especifique los valores para los campos **Nombre de cuenta de almacenamiento** y **Clave de cuenta** . Estos valores se almacenarán como información confidencial en el paquete SSIS.  
  
    2.  Seleccione **Use HTTPS** (Usar HTTPS) si desea utilizar HTTPS en lugar de HTTP para conectarse con el servicio de Almacenamiento de Azure.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
5.  Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

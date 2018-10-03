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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 31440d6479353467d687467466f9c838a49d5252
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724153"
---
# <a name="azure-storage-connection-manager"></a>Administrador de conexiones de Almacenamiento de Azure
  El **Administrador de conexiones de Almacenamiento de Azure** habilita un paquete SSIS para conectarse a una cuenta de Almacenamiento de Azure utilizando los valores especificados para las propiedades nombre de cuenta y clave de cuenta de almacenamiento.  
   
 El **Administrador de conexiones de Azure Storage** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureStorage**y haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo Azure Storage Connection Manager Editor (Editor del administrador de conexiones de Almacenamiento de Azure), elija **Use Azure account** (Usar cuenta de Azure) para conectarse a un servicio de Almacenamiento de Azure a través de Internet o elija **Use local developer account** (Usar cuenta de desarrollador local) para conectarse al servicio local hospedado en el Emulador de almacenamiento de Azure.  
  
3.  Si ha seleccionado la opción **Use Azure account** (Usar cuenta de Azure), realice lo siguiente:  
  
    1.  Especifique los valores para los campos **Nombre de cuenta de almacenamiento** y **Clave de cuenta** . Estos valores se almacenarán como información confidencial en el paquete SSIS.  
  
    2.  Seleccione **Use HTTPS** (Usar HTTPS) si desea utilizar HTTPS en lugar de HTTP para conectarse con el servicio de Almacenamiento de Azure.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
5.  Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

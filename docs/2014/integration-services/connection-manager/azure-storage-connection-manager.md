---
title: Administrador de conexiones de Azure Storage | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c6b6c86aa3f76088ff3cb0e36a1a111b325944ea
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921096"
---
# <a name="azure-storage-connection-manager"></a>Administrador de conexiones de Almacenamiento de Azure
  El Administrador de conexiones de Azure Storage habilita un paquete SSIS para conectarse a una cuenta de Azure Storage utilizando los valores especificados para las propiedades nombre de cuenta y clave de cuenta de almacenamiento.  
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureStorage**y haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo Azure Storage Connection Manager Editor (Editor del administrador de conexiones de Almacenamiento de Azure), elija **Use Azure account** (Usar cuenta de Azure) para conectarse a un servicio de Almacenamiento de Azure a través de Internet o elija **Use local developer account** (Usar cuenta de desarrollador local) para conectarse al servicio local hospedado en el Emulador de almacenamiento de Azure.  
  
3.  Si ha seleccionado la opción **Use Azure account** (Usar cuenta de Azure), realice lo siguiente:  
  
    1.  Especifique los valores para los campos **Nombre de cuenta de almacenamiento** y **Clave de cuenta**. Estos valores se almacenarán como información confidencial en el paquete SSIS.  
  
    2.  Seleccione **Use HTTPS** (Usar HTTPS) si desea utilizar HTTPS en lugar de HTTP para conectarse con el servicio de Azure Storage.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
5.  Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  

---
title: Conexión con Microsoft Azure Storage (Restauración) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7be978540b673578fb9ca401f25dfab053f4f7e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854186"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Conectar con Azure Storage (Restauración)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo permite especificar la conexión a la información de la cuenta de Almacenamiento de Windows Azure para recuperar el almacenamiento de archivos de la cuenta de Almacenamiento de Windows Azure. Después de especificar la información necesaria, haga clic en **Conectar** para establecer la conexión al Almacenamiento de Windows Azure.  
  
## <a name="windows-azure-storage-account"></a>Cuenta de Almacenamiento de Windows Azure  
 **Cuenta de almacenamiento**  
 Seleccione, escriba o pegue el nombre de la cuenta de Almacenamiento de Windows Azure que desee utilizar. El cuadro desplegable muestra las cuentas utilizadas previamente.  
  
 **Clave de cuenta**  
 Especifique la tecla de acceso de la cuenta de Almacenamiento de Windows Azure.  
  
 Casilla**Usar puntos de conexión seguros (HTTPS)**   
 Seleccione esta opción para establecer una conexión segura con Almacenamiento de Windows Azure (recomendado).  
  
 Casilla**Guardar clave de cuenta**   
 Active esta casilla si desea que SQL Server recuerde la tecla de acceso para esta cuenta de almacenamiento.  
  
### <a name="sql-credential"></a>Credencial SQL  
 **Seleccionar una credencial existente**  
 Seleccione una credencial existente de SQL que coincida con la información de clave de cuenta y de cuenta de almacenamiento.  
  
 **Crear una nueva credencial**  
 Seleccione esta opción para crear una nueva credencial utilizando la información de clave de cuenta y de cuenta de almacenamiento. Especifique el nombre de la nueva credencial en el campo **Nombre de credencial** .  
  
  

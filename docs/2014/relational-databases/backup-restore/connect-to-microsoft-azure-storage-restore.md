---
title: Conectarse a Azure Storage (restauración) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fbb57fe629797e34cc7c61f224d65d46d4e66cd
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154774"
---
# <a name="connect-to-azure-storage-restore"></a>Conectarse a Azure Storage (restauración)
  El cuadro de diálogo permite especificar la conexión a la información de la cuenta de almacenamiento de Azure para recuperar el almacenamiento de archivos en la cuenta de almacenamiento de Azure. Después de especificar la información necesaria, haga clic en **conectar** para establecer la conexión al almacenamiento de Azure.  
  
## <a name="azure-storage-account"></a>Cuenta de Almacenamiento de Azure  
 **Cuenta de almacenamiento**  
 Seleccione, escriba o pegue el nombre de la cuenta de almacenamiento de Azure que desea usar. El cuadro desplegable muestra las cuentas utilizadas previamente.  
  
 **Clave de cuenta**  
 Especifique la clave de acceso de la cuenta de almacenamiento de Azure.  
  
 Casilla**Usar puntos de conexión seguros (HTTPS)**  
 Seleccione esta opción para establecer una conexión segura con el almacenamiento de Azure recomendado.  
  
 Casilla**Guardar clave de cuenta**  
 Active esta casilla si desea que SQL Server recuerde la tecla de acceso para esta cuenta de almacenamiento.  
  
### <a name="sql-credential"></a>Credencial SQL  
 **Seleccionar una credencial existente**  
 Seleccione una credencial existente de SQL que coincida con la información de clave de cuenta y de cuenta de almacenamiento.  
  
 **Crear una nueva credencial**  
 Seleccione esta opción para crear una nueva credencial utilizando la información de clave de cuenta y de cuenta de almacenamiento. Especifique el nombre de la nueva credencial en el campo **Nombre de credencial** .  
  
  

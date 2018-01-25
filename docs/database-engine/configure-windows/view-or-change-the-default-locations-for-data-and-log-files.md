---
title: Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro | Microsoft Docs
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2f5d4d317ce451cd9080142589817118653a7019
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
 El mejor procedimiento para proteger los archivos de datos y de registro es asegurarse de que estén protegidos mediante listas de control de acceso (ACL). Establezca las ACL en el directorio raíz en el que se crean los archivos.  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>Ver o cambiar las ubicaciones predeterminadas de los archivos de base de datos  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en el servidor y, luego, haga clic en **Propiedades**.  
  
2.  En el panel de la izquierda de esa página Propiedades, haga clic en la pestaña **Configuración de base de datos** .  
  
3.  En **Ubicaciones predeterminadas de la base de datos**, vea las ubicaciones predeterminadas actuales de los archivos de datos y de registro nuevos. Para cambiar una ubicación predeterminada, escriba una nueva ruta de acceso predeterminada en el campo **Datos** o **Registro** , o haga clic en el botón Examinar para buscar y seleccionar una ruta de acceso.  
  
>**NOTA:** Después de cambiar las ubicaciones predeterminadas, debe detener e iniciar el servicio SQL Server para completar el cambio.  
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Crear una base de datos](../../relational-databases/databases/create-a-database.md)  
  
  

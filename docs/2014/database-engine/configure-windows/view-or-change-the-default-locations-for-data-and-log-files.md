---
title: Ver o cambiar las ubicaciones predeterminadas de los datos y archivos de registro (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b62c6264686efe2b117ca755fc291c784308fe9d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320785"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro (SQL Server Management Studio)
  En este tema se describe cómo ver y cambiar las ubicaciones predeterminadas de los archivos de datos y registro nuevos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La ruta de acceso predeterminada se obtiene del Registro. Después de cambiar la ubicación todas las nuevas bases de datos creadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizará dicha ubicación si no se ha especificado otra.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para ver o cambiar los datos y registro predeterminado ubicaciones de archivos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Seguimiento:**  [Cambiar las ubicaciones predeterminadas](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Recommendations"></a> Recomendaciones  
 El mejor procedimiento para proteger los archivos de datos y de registro es asegurarse de que estén protegidos mediante listas de control de acceso (ACL). Las listas de control de acceso se deben establecer en el directorio raíz en el que se crean los archivos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>Para ver o cambiar las ubicaciones predeterminadas de los archivos de base de datos  
  
1.  En el Explorador de objetos, haga clic con el botón secundario en un servidor y haga clic en **Propiedades**.  
  
2.  En el panel izquierdo, haga clic en la página **Configuración de base de datos** .  
  
3.  En **Ubicaciones predeterminadas de la base de datos**, vea las ubicaciones predeterminadas actuales de los archivos de datos y de registro nuevos. Para cambiar una ubicación predeterminada, escriba una nueva ruta de acceso predeterminada en el campo **Datos** o **Registro** , o haga clic en el botón Examinar para buscar y seleccionar una ruta de acceso.  
  
##  <a name="FollowUp"></a> Seguimiento: Después de cambiar las ubicaciones predeterminadas  
 Debe detener e iniciar el servicio SQL Server para completar el cambio.  
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Crear una base de datos](../../relational-databases/databases/create-a-database.md)  
  
  

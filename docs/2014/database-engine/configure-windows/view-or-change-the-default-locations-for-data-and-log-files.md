---
title: Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y de registro (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: def6be137aecbab7f2730fa4c2bf210b374a3a7a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934736"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro (SQL Server Management Studio)
  En este tema se describe cómo ver y cambiar las ubicaciones predeterminadas de los archivos de datos y registro nuevos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La ruta de acceso predeterminada se obtiene del Registro. Después de cambiar la ubicación todas las nuevas bases de datos creadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizará dicha ubicación si no se ha especificado otra.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para ver o cambiar las ubicaciones predeterminadas de los archivos de datos y de registro, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Seguimiento:**  [Cambiar las ubicaciones predeterminadas](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
 El mejor procedimiento para proteger los archivos de datos y de registro es asegurarse de que estén protegidos mediante listas de control de acceso (ACL). Las listas de control de acceso se deben establecer en el directorio raíz en el que se crean los archivos.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>Para ver o cambiar las ubicaciones predeterminadas de los archivos de base de datos  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y haga clic en **Propiedades**.  
  
2.  En el panel izquierdo, haga clic en la página **Configuración de base de datos** .  
  
3.  En **Ubicaciones predeterminadas de la base de datos**, vea las ubicaciones predeterminadas actuales de los archivos de datos y de registro nuevos. Para cambiar una ubicación predeterminada, escriba una nueva ruta de acceso predeterminada en el campo **Datos** o **Registro** , o haga clic en el botón Examinar para buscar y seleccionar una ruta de acceso.  
  
##  <a name="follow-up-after-changing-the-default-locations"></a><a name="FollowUp"></a>Seguimiento: después de cambiar las ubicaciones predeterminadas  
 Debe detener e iniciar el servicio SQL Server para completar el cambio.  
  
## <a name="see-also"></a>Consulte también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Crear una base de datos](../../relational-databases/databases/create-a-database.md)  
  
  

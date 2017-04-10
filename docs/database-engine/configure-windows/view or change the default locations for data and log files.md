---
title: "Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "archivos de registro [SQL Server], cambiar la ubicación predeterminada"
  - "archivos de datos [SQL Server], cambiar la ubicación predeterminada"
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro (SQL Server Management Studio)
  En este tema se describe cómo ver y cambiar las ubicaciones predeterminadas de los archivos de registro y datos nuevos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La ruta de acceso predeterminada se obtiene del Registro. Después de cambiar la ubicación todas las nuevas bases de datos creadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizará dicha ubicación si no se ha especificado otra.  
  
 
##  <a name="Recommendations"></a> Recomendaciones  
 El mejor procedimiento para proteger los archivos de datos y de registro es asegurarse de que estén protegidos mediante listas de control de acceso (ACL). Establezca las ACL en el directorio raíz en el que se crean los archivos.  
  
  
## Ver o cambiar las ubicaciones predeterminadas de los archivos de base de datos  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en el servidor y, luego, haga clic en **Propiedades**.  
  
2.  En el panel de la izquierda de esa página Propiedades, haga clic en la pestaña **Configuración de base de datos**.  
  
3.  En **Ubicaciones predeterminadas de la base de datos**, vea las ubicaciones predeterminadas actuales de los archivos de datos y de registro nuevos. Para cambiar una ubicación predeterminada, escriba una nueva ruta de acceso predeterminada en el campo **Datos** o **Registro** , o haga clic en el botón Examinar para buscar y seleccionar una ruta de acceso.  
  
>**NOTA:** Después de cambiar las ubicaciones predeterminadas, debe detener e iniciar el servicio SQL Server para completar el cambio.  
  
## Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Crear una base de datos](../../relational-databases/databases/create-a-database.md)  
  
  
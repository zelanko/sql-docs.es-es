---
title: "P&#225;gina Escribir contrase&#241;as (Asistente para agregar r&#233;plica) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.addreplicawizard.enterpasswords.f1"
ms.assetid: e69207a0-c5c4-44e4-ae9a-4afbb67251d1
caps.latest.revision: 7
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 7
---
# P&#225;gina Escribir contrase&#241;as (Asistente para agregar r&#233;plica)
  En este tema de Ayuda se describen las opciones de la página **Escribir contraseñas** . Este tema se aplica al [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Si las réplicas que seleccionó en la página **Especificar réplicas** contienen bases de datos que tienen una clave maestra de base de datos, aparecerá la página Escribir contraseñas.  
  
## Opciones para escribir contraseñas  
 La cuadrícula **Usar bases de datos en esta instancia de SQL Server** muestra cada base de datos de usuario local. Estas son sus columnas:  
  
 **Nombre**  
 Muestra el nombre de una base de datos de usuario local.  
  
 **Tamaño**  
 Muestra el tamaño de la base de datos, si el tamaño está disponible para el asistente.  
  
 **Estado**  
 Indica **Se requiere contraseña** en bases de datos que tienen una clave maestra de base de datos. Después de escribir las contraseñas para las claves maestras de base de datos en la columna **Contraseñas** , haga clic en **Actualizar**. Si ha especificado la contraseña correctamente, la columna **Estado** indica **Password entered**(Contraseña escrita).  
  
 Si la base de datos no tiene una clave maestra de base de datos, el **estado** columna indica **No se necesita contraseña**.  
  
 **Contraseña**  
 Si la columna **Estado** indica **Se requiere contraseña**, escriba la contraseña de la clave maestra de base de datos.  
  
 **Actualizar**  
 Haga clic para actualizar la cuadrícula. Esto es útil después de escribir las contraseñas necesarias.  
  
## Tareas relacionadas  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## Vea también  
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)  
  
  
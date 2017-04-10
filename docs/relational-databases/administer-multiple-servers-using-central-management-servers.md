---
title: "Administrar varios servidores mediante Servidores de administraci&#243;n central | Microsoft Docs"
ms.custom: ""
ms.date: "08/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas multiservidor"
  - "servidor de administración central"
  - "administración multiservidor [SQL Server]"
  - "servidores maestros [SQL Server], servidores de administración central"
  - "configuración de destino [SQL Server]"
  - "configuración de servidor [SQL Server]"
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Administrar varios servidores mediante Servidores de administraci&#243;n central
  Puede administrar varios servidores designando los servidores de administración central y creando grupos de servidores.  
  
## ¿Qué son un servidor de administración central y los grupos de servidores?  
 Una instancia de SQL Server designada como servidor de administración central mantiene los grupos de servidores que contienen la información de conexión de una o varias instancias. Puede ejecutar instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] y directivas de administración basada en directivas al mismo tiempo en grupos de servidores. También puede ver los archivos de registro en las instancias que se administran a través de un servidor de administración central. 
 
 Básicamente, un servidor de administración central es un repositorio central que contiene una lista de los servidores administrados. Las versiones anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] no se pueden designar como servidores de administración central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] también se pueden ejecutar con los grupos de servidores locales en Servidores registrados.  
  
## Crear servidor de administración central y grupos de servidores 
 Para crear un Servidor de administración central y grupos de servidores, use la ventana **Servidores registrados** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que el servidor de administración central no puede ser miembro de un grupo que mantenga. 
 
 Para obtener más información sobre cómo crear servidores de administración central y grupos de servidores, consulte [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## Vea también  
 [Administrar servidores mediante administración basada en directivas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
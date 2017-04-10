---
title: "Tutorial: Preparar el servidor para la replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicación [SQL Server], tutoriales"
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Tutorial: Preparar el servidor para la replicaci&#243;n
Es importante planificar la seguridad antes de configurar la topología de replicación. En este tutorial se muestra cómo proteger una topología de replicación y cómo configurar la distribución, que es el primer paso en la replicación de datos. Debe finalizar este tutorial antes que cualquiera de los otros tutoriales.  
  
> [!NOTE]  
> Para replicar datos de forma segura entre servidores, debe implementar todas las recomendaciones de [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Aprendizaje  
En este tutorial aprenderá a preparar un servidor de manera que la replicación se ejecute de forma segura con los privilegios mínimos. En la primera lección se muestra cómo crear cuentas de servicio de Windows utilizadas para ejecutar agentes de replicación. En la segunda lección se muestra cómo configurar la carpeta utilizada para generar y almacenar instantáneas de publicación. En la tercera lección se muestra cómo configurar la distribución y establecer permisos.  
  
## Requisitos  
Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación.  
  
Para utilizar este tutorial, el sistema debe tener instalados los siguientes componentes:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
**Tiempo estimado para completar este tutorial: 30 minutos.**  
  
## Lecciones de este tutorial  
  
-   [Lección 1: Crear cuentas de Windows para replicación](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lección 2: Preparar la carpeta de instantáneas](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lección 3: Configurar la distribución](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[Iniciar el tutorial](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## Vea también  
[Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
[Seguridad y protección &#40;Replicación&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  

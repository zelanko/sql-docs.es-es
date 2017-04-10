---
title: "Ejecutar scripts durante la sincronizaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sincronización [replicación de SQL Server], scripts"
  - "scripts [replicación de SQL Server], sincronización y"
  - "sp_addscriptexec"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Ejecutar scripts durante la sincronizaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  La replicación admite la ejecución de script a petición para suscriptores a publicaciones transaccionales y de combinación. Esta funcionalidad copia el script en el directorio de trabajo de la replicación y, a continuación, usa **sqlcmd** para aplicar el script en el suscriptor. De forma predeterminada, si hay un error al aplicar el script para una suscripción a una publicación transaccional, el Agente de distribución se detendrá. Puede especificar que un script [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecute mediante programación con los procedimientos almacenados de la replicación.  
  
### Para especificar que un script se ejecute para todos los suscriptores a una publicación transaccional, de instantáneas o de combinación  
  
1.  Cree y pruebe el script [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutará a petición.  
  
2.  Guarde el archivo de script en una ubicación en la que pueda tener acceso el Agente de instantáneas de la publicación.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addscriptexec & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Especifique **@publication**, el nombre del archivo de script con la ruta UNC completa creada en el paso 2 para **@scriptfile**y uno de los valores siguientes para **@skiperror**:  
  
    -   **0** -el agente dejará de ejecutarse el script si se produce un error.  
  
    -   **1** -el agente registrará errores y seguir ejecutando la secuencia de comandos cuando se producen errores.  
  
4.  El script especificado se ejecutará en cada suscriptor cuando el agente se vuelva a ejecutar para sincronizar la suscripción.  
  
## Vea también  
 [Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
  
  
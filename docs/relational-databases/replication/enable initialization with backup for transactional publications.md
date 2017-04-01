---
title: "Habilitar la inicializaci&#243;n con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicialización de suscripción manual [replicación de SQL Server]"
  - "suscripciones [replicación de SQL Server], inicializar"
  - "inicializar suscripciones [replicación de SQL Server], sin instantáneas"
  - "replicación transaccional, copia de seguridad y restauración"
  - "copias de seguridad [replicación de SQL Server], replicación transaccional"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Habilitar la inicializaci&#243;n con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio)
  Para inicializar una suscripción a una publicación transaccional desde una copia de seguridad, habilite la publicación para permitir la inicialización desde la copia de seguridad y, después, especifique la información de la copia de seguridad al crear la suscripción:  
  
-   Habilitar la publicación en el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Especifique la información de copia de seguridad con el procedimiento almacenado [sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para obtener más información acerca de los parámetros requeridos por **sp_addsubscription**, consulte [inicializar una suscripción transaccional desde una copia de seguridad y Nº 40; Programación de replicación Transact-SQL & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md).  
  
### Para habilitar la inicialización con una copia de seguridad  
  
1.  En el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione el valor **True** para el **Permitir inicialización desde archivos de copia de seguridad** opción.  
  
## Vea también  
 [Inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
---
title: "Especificar el formato de instant&#225;nea (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [replicación de SQL Server], formatos"
  - "replicación de instantáneas [SQL Server], formatos"
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Especificar el formato de instant&#225;nea (SQL Server Management Studio)
  Especificar el formato de instantánea en la **instantánea** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para especificar el formato de instantánea  
  
1.  En el **instantánea** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecutan SQL Server** o **carácter: necesario si un publicador o suscriptor no ejecuta SQL Server**.  
  
    > [!NOTE]  
    >  Se recomienda seleccionar el formato nativo, a menos que esta publicación deba ser compatible con suscripciones a una base de datos de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o una base de datos que no sea de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Vea también  
 [Configurar propiedades de la instantánea & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
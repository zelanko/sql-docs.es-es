---
title: Conceder acceso a una base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30de5de3d238905802e80d433c2df7deaf058929
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-2---granting-access-to-a-database"></a>Lección 2: 2: conceder acceso a una base de datos
Mary ahora tiene acceso a esta instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero no tiene permiso para tener acceso a las bases de datos. Incluso no tiene acceso a su propia base de datos **TestData** hasta que la autorice como usuario de base de datos.  
  
Para conceder acceso a Mary, cambie a la base de datos **TestData** y, a continuación, use la instrucción CREATE USER para asignar su inicio de sesión a un usuario denominado Mary.  
  
### <a name="to-create-a-user-in-a-database"></a>Para crear un usuario en una base de datos  
  
1.  Escriba y ejecute las siguientes instrucciones (reemplace `computer_name` con el nombre de su equipo) para conceder acceso a `Mary` a la base de datos `TestData` .  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    Ahora, Mary tiene acceso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y a la base de datos `TestData` .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Crear vistas y procedimientos almacenados](../t-sql/lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
  


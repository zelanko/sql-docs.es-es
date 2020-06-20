---
title: Conceder acceso a una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0e9a67ddf9ff079c4ff5075b8601aec4c0922e89
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85000603"
---
# <a name="granting-access-to-a-database"></a>Conceder acceso a una base de datos
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
 [Crear vistas y procedimientos almacenados](lesson-2-3-creating-views-and-stored-procedures.md)  
  
  

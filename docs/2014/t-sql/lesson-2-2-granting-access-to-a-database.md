---
title: Conceder acceso a una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 11
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7971df050304f242e79abcc7e26bdb5d31e5fb09
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037096"
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
  
  

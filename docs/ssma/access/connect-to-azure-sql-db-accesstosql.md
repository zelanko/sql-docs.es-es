---
title: Conectarse a la base de datos de SQL Azure (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 86a145cd23f40e41ef63b166e7536f91ee2129d9
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conectarse a la base de datos de SQL Azure (AccessToSQL)
Use el cuadro de diálogo de SQL Azure para conectarse a la base de datos de SQL Azure que se va a migrar.  
  
Para tener acceso a este cuadro de diálogo, en la **archivo** menú, seleccione **conectarse a SQL Azure**. Si se ha conectado anteriormente, el comando es **volver a conectar a SQL Azure.**  
  
## <a name="options"></a>Opciones  
**Nombre de servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a SQL Azure.  
  
**Base de datos**  
  
Seleccione, escriba o **examinar** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para Access no es compatible con la conexión a la base de datos maestra en SQL Azure.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de SQL Azure SSMA  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Cifrar**  
  
SSMA recomienda conexión cifrada a SQL Azure.  
  
## <a name="create-azure-database"></a>Crear base de datos de Azure  
Para crear una nueva base de datos de azure, siga los pasos siguientes  
  
1.  Haga clic en el botón Examinar que se encuentra en la conexión al cuadro de diálogo de SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen dos elementos de menú  
  
    1.  **(no hay bases de datos que se encuentra)**  que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Crear nueva base de datos** que siempre está habilitada, lo que permite al usuario crear una nueva base de datos de azure en la cuenta de SQL Azure. Al hacer clic en este elemento de menú, crear cuadro de diálogo de la base de datos de azure está presente con el nombre de la base de datos y el tamaño.  
  
3.  En el momento de creación de la base de datos, estos dos parámetros se proporciona como entrada.  
  
    1.  **Nombre de base de datos:** escriba el nombre de la base de datos.  
  
    2.  **Tamaño de base de datos:** seleccione el tamaño de base de datos que se debe crear en la cuenta de SQL Azure.  
  


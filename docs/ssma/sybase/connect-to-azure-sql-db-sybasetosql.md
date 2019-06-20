---
title: Conectarse a Azure SQL DB (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 057a39fd393be6cce9232d787b0d110a4be2035a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63060998"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Conectarse a Azure SQL DB (SybaseToSQL)
Utilice la conexión al cuadro de diálogo de Azure SQL DB para conectarse a la base de datos de Azure SQL DB que se va a migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **Connect a Azure SQL DB**. Si se ha conectado anteriormente, el comando es **volver a conectar a Azure SQL DB.**  
  
## <a name="options"></a>Opciones  
**Nombre de servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a Azure SQL DB.  
  
**Base de datos**  
  
Seleccione, escriba o **examinar** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite la conexión a la base de datos maestra en la base de datos de SQL Azure.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de Azure SQL DB SSMA  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Encrypt**  
  
SSMA recomienda conexión cifrada a Azure SQL DB.  
  
## <a name="create-azure-database"></a>Crear base de datos de Azure  
Si no hay ninguna base de datos en la cuenta de Azure SQL DB, puede crear la primera base de datos.  
  
Para crear una nueva base de datos por primera vez, siga los pasos siguientes  
  
1.  Haga clic en el botón Examinar que se encuentra en la conexión al cuadro de diálogo de la base de datos de SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen los siguientes dos elementos de menú.  
  
    1.  **(no hay bases de datos que se encuentra)**  que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Crear nueva base de datos** que está habilitada sólo cuando no hay ninguna base de datos en la cuenta de Azure SQL DB. Al hacer clic en este elemento de menú, cuadro de diálogo Crear base de datos de Azure está presente con el tamaño y el nombre de la base de datos.  
  
3.  En el momento de creación de la base de datos, los dos parámetros siguientes se proporcionan como entrada:  
  
    1.  **Nombre de la base de datos:** Escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** Seleccione el tamaño de base de datos que necesita para crear en la cuenta de Azure SQL DB.  
  

---
title: Conectarse a Azure SQL DB (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 12da1aa42f468b92e1833410e635183aabf3a384
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103245"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Conectarse a Azure SQL DB (MySQLToSQL)
Utilice la conexión al cuadro de diálogo de SQL Azure para conectarse a la base de datos de SQL Azure que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **conectarse a SQL Azure**. Si se ha conectado anteriormente, el comando es **volver a conectar a SQL Azure.**  
  
## <a name="options"></a>Opciones  
**Nombre de servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a SQL Azure.  
  
**Base de datos**  
  
Seleccione, escriba o **examinar** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para MySQL no admite la conexión a la base de datos maestra en SQL Azure.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de SQL Azure SSMA  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Encrypt**  
  
SSMA recomienda conexión cifrada a SQL Azure.  
  
## <a name="create-azure-database"></a>Crear base de datos de Azure  
Si no hay ninguna base de datos en la cuenta de SQL Azure, puede crear la primera base de datos.  
  
Para crear una nueva base de datos por primera vez, siga los pasos siguientes  
  
1.  Haga clic en el botón Examinar que se encuentra en la conexión al cuadro de diálogo de SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen los siguientes dos elementos de menú.  
  
    1.  **(no hay bases de datos que se encuentra)**  que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Crear nueva base de datos** que está habilitada sólo cuando no hay ninguna base de datos en la cuenta de SQL Azure. Al hacer clic en este elemento de menú, cuadro de diálogo Crear base de datos de Azure está presente con el tamaño y el nombre de la base de datos.  
  
3.  En el momento de creación de la base de datos, los dos parámetros siguientes se proporcionan como entrada:  
  
    1.  **Nombre de la base de datos:** Escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** Seleccione el tamaño de base de datos que necesita para crear en la cuenta de SQL Azure.  
  

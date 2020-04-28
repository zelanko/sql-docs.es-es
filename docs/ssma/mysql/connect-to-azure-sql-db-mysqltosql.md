---
title: Conexión a Azure SQL DB (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103245"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Conectarse a Azure SQL DB (MySQLToSQL)
Utilice el cuadro de diálogo conectar con SQL Azure para conectarse a la base de datos de SQL Azure que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a SQL Azure**. Si ya se ha conectado, el comando se **vuelve a conectar a SQL Azure.**  
  
## <a name="options"></a>Opciones  
**Nombre del servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a SQL Azure.  
  
**Base de datos**  
  
Seleccione, escriba o **examine** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para MySQL no admite la conexión a la base de datos maestra en SQL Azure.  
  
**Nombre de usuario**  
  
Escriba el nombre de usuario que SSMA usará para conectarse a la base de datos de SQL Azure  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Encrypt**  
  
SSMA recomienda una conexión cifrada para SQL Azure.  
  
## <a name="create-azure-database"></a>Creación de una base de datos de Azure  
Si no hay ninguna base de datos en la cuenta de SQL Azure, puede crear la primera base de datos.  
  
Para crear una nueva base de datos por primera vez, siga los pasos siguientes:  
  
1.  Haga clic en el botón examinar que se encuentra en el cuadro de diálogo conectar con SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen los dos elementos de menú siguientes.  
  
    1.  **(no se encontró ninguna base de datos)** que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Cree una nueva base de datos** que solo esté habilitada cuando no haya bases de datos en SQL Azure cuenta. Al hacer clic en este elemento de menú, el cuadro de diálogo crear base de datos de Azure aparece con el nombre y el tamaño de la base de datos.  
  
3.  En el momento de la creación de la base de datos, los dos parámetros siguientes se proporcionan como entrada:  
  
    1.  **Nombre de la base de datos:** Escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** Seleccione el tamaño de la base de datos que necesita crear en SQL Azure cuenta.  
  

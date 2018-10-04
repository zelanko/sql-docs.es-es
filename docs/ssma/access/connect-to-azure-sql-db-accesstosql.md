---
title: Conectarse a Azure SQL DB (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 57a745385de80a3040897310ddc5b43b1301ea86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717483"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conectarse a Azure SQL DB (AccessToSQL)
Utilice la conexión al cuadro de diálogo de SQL Azure para conectarse a la base de datos de SQL Azure que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **conectarse a SQL Azure**. Si se ha conectado anteriormente, el comando es **volver a conectar a SQL Azure.**  
  
## <a name="options"></a>Opciones  
**Nombre de servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a SQL Azure.  
  
**Base de datos**  
  
Seleccione, escriba o **examinar** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para Access no admite la conexión a la base de datos maestra en SQL Azure.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de SQL Azure SSMA  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Encrypt**  
  
SSMA recomienda conexión cifrada a SQL Azure.  
  
## <a name="create-azure-database"></a>Crear base de datos de Azure  
Para crear una nueva base de datos de azure, siga los pasos siguientes  
  
1.  Haga clic en el botón Examinar que se encuentra en la conexión al cuadro de diálogo de SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen dos elementos de menú  
  
    1.  **(no hay bases de datos que se encuentra)**  que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Crear nueva base de datos** que siempre está habilitada, lo que permite al usuario crear una nueva base de datos de azure en la cuenta de SQL Azure. Al hacer clic en este elemento de menú, crear está presente con el nombre de la base de datos y el tamaño del cuadro de diálogo de la base de datos de azure.  
  
3.  En el momento de creación de la base de datos, estos dos parámetros se proporciona como entrada.  
  
    1.  **Nombre de la base de datos:** escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** seleccionar el tamaño de base de datos que se debe crear en la cuenta de SQL Azure.  
  

---
title: Conexión a Azure SQL Database (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 34e25824ee95745bd5069a6ed601318d47a96e81
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865253"
---
# <a name="connect-to-azure-sql-database-accesstosql"></a>Conexión a Azure SQL Database (AccessToSQL)
Utilice el cuadro de diálogo conectar con SQL Azure para conectarse a la base de datos de SQL Azure que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a SQL Azure**. Si ya se ha conectado, el comando se **vuelve a conectar a SQL Azure.**  
  
## <a name="options"></a>Opciones  
**Nombre de servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a SQL Azure.  
  
**Base de datos**  
  
Seleccione, escriba o **examine** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para Access no admite la conexión a la base de datos maestra en SQL Azure.  
  
**Nombre de usuario**  
  
Escriba el nombre de usuario que SSMA usará para conectarse a la base de datos de SQL Azure  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**Encrypt**  
  
SSMA recomienda una conexión cifrada para SQL Azure.  
  
## <a name="create-database"></a>Crear base de datos  
Para crear una nueva base de datos, siga estos pasos:  
  
1.  Haga clic en el botón examinar que se encuentra en el cuadro de diálogo conectar con SQL Azure  
  
2.  Si no hay ninguna base de datos, aparecen dos elementos de menú.  
  
    1.  **(no se encontró ninguna base de datos)** que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Cree una nueva base de datos** que siempre esté habilitada, lo que permite al usuario crear una nueva base de datos. Al hacer clic en este elemento de menú, el cuadro de diálogo crear base de datos está presente con el nombre y el tamaño de la base de datos.  
  
3.  En el momento de la creación de la base de datos, estos dos parámetros se proporcionan como entrada.  
  
    1.  **Nombre de la base de datos:** Escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** Seleccione el tamaño de la base de datos que necesita crear en SQL Azure cuenta.  
  

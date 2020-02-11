---
title: Conexión a Azure SQL DB (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 68fbac69959d423477750a69bb6e5b06ab62af2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083472"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Conectarse a Azure SQL DB (SybaseToSQL)
Use el cuadro de diálogo conectar a base de datos SQL de Azure para conectarse a la base de datos de Azure SQL Database que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a Azure SQL dB**. Si ya se ha conectado, el comando se **vuelve a conectar a Azure SQL dB.**  
  
## <a name="options"></a>Opciones  
**Nombre del servidor**  
  
Seleccione o escriba el nombre del servidor para conectarse a Azure SQL DB.  
  
**Base de datos**  
  
Seleccione, escriba o **examine** el nombre de la base de datos.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite la conexión a la base de datos maestra en Azure SQL DB.  
  
**Nombre de usuario**  
  
Escriba el nombre de usuario que SSMA usará para conectarse a la base de datos de Azure SQL DB  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario  
  
**Toda**  
  
SSMA recomienda una conexión cifrada a Azure SQL DB.  
  
## <a name="create-azure-database"></a>Creación de una base de datos de Azure  
Si no hay ninguna base de datos en la cuenta de Azure SQL DB, puede crear la primera base de datos.  
  
Para crear una nueva base de datos por primera vez, siga los pasos siguientes:  
  
1.  Haga clic en el botón examinar que se encuentra en el cuadro de diálogo conectarse a Azure SQL DB  
  
2.  Si no hay ninguna base de datos, aparecen los dos elementos de menú siguientes.  
  
    1.  **(no se encontró ninguna base de datos)** que está deshabilitada y atenuada todo el tiempo  
  
    2.  **Cree una nueva base de datos** que solo esté habilitada cuando no haya bases de datos en la cuenta de Azure SQL Database. Al hacer clic en este elemento de menú, el cuadro de diálogo crear base de datos de Azure aparece con el nombre y el tamaño de la base de datos.  
  
3.  En el momento de la creación de la base de datos, los dos parámetros siguientes se proporcionan como entrada:  
  
    1.  **Nombre de la base de datos:** Escriba el nombre de la base de datos.  
  
    2.  **Tamaño de la base de datos:** Seleccione el tamaño de la base de datos que necesita crear en la cuenta de Azure SQL DB.  
  

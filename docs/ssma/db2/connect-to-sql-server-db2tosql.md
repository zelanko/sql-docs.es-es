---
title: Conexión a SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: bc14a072-8949-4ee0-a4b4-ada55fe8df5c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3d96be29aa74d3903e47f20ec6841b4a20135727
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68141077"
---
# <a name="connect-to-sql-server-db2tosql"></a>Conexión a SQL Server (DB2ToSQL)
Utilice el cuadro de diálogo **conectar con SQL Server** para conectarse a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de a la que desea migrar. Para tener acceso al cuadro de diálogo **conectar con SQL Server** , en el menú **archivo** , haga clic en **conectar a SQL Server**.  
  
## <a name="options"></a>Opciones  
**Nombre del servidor**  
Escriba o seleccione la instancia de SQL Server a la que se va a conectar. De forma predeterminada, se muestra la instancia de a la que se conectó más recientemente.  
  
-   Si se está conectando a la instancia predeterminada en el equipo local, puede especificar **localhost** o un punto (**.**).  
  
-   Si se va a conectar a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
-   Si se va a conectar a una instancia con nombre en otro equipo, escriba el nombre del equipo, una barra diagonal inversa y el nombre de la instancia, *por ejemplo*\\, mi*instancia*.  
  
**Puerto de servidor**  
Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está configurada para aceptar conexiones en el puerto predeterminado (1433), escriba el número de puerto. De lo contrario, deje este valor en blanco.  
  
**Base de datos**  
Especifique la base de datos a la que se van a migrar objetos y datos. Esta opción no está disponible cuando se vuelve a conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a.  
  
**Autenticación**  
Seleccione el método de autenticación que se utiliza para conectarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a. Para usar la cuenta de Windows actual, seleccione autenticación de Windows. Para especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión y una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contraseña, seleccione autenticación.  
  
**Nombre de usuario**  
Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la autenticación de, escriba el inicio de sesión de para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]esa instancia de. Si usa la autenticación de Windows, esta opción no está disponible.  
  
**Contraseña**  
Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la autenticación de, escriba la contraseña para el inicio de sesión de en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]esa instancia de. Si usa la autenticación de Windows, esta opción no está disponible.  
  
**Cifrar conexión**  
Si desea conectarse de forma segura a SQL Server, haga uso de cifrar conexión activando la casilla **cifrar conexión** .  
  
**Confiar en certificado de servidor**  
Si desea usar esta opción, active la casilla **confiar en certificado de servidor** .  
  
> [!NOTE]  
> Para habilitar el **certificado de servidor de confianza**, "Encrypt" debe establecerse en **true**.  
  

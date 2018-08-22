---
title: Conectarse a SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4ef384ea-5f3e-4f70-ad7c-b62d7b0da628
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: 3d57af05812d68056805ba578d1dc1e53822fbd2
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393896"
---
# <a name="connect-to-sql-server--oracletosql"></a>Conectarse a SQL Server (OracleToSQL)
Use la **conectar con SQL Server** cuadro de diálogo para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea migrar a. Para tener acceso a la **conectar con SQL Server** cuadro de diálogo el **archivo** menú, haga clic en **conectar con SQL Server**.  
  
## <a name="options"></a>Opciones  
**Nombre del servidor**  
Escriba o seleccione la instancia de SQL Server para conectarse a. De forma predeterminada, se muestra la instancia que se haya conectado más recientemente.  
  
-   Si se conecta a la instancia predeterminada en el equipo local, puede escribir cualquiera **localhost** o un punto (**.**).  
  
-   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
-   Si se conecta a una instancia con nombre en otro equipo, escriba el nombre del equipo, una barra diagonal inversa y el nombre de instancia, como *MyServer*\\*MyInstance*.  
  
**Puerto del servidor**  
Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está configurado para aceptar las conexiones en el valor predeterminado (1433) de puerto, escriba el número de puerto. En caso contrario, deje este valor en blanco.  
  
**Base de datos**  
Especifique la base de datos para migrar objetos y datos. Esta opción no está disponible al volver a conectarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Autenticación**  
Seleccione el método de autenticación que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para usar la cuenta de Windows actual, seleccione autenticación de Windows. Para especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión y contraseña, seleccione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.  
  
**Nombre de usuario.**  
Si usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, escriba el inicio de sesión para esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si usas la autenticación de Windows, esta opción no está disponible.  
  
**Contraseña**  
Si usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, escriba la contraseña para el inicio de sesión en esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si usas la autenticación de Windows, esta opción no está disponible.  
  
**Cifrar conexión**  
Si desea conectarse de forma segura a SQL Server, asegúrese de usar de conexión Encrypt activando el **cifrar conexión** casilla de verificación.  
  
**TrustServerCertificate**  
Si desea usar esta opción, seleccione el **confiar en certificado de servidor** casilla de verificación.  
  
> [!NOTE]  
> Para habilitar **confiar en certificado de servidor**, "Cifrar" debe establecerse en **True**.  
  

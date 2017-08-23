---
title: Conectarse a SQL Server (MySQLToSQL) | Documentos de Microsoft
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
ms.assetid: d73abd3a-80df-4293-b973-1723069db049
caps.latest.revision: 3
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 514aebaf8dad32b7ff2ffd97d9d873de59e87713
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sql-server-mysqltosql"></a>Conectarse a SQL Server (MySQLToSQL)
Use la **conectar con SQL Server** cuadro de diálogo para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que van a migrar a. Para tener acceso a la **conectar con SQL Server** cuadro de diálogo, en la **archivo** menú, haga clic en **conectar con SQL Server**.  
  
## <a name="options"></a>Opciones  
**Nombre del servidor**  
Escriba o seleccione la instancia de SQL Server para conectarse a. De forma predeterminada, se muestra la instancia que se conectó más recientemente.  
  
-   Si se conecta a la instancia predeterminada en el equipo local, puede escribir cualquiera **localhost** o un punto (**.**).  
  
-   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
-   Si se conecta a una instancia con nombre en otro equipo, escriba el nombre del equipo, una barra diagonal inversa y el nombre de instancia, como *MyServer*\\*MyInstance*.  
  
**Puerto del servidor**  
Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no está configurado para aceptar las conexiones en el valor predeterminado (1433) de puerto, escriba el número de puerto. En caso contrario, deje este valor en blanco.  
  
**Base de datos**  
Especifique la base de datos para migrar objetos y datos. Esta opción no está disponible cuando vuelve a conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Autenticación**  
Seleccione el método de autenticación que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para usar su cuenta de Windows actual, seleccione autenticación de Windows. Para especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] inicio de sesión y una contraseña, seleccione [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación.  
  
**Nombre de usuario.**  
Si utilizas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, escriba el inicio de sesión para esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si usa la autenticación de Windows, esta opción no está disponible.  
  
**Contraseña**  
Si utilizas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, escriba la contraseña para el inicio de sesión en esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si usa la autenticación de Windows, esta opción no está disponible.  
  
**Cifrar conexión**  
Si desea conectarse de forma segura a SQL Server, asegúrese de usar de cifrar conexión comprobando el **cifrar conexión** casilla de verificación.  
  
**TrustServerCertificate**  
Si desea usar esta opción, seleccione la **confiar en certificado de servidor** casilla de verificación.  
  
> [!NOTE]  
> Para habilitar **confiar en certificado de servidor**, "Cifrar" debe establecerse en **True**.  
  


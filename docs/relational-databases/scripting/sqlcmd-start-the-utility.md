---
title: Iniciar la utilidad sqlcmd | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 55dddd4edd48e0b6d158168b7140d2617accc683
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcmd---start-the-utility"></a>sqlcmd - Iniciar la utilidad
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] La [utilidad sqlcmd](../../tools/sqlcmd-utility.md) permite escribir instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimientos del sistema y archivos de script en el símbolo del sistema, en el Editor de consultas en modo SQLCMD, en un archivo de script de Windows o en un paso de trabajo del sistema operativo (Cmd.exe) de un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
> [!NOTE]  
>  La autenticación de Windows es el modo de autenticación predeterminado para **sqlcmd**. Para usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe especificar un nombre de usuario y una contraseña mediante las opciones **-U** y **-P** .  
  
> [!NOTE]  
>  De forma predeterminada, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] se instala como la instancia con nombre **sqlexpress**.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Inicio de la utilidad sqlcmd y conexión con una instancia predeterminada de SQL Server  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, a continuación, haga clic en **Aceptar** para abrir una ventana del símbolo del sistema. (Si no se ha conectado antes a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quizás tenga que configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que acepte conexiones).  
  
2.  En el símbolo del sistema, escriba **sqlcmd**.  
  
3.  Presione ENTRAR.  
  
     Ahora tiene una conexión de confianza con la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se está ejecutando en el equipo.  
  
     **1>** es el símbolo del sistema de **sqlcmd** que especifica el número de línea. Cada vez que presione ENTRAR, el número se incrementará en uno.  
  
4.  Para finalizar la sesión de **sqlcmd** , escriba **EXIT** en el símbolo del sistema de **sqlcmd** .  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Inicio de la utilidad sqlcmd y conexión con una instancia con nombre de SQL Server  
  
1.  Abra una ventana del símbolo del sistema y escriba **sqlcmd -S***myServer\instanceName*. Reemplace *myServer\instanceName* por el nombre del equipo y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que quiera conectarse.  
  
2.  Presione ENTRAR.  
  
     El símbolo del sistema de **sqlcmd** (1>) indica que está conectado con la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] escritas están almacenadas en un búfer. Se ejecutan como un lote cuando se encuentra el comando GO.  
  
## <a name="see-also"></a>Ver también  
 [Ejecutar archivos de scripts Transact-SQL mediante sqlcmd](../../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)  
  
  

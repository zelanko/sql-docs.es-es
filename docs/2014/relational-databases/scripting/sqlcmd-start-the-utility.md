---
title: Iniciar la utilidad sqlcmd
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f8f63b4ddb3e8641ef503a615d57c63be35164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75243268"
---
# <a name="start-the-sqlcmd-utility"></a>Iniciar la utilidad sqlcmd
  Para empezar a usar `sqlcmd`, primero debe iniciar la utilidad y conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede conectarse a una instancia con nombre o a la instancia predeterminada. El primer paso consiste en iniciar la utilidad `sqlcmd`.  
  
> [!NOTE]  
>  La autenticación de Windows es el modo de autenticación predeterminado para `sqlcmd`. Para usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe especificar un nombre de usuario y una contraseña mediante las opciones **-U** y **-P** .  
  
> [!NOTE]  
>   De forma predeterminada, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] se instala como la instancia con nombre **sqlexpress**.  
  
 Si no se ha conectado antes a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quizás tenga que configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que acepte conexiones.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Para iniciar la utilidad sqlcmd y conectar con una instancia predeterminada de SQL Server  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, a continuación, haga clic en **Aceptar** para abrir una ventana del símbolo del sistema.  
  
2.  En el símbolo del sistema, escriba `sqlcmd`.  
  
3.  Presione ENTRAR.  
  
     Ahora tiene una conexión de confianza con la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se está ejecutando en el equipo.  
  
     **1>** es el `sqlcmd` símbolo del sistema que especifica el número de línea. Cada vez que presione ENTRAR, el número se incrementará en uno.  
  
4.  Para finalizar la `sqlcmd` sesión, escriba `EXIT` en el `sqlcmd` símbolo del sistema.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Para iniciar la utilidad sqlcmd y conectar con una instancia con nombre de SQL Server  
  
1.  Abra una ventana del símbolo del sistema y `sqlcmd -S`escriba *myServer\instanceName*. Reemplace *myServer\instanceName* por el nombre del equipo y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que quiera conectarse.  
  
2.  Presione ENTRAR.  
  
     El `sqlcmd` símbolo del sistema (1>) indica que está conectado a la instancia especificada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
    > [!NOTE]  
    >  Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] escritas están almacenadas en un búfer. Se ejecutan como un lote cuando se encuentra el comando GO.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar archivos de scripts Transact-SQL mediante sqlcmd](sqlcmd-run-transact-sql-script-files.md)  
  
  

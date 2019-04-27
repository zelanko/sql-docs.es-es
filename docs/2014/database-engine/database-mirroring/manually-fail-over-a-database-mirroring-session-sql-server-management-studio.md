---
title: Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 4ecf9c63-b3a4-4c54-b553-5bc37973232b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b42fdb9d53a4aa0444a98ee311000fb1c2929ff1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756155"
---
# <a name="manually-fail-over-a-database-mirroring-session-sql-server-management-studio"></a>Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos (SQL Server Management Studio)
  Cuando la base de datos reflejada se sincroniza (es decir, cuando el estado de la base de datos es SYNCHRONIZED), el propietario de la base de datos puede iniciar una conmutación por error manual en el servidor reflejado.  
  
 Durante una conmutación por error manual, los roles de servidor principal y reflejado se intercambian en la base de datos en la que se produce la conmutación por error. La base de datos reflejada se convierte en la base de datos principal, y la base de datos principal se convierte en la reflejada. Por ejemplo, en la siguiente tabla se muestra cómo una conmutación por error manual intercambia los roles de dos asociados de creación de reflejo: `SQLDBENGINE0_1` y `SQLDBENGINE0_2`.  
  
|Servidor|Antes de la conmutación por error|Después de la conmutación por error|  
|------------|---------------------|--------------------|  
|`SQLDBENGINE0_1`|PRINCIPAL|MIRROR|  
|`SQLDBENGINE0_2`|MIRROR|PRINCIPAL|  
  
 Observe que los roles de servidor de las demás sesiones de creación de reflejo de la base de datos no se ven afectados. Para obtener más información, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
### <a name="to-manually-fail-over-database-mirroring"></a>Para realizar manualmente una conmutación por error de la creación de reflejo de la base de datos  
  
1.  Conéctese a la instancia de servidor principal y, en el panel **Explorador de objetos** , haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos de la que se va a realizar la conmutación por error.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Reflejado**. Así se abre la página **Creación de reflejo** del cuadro de diálogo **Propiedades de la base de datos** .  
  
4.  Haga clic en **Conmutación por error**.  
  
     Aparece un cuadro de confirmación.  El servidor principal intenta conectarse al servidor reflejado mediante la Autenticación de Windows. Si la Autenticación de Windows no funciona, el servidor principal muestra el cuadro de diálogo **Conectar con el servidor** . Si el servidor reflejado usa la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **Autenticación de SQL Server** en el cuadro **Autenticación** . En el cuadro de texto **Inicio de sesión** , especifique la cuenta de inicio de sesión para conectar con el servidor reflejado, y en el cuadro de texto **Contraseña** , especifique la contraseña correspondiente a la cuenta.  
  
     Si la conmutación por error se realiza correctamente, se cierra el cuadro de diálogo **Propiedades de la base de datos** . La base de datos reflejada se convierte en la base de datos principal, y la base de datos principal se convierte en la reflejada.  
  
     Si no se puede efectuar la conmutación por error, aparece un mensaje de error y el cuadro de diálogo permanece abierto.  
  
    > [!IMPORTANT]  
    >  Si ha modificado alguna propiedad desde que se abrió la página **Creación de reflejos** , estos cambios no se guardarán.  
  
     El cuadro de diálogo se cierra automáticamente.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de la base de datos &#40;página Creación de reflejo&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)   
 [Pausar o reanudar una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
  

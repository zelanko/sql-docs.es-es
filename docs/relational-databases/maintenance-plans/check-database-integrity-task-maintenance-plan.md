---
title: Tarea Comprobar la integridad de la base de datos (Plan de mantenimiento) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.maintplanproperties.integrity.f1
- sql13.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ad37935a63e55d949aaad8b3792e3180e78be5c3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="check-database-integrity-task-maintenance-plan"></a>Tarea Comprobar la integridad de la base de datos (Plan de mantenimiento)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilice el cuadro de diálogo **Tarea Comprobar la integridad de la base de datos** para comprobar la asignación e integridad estructural de las tablas de usuario y del sistema, y los índices de la base de datos por medio de la ejecución de la instrucción `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] . La ejecución de `DBCC` garantiza que se notifiquen todos los problemas de integridad que puedan existir en la base de datos, lo que permitirá su tratamiento posterior por parte de un administrador del sistema o del propietario de la base de datos.  
  
## <a name="options"></a>Opciones  
 **Conexión**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Bases de datos**  
 Especifique las bases de datos a las que afecta esta tarea.  
  
-   **Todas las bases de datos**  
  
     Genere un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de **tempdb**.  
  
-   **Todas las bases de datos del sistema**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de **tempdb**. No se ejecutarán tareas de mantenimiento en las bases de datos creadas por usuarios.  
  
-   **Todas las bases de datos de usuario**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos creadas por usuarios. No se ejecutarán tareas de mantenimiento en las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento únicamente en las bases de datos seleccionadas. Si elige esta opción, deberá seleccionar al menos una base de datos de la lista.  
  
    > [!NOTE]  
    >  Los planes de mantenimiento solo se ejecutan en bases de datos con un nivel de compatibilidad de 80 o superior. Las bases de datos con un nivel de compatibilidad de 70 o inferior no se muestran.  
  
 **Incluir índices**  
 Comprueba la integridad de todas las páginas de índice y de todas las páginas de datos de tabla.  
  
 **Solo físico**  
 Limita la comprobación a la integridad de la estructura física de la página, los encabezados de registros y la coherencia de la asignación de la base de datos. Con esta opción puede reducir el tiempo de ejecución de DBCC CHECKDB en bases de datos grandes, y se recomienda para el uso frecuente en sistemas de producción.  
  
 **Tablock**  
 Hace que DBCC CHECKDB obtenga bloqueos en lugar de utilizar una instantánea de base de datos interna. Se incluye un bloqueo exclusivo (X) a corto plazo en la base de datos. El uso de esta opción puede ayudar a que DBCC CHECKDB se ejecute más rápido en una base de datos con mucha carga, pero mientras está en ejecución disminuye la simultaneidad disponible en la base de datos.  
  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  
  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **Actualizar**  
 Actualiza la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] with Windows Authentication.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication. Esta opción no está disponible.  
  
 **Nombre de usuario.**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Vea también  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
  

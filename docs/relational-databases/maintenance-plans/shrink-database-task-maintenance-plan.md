---
title: Tarea Reducir base de datos (Plan de mantenimiento) | Microsoft Docs
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
- Shrink Database Task
- Shrink Database(s) Task
- sql13.swb.maint.shrink.f1
helpviewer_keywords:
- Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e067169014c05c90b04d9f757fcae397cb1834b
ms.lasthandoff: 04/11/2017

---
# <a name="shrink-database-task-maintenance-plan"></a>Tarea Reducir base de datos (Plan de mantenimiento)
  Utilice el cuadro de diálogo **Tarea Reducir base de datos** para crear una tarea que intente reducir el tamaño de las bases de datos seleccionadas. Utilice las opciones que se indican a continuación para determinar el espacio disponible que se mantiene en la base de datos después de reducir su tamaño (cuanto mayor sea el porcentaje, menos se podrá reducir la base de datos). El valor se basa es un porcentaje de los datos reales de la base de datos. Por ejemplo, una base de datos de 100 MB que contenga 60 MB de datos y 40 MB de espacio disponible, con un porcentaje de espacio disponible del 50 por ciento, dará como resultado 60 MB de datos y 30 MB de espacio disponible (porque el 50 por ciento de 60 MB es 30 MB). Solo se elimina el espacio de la base de datos que exceda el porcentaje indicado. Los valores válidos son de 0 a 100.  
  
 La reducción de los archivos de datos permite recuperar espacio moviendo páginas de datos del final del archivo a espacio desocupado próximo al principio del archivo. Cuando se crea suficiente espacio disponible al final del archivo, las páginas de datos situadas al final del mismo se pueden desasignar y devolver al sistema de archivos.  
  
> [!WARNING]  
>  Los datos que se mueven para reducir un archivo se pueden dispersar en cualquier ubicación disponible en el archivo. Esto produce la fragmentación de índices y puede reducir el rendimiento de las consultas que buscan un intervalo del índice. Para eliminar la fragmentación, considere la posibilidad de volver a generar los índices en el archivo después de la reducción.  
  
 Esta tarea ejecuta la instrucción DBCC SHRINKDATABASE.  
  
## <a name="options"></a>Opciones  
 **Conexión**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Bases de datos**  
 Especifique las bases de datos a las que afecta esta tarea.  
  
-   **Todas las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de tempdb.  
  
-   **Todas las bases de datos del sistema**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de tempdb. No se ejecutarán tareas de mantenimiento en las bases de datos creadas por usuarios.  
  
-   **Todas las bases de datos de usuario**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos creadas por usuarios. No se ejecutarán tareas de mantenimiento en las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento únicamente en las bases de datos seleccionadas. Si elige esta opción, deberá seleccionar al menos una base de datos de la lista.  
  
    > [!NOTE]  
    >  Los planes de mantenimiento solo se ejecutan en bases de datos con un nivel de compatibilidad de 80 o superior. Las bases de datos con un nivel de compatibilidad de 70 o inferior no se muestran.  
  
 **Reducir la base de datos cuando se incremente por encima de**  
 Especifique el tamaño en megabytes que provoca la ejecución de esta tarea.  
  
 **Espacio disponible tras la reducción**  
 Detiene la reducción cuando el espacio disponible en los archivos de base de datos alcanza este tamaño.  
  
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
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] with [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Authentication.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication. Esta opción no está disponible.  
  
 **Nombre de usuario.**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Vea también  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
  
  

---
title: "Tarea Actualizar estadísticas (Plan de mantenimiento) | Microsoft Docs"
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
- sql13.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 774fe7654f9a67ae7e149b80b05e047ac958c10b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="update-statistics-task-maintenance-plan"></a>Tarea Actualizar estadísticas (Plan de mantenimiento)
  Utilice el cuadro de diálogo **Tarea Actualizar estadísticas** para actualizar la información de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre los datos de tablas e índices. Esta tarea vuelve a muestrear las estadísticas de distribución de cada índice creado en las tablas de usuario de la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza las estadísticas de distribución para optimizar la navegación de las tablas durante el procesamiento de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para generar automáticamente las estadísticas de distribución, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestrea periódicamente los datos de la tabla correspondiente para cada índice. Este tamaño de la muestra se basa en el número de filas de la tabla y en la frecuencia de modificación de los datos. Utilice esta opción para realizar un muestreo adicional con el porcentaje especificado de datos de las tablas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza esta información para crear planes de consultas mejores.  
  
 Esta tarea ejecuta la instrucción UPDATE STATISTICS.  
  
## <a name="options"></a>Opciones  
 **Conexión**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Bases de datos**  
 Especifique las bases de datos a las que afecta esta tarea.  
  
-   **Todas las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de tempdb.  
  
-   **Todas las bases de datos del sistema**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a excepción de tempdb. No se ejecutarán tareas de mantenimiento en las bases de datos creadas por usuarios.  
  
-   **Todas las bases de datos de usuario**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos creadas por usuarios. No se ejecutarán tareas de mantenimiento en las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Las bases de datos**  
  
     Genera un plan de mantenimiento que ejecuta tareas de mantenimiento únicamente en las bases de datos seleccionadas. Si elige esta opción, deberá seleccionar al menos una base de datos de la lista.  
  
 **Nota** Los planes de mantenimiento solo se pueden ejecutar en bases de datos con un nivel de compatibilidad de 80 o superior. Las bases de datos con un nivel de compatibilidad de 70 o inferior no se muestran.  
  
 **Objeto**  
 Limite la cuadrícula **Selección** para mostrar tablas, vistas o ambas cosas.  
  
 **Selección**  
 Especifique las tablas o índices que se ven afectados por esta tarea. No estará disponible cuando se seleccione **Tablas y vistas** en el cuadro Objeto.  
  
 **Todas las estadísticas existentes**  
 Actualiza las estadísticas tanto de las columnas como de los índices.  
  
 **Solo estadísticas de columna**  
 Solo actualiza las estadísticas de las columnas.  
  
 **Solo estadísticas de índice**  
 Solo actualiza las estadísticas de los índices.  
  
 **Tipo de recorrido**  
 Tipo de recorrido usado para obtener estadísticas actualizadas.  
  
 **Recorrido completo**  
 Lee todas las filas de la tabla o vista para obtener las estadísticas.  
  
 **Muestrear por**  
 Especifica el porcentaje de la tabla o vista indizada, o el número de filas del que se tomarán muestras cuando se recopilen las estadísticas de tablas o vistas de gran tamaño.  
  
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
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  


---
title: "Función clasificadora del regulador de recursos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: resource-governor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a47914e36079c04040e1ccc23228278396154fbe
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="resource-governor-classifier-function"></a>Función clasificadora del regulador de recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] El proceso de clasificación del regulador de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna las sesiones de entrada a un grupo de carga de trabajo según las características de la sesión. Puede adaptar la lógica de clasificación escribiendo una función definida por el usuario, denominada función clasificadora.  
  
## <a name="classification"></a>Clasificación  
 El regulador de recursos admite la clasificación de sesiones de entrada. La clasificación se basa en un conjunto de criterios escritos por el usuario contenidos en una función. Los resultados de la lógica de la función permiten al regulador de recursos clasificar las sesiones en los grupos de cargas de trabajo existentes.  
  
> [!NOTE]  
>  El grupo de cargas de trabajo interno se rellena con las solicitudes que solo son para uso interno. No se pueden cambiar los criterios que se usan para enrutar estas solicitudes y no se pueden clasificar las solicitudes en el grupo de cargas de trabajo interno.  
  
 Puede escribir una función escalar que contenga la lógica que se utiliza para asignar las sesiones entrantes a un grupo de cargas de trabajo. Para poder ejecutar esta función, debe completar las acciones siguientes:  
  
-   Crear y registrar la función utilizando la instrucción ALTER RESOURCE GOVERNOR. Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
-   Actualizar la configuración del regulador de recursos utilizando la instrucción ALTER RESOURCE GOVERNOR con el parámetro RECONFIGURE.  
  
 Después de crear la función y aplicar los cambios de configuración, el clasificador del regulador de recursos utilizará el nombre del grupo de cargas de trabajo devuelto por la función para enviar una nueva solicitud al grupo de cargas de trabajo adecuado.  
  
> [!IMPORTANT]  
>  La sesión del cliente puede expirar si la función de clasificación no se completa dentro del tiempo de espera especificado para el inicio de sesión. El tiempo de espera de inicio de sesión es una propiedad del cliente y como a tal, el servidor no está al tanto de los tiempos de espera. Una función clasificadora que se ejecute durante un tiempo prolongado puede dejar al servidor con conexiones huérfanas durante largos períodos de tiempo. Es importante que cree funciones clasificadoras que finalicen su ejecución antes de que se acabe el tiempo de espera de la conexión.  
  
 La función definida por el usuario tiene las siguientes características y comportamientos:  
  
-   La función definida por el usuario se evalúa para cada nueva sesión, incluso cuando la agrupación de conexiones esté habilitada.  
  
-   La función definida por el usuario proporciona el contexto del grupo de cargas de trabajo para la sesión. Una vez determinada la pertenencia al grupo, la sesión se enlaza al grupo de cargas de trabajo durante la duración de la sesión.  
  
-   Si la función definida por el usuario devuelve NULL, predeterminado o el nombre de un grupo que no existe, la sesión recibirá el contexto del grupo de cargas de trabajo predeterminado. La sesión también recibe el contexto predeterminado si se produce un error en la función por cualquier motivo.  
  
-   La función se debería definir con ámbito del servidor (base de datos maestra).  
  
-   La designación de la función clasificadora definida por el usuario solo surte efecto después de ejecutar ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Solo se puede definir una función definida por el usuario como clasificador a la vez.  
  
-   La función del clasificador definida por el usuario no se puede eliminar o modificar a menos que se quite su estado de clasificador.  
  
-   Con la ausencia de una función del clasificador definida por el usuario, todas las sesiones se clasifican en el grupo predeterminado.  
  
-   El grupo de cargas de trabajo devuelto por la función clasificadora está fuera del ámbito de la restricción del enlace de esquema. Por ejemplo, no puede quitar una tabla, pero puede quitar un grupo de cargas de trabajo.  
  
> [!IMPORTANT]  
>  Se recomienda habilitar la conexión de administrador dedicada (DAC) en el servidor. La conexión de administrador dedicada no está sujeta a la clasificación del regulador de recursos y se puede utilizar para supervisar y solucionar problemas de una función clasificadora. Para obtener más información, vea [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Si no hay disponible una conexión de administrador dedicada para solucionar los problemas, la otra opción es reiniciar el sistema en modo de usuario único. Aunque el modo de usuario único no está sujeto a clasificación, no ofrece la capacidad de diagnosticar la clasificación del regulador de recursos mientras se ejecuta.  
  
### <a name="classification-process"></a>Proceso de clasificación  
 En el contexto del regulador de recursos, el proceso de inicio de sesión para una sesión consta de los pasos siguientes:  
  
1.  Autenticación del inicio de sesión  
  
2.  Ejecución del desencadenador LOGON  
  
3.  Clasificación  
  
 Cuando la clasificación se inicia, el regulador de recursos ejecuta la función clasificadora y utiliza el valor devuelto por la función para enviar solicitudes al grupo de cargas de trabajo adecuado.  
  
> [!NOTE]  
>  La información sobre la ejecución de la función clasificadora y sobre los desencadenadores LOGON se expone en [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) y [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
## <a name="classification-function-tasks"></a>Tareas de función de clasificación  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo crear y probar una función clasificadora definida por el usuario.|[Crear y probar una función clasificadora definida por el usuario](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Configurar el regulador de recursos utilizando una plantilla](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Ver las propiedades del regulador de recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  

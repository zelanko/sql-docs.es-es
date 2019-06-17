---
title: Registrar base de datos reflejada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbmmonitor.registermirroreddb.f1
ms.assetid: 6acd02b9-2311-49b0-a5f8-3852beecb4b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b5be7eb52d0aa8c0a94b1a4ff63493e7f641bdbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754460"
---
# <a name="register-mirrored-database"></a>Registrar base de datos reflejada
  Utilice este cuadro de diálogo para registrar una o varias bases de datos reflejadas en una instancia del servidor determinada, mediante la adición de las bases de datos al Monitor de creación de reflejo de la base de datos. Cuando se agrega una base de datos, el Monitor de creación de reflejo de la base de datos almacena localmente en caché información acerca de la base de datos, sus asociados y el método de conexión a éstos.  
  
> [!IMPORTANT]  
>  Si es miembro del rol fijo de servidor **sysadmin** en la instancia del servidor principal, pero no en la instancia del servidor reflejado, solo puede ver el estado en la instancia del servidor principal.  
  
 **Para utilizar SQL Server Management Studio a fin de supervisar la creación de reflejo de la base de datos**  
  
-   [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opciones  
 **Instancia del servidor**  
 Seleccione una instancia del servidor en la lista, que contiene instancias del servidor con las que el Monitor de creación de reflejo de la base de datos ya tiene una conexión almacenada, o bien haga clic en **Conectar**. Para especificar nuevas credenciales para una instancia del servidor de la lista, haga clic en **Conectar** y conéctese mediante las nuevas credenciales.  
  
> [!NOTE]  
>  Para registrar bases de datos en varias instancias del servidor, una vez terminada la búsqueda de una instancia del servidor en las bases de datos deseadas, haga clic en **Aplicar**y, luego, seleccione otra instancia del servidor.  
  
 **Conectar**  
 Para especificar nuevas credenciales para la instancia del servidor, haga clic en **Conectar** y conéctese mediante las nuevas credenciales. Al conectarse a una instancia del servidor, el Monitor de creación de reflejo de la base de datos muestra **Esperando datos**.  
  
 **Bases de datos reflejadas**  
 La cuadrícula **Bases de datos reflejadas** muestra las bases de datos reflejadas en la instancia del servidor.  
  
 La cuadrícula contiene las columnas siguientes:  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**Registrar**|Comprueba cada una de las bases de datos que desee registrar. Si se supervisa actualmente una base de datos, su casilla estará activada y permanecerá deshabilitada.<br /><br /> Nota: Para eliminar del Registro una base de datos, cierre el cuadro de diálogo **Registrar base de datos reflejada**, seleccione la base de datos en el árbol de navegación y seleccione **Eliminar del Registro** en el menú **Acción**.|  
|**Base de datos**|Nombre de una base de datos reflejada en la instancia del servidor seleccionada.|  
|**Rol actual**|Rol de creación de reflejo actual de la base de datos, ya sea principal o reflejada, en la instancia del servidor seleccionada.|  
|**Asociado (Conectar como)**|Nombre del asociado de conmutación por error de la base de datos. Se muestra entre paréntesis **Autenticación de Windows del usuario de consola** o **Autenticación de SQL Server de inicio de sesión '***\<nombre de inicio de sesión>***'** . Esta información de autenticación es la que se utiliza actualmente (si la instancia se ha agregado antes) o la que se utilizará en un futuro (si la instancia no se ha agregado al monitor).|  
  
 **Mostrar el cuadro de diálogo para administrar conexiones de instancia del servidor cuando haga clic en Aceptar**  
 De forma predeterminada, el Monitor de creación de reflejo de la base de datos utiliza las credenciales de autenticación de Windows para instancias del servidor asociado, cuyas credenciales no se han proporcionado con anterioridad. Habilite esta opción para cambiar las credenciales de una o varias instancias del servidor al terminar de registrar las bases de datos.  
  
 Si esta opción está habilitada, al hacer clic en **Aceptar**, se abre el cuadro de diálogo para **administrar conexiones de instancia del servidor** . En dicho diálogo, puede elegir una instancia del servidor para la que desee especificar credenciales del monitor, que usará al conectarse a un asociado de conmutación por error determinado.  
  
 Para editar credenciales para un asociado, localice su entrada en la cuadrícula **Instancias del servidor** y haga clic en **Editar** en la fila. Se abrirá el cuadro de diálogo **Conectar al servidor** para ese nombre de instancia del servidor, con los controles de credencial inicializados en el valor actual almacenado en caché. Cambie las credenciales según corresponda y haga clic en **Conectar**. Si las credenciales tienen privilegios suficientes, la columna **Conectar utilizando** se actualizará con las nuevas credenciales.  
  
 **Aplicar**  
 Haga clic en este botón para registrar las bases de datos seleccionadas (y guardar las credenciales para las instancias del servidor asociado) a la vez que se mantiene abierto el cuadro de diálogo.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de bases de datos &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
  

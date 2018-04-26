---
title: Administración de sesiones de eventos en el Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60be76424ca6933fd1eea87f8e0edef560a6b09c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>Administrar sesiones de eventos en el Explorador de objetos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  En este tema se describen las acciones que se pueden llevar a cabo en el **Explorador de objetos** que afectan a una sesión de eventos extendidos:  
  
-   Crear una sesión de eventos extendidos  
  
-   Iniciar o detener una sesión de eventos extendidos  
  
-   Exportar una sesión de eventos extendidos  
  
-   Importar una plantilla de sesión de eventos extendidos  
  
-   Editar una sesión de eventos extendidos  
  
-   Eliminar una sesión de eventos extendidos  
  
## <a name="create-an-extended-events-session"></a>Crear una sesión de eventos extendidos  
 Para obtener más información acerca de cómo crear una sesión de eventos extendidos, vea [Create an Extended Events Session](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74).  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>Iniciar o detener una sesión de eventos extendidos  
 Puede iniciar o detener una sesión de eventos extendidos mediante el **Editor de consultas** usando la instrucción **ALTER EVENT SESSION** o usando el nodo **Eventos extendidos** del **Explorador de objetos**.  
  
 Cuando se detiene una sesión de eventos, la sesión ya no se muestra como una sesión activa en la vista de administración dinámica (DMV) sys.dm_xe_sessions. Sin embargo, la definición de la sesión permanece intacta y se puede reiniciar la sesión. Para quitar completamente la definición de una sesión, se debe eliminar la sesión.  
  
 Para iniciar o detener una sesión de eventos extendidos, debe disponer del permiso ALTER ANY EVENT SESSION.  
  
 Cuando se detiene una sesión que usa un destino en memoria, como los destinos de búfer en anillo, de creación de depósitos, de emparejamiento de eventos o de contador de eventos sincrónicos, se pierde toda la información almacenada en el búfer de la sesión (la columna target_data de la DMV sys.dm_xe_session_targets). Para obtener acceso a los datos de evento después de detener la sesión, debe guardar los datos antes de detener o configurar la sesión para que se utilice el destino de archivo.  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>Iniciar o detener una sesión de eventos extendidos mediante el Editor de consultas  
 Para iniciar una sesión, emita las instrucciones siguientes, reemplazando *nombre_sesión* por el nombre de la sesión de eventos extendidos:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 Para detener una sesión, emita las instrucciones siguientes, reemplazando *nombre_sesión* por el nombre de la sesión de eventos extendidos:  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>Iniciar o detener una sesión de eventos extendidos en el Explorador de objetos  
 Para iniciar o detener una sesión de eventos extendidos en el **Explorador de objetos**, expanda los nodos **Administración**, **Eventos extendidos**y **Sesiones** y, a continuación, haga clic con el botón secundario en una sesión y en **Iniciar sesión** o **Detener sesión**.  
  
## <a name="export-an-extended-events-session-template"></a>Exportar una plantilla de sesión de eventos extendidos  
 Puede exportar una sesión de eventos extendidos con el **Explorador de objetos**y guardarlos en un archivo de plantilla .xml. Por ejemplo, puede exportar una sesión y, a continuación, aplicar la plantilla a una nueva sesión de evento mediante el **Asistente para nueva sesión** o el cuadro de diálogo **Nueva sesión** .  
  
 Al exportar una sesión, asegúrese de que guarda el archivo de plantilla en una ubicación que usa el sistema de archivos NTFS y que restringe el acceso a los usuarios que están autorizados para ver la información.  
  
 Para exportar una sesión de eventos extendidos en el **Explorador de objetos**:  
  
1.  Expanda los nodos de **Administración**, **Eventos extendidos**y **Sesiones** .  
  
2.  Haga clic con el botón derecho en la sesión que quiere exportar y seleccione **Exportar sesión**.  
  
3.  En el cuadro de diálogo **Guardar como** , seleccione una ubicación para guardar el archivo, escriba el nombre de archivo en el cuadro **Nombre de archivo** y, a continuación, haga clic en **Guardar**.  
  
     Si guarda el archivo en la ubicación predeterminada de la plantilla de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , la plantilla aparecerá en la lista desplegable de plantillas predefinidas cuando use el cuadro de diálogo **Asistente para nueva sesión** y **Nueva sesión** .  
  
## <a name="import-an-extended-events-session-template"></a>Importar una plantilla de sesión de eventos extendidos  
 Mediante el **Explorador de objetos**, puede importar una plantilla para una sesión de eventos extendidos. Por ejemplo, puede que desee realizar esta operación para crear una sesión de una plantilla que se exportó desde otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para importar una sesión de eventos extendidos, debe tener los permisos necesarios para **ALTER ANY EVENT SESSION** .  
  
 Antes de importar un archivo de plantilla, asegúrese de que el archivo procede de un origen de confianza. Los archivos de plantilla deben guardarse en una ubicación que use el sistema de archivos NTFS y donde el acceso está restringido a los usuarios que estén autorizados para ver la información.  
  
 Para importar una sesión de eventos extendidos:  
  
1.  En el **Explorador de objetos**, expanda los nodos **Administración**y después **Eventos extendidos** .  
  
2.  Haga clic con el botón derecho en **Sesiones** y seleccione **Nueva sesión**.  
  
3.  Especifica un nombre para la sesión.  
  
4.  Expanda la lista desplegable **Plantilla** .  
  
5.  Haga clic en **\<File From … (Archivo de …) >Abrir** y busque la sesión (archivo XML) que quiere importar.  
  
 La sesión aparecen bajo el nodo **Sesiones** . De forma predeterminada, no se inicia la sesión.  
  
## <a name="edit-an-extended-events-session"></a>Editar una sesión de eventos extendidos  
 Puede modificar una sesión de eventos extendidos en el Explorador de objetos.  
  
 Para editar una sesión de eventos extendidos:  
  
1.  En el **Explorador de objetos**, expanda los nodos **Administración**, **Eventos extendidos**y **Sesiones** .  
  
2.  Haga clic con el botón derecho en una sesión y seleccione **Propiedades**.  
  
3.  En la sección **Seleccionar una página** , seleccione la página o las páginas que desee editar.  
  
4.  Después de finalizar la revisión de la sesión de evento, haga clic en **Aceptar**.  
  
## <a name="script-an-event-session-definition-using-includetsqlincludestsql-mdmd"></a>Crear un script para una definición de la sesión de eventos mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 Tanto el Asistente para nueva sesión como el cuadro de diálogo Nueva sesión tienen una opción de script que genera [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir la sesión de eventos extendidos.  
  
 Puede tener acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] para una sesión de eventos extendidos existente haciendo clic con el botón secundario en el nombre de la sesión, seleccionando **Incluir sesión como**y después seleccionando **Crear para**.  
  
## <a name="delete-an-extended-events-session"></a>Eliminar una sesión de eventos extendidos  
 Puede eliminar una sesión de eventos extendidos:  
  
-   En el Editor de consultas mediante **DROP EVENT SESSION**.  
  
-   En el **Explorador de objetos**.  
  
 Cuando se elimina una sesión de eventos, se quita toda la información de configuración y la definición de la sesión ya no aparece en la vista de catálogo sys.server_event_sessions.  
  
> [!NOTE]  
>  system_health y Always On_health se incluyen con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no los elimine. system_health está habilitado de forma predeterminada (para obtener más información, vea [Usar la sesión system_health](../../relational-databases/extended-events/use-the-system-health-session.md)). Always On_health está desactivado de forma predeterminada. Estas sesiones recopilan los datos que pueden ser útiles para diagnosticar problemas de rendimiento.  
  
 Para eliminar una sesión de eventos extendidos, debe disponer del permiso ALTER ANY EVENT SESSION.  
  
 Para eliminar una sesión de eventos extendidos en el **Explorador de objetos**:  
  
1.  Expanda los nodos de **Administración**, **Eventos extendidos**y **Sesiones** .  
  
2.  Haga clic con el botón derecho en la sesión y seleccione **Eliminar**.  
  
3.  En el cuadro de diálogo **Eliminar objeto** , haga clic en **Aceptar**.  
  
4.  Después de finalizar la revisión de la sesión de evento, haga clic en **Aceptar**.  
  
 Para eliminar una sesión de eventos extendidos en el **Editor de consultas**, emita las instrucciones siguientes, reemplazando *nombre_sesión* por el nombre de la sesión de eventos extendidos que quiere eliminar:  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
  

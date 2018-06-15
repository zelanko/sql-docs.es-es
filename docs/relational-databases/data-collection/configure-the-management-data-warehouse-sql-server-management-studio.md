---
title: Configuración del almacén de administración de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48225263d322b901baa87084b47bedaf36fcc601
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33145206"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>Configurar el almacén de administración de datos (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo configurar el almacén de administración de datos para admitir el almacenamiento de datos en una o varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utilizan el recopilador de datos. Estas instancias pueden estar en el mismo servidor o en servidores diferentes. También se proporcionan descripciones de la interfaz de usuario del cuadro de diálogo [Asistente para configurar el almacén de administración de datos](#Wizard) . Para obtener información acerca de cómo configurar un recopilador de datos, vea [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md).  
  
> [!NOTE]  
>  Si se configura el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se ejecute mediante una de las cuentas de servicio del sistema (sistema local, servicio de red o servicio local) y el almacén de administración de datos se crea en una instancia diferente del recopilador de datos, debe configurar los conjuntos de recopilación para que utilicen un proxy para cargar los datos en el almacén de administración de datos.  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>Configurar el almacén de administración de datos en una o varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Asegúrese de que el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se esté ejecutando.  
  
2.  En el Explorador de objetos, expanda el nodo **Administración** .  
  
3.  Haga clic con el botón derecho en **Recopilación de datos**, expanda **Tareas**y haga clic en **Configurar almacén de administración de datos**.  
  
4.  Use el [Asistente para configurar el almacén de administración de datos](#Wizard) para crear un almacén de administración de datos, configurar inicios de sesión, habilitar la recopilación de datos e iniciar **Conjuntos de recopilación de datos del sistema**.  
  
     Para configurar varias instancias, continúe con el paso 5.  
  
    > [!NOTE]  
    >  Se recomienda utilizar servidores proxy en las implementaciones en que el recopilador de datos está instalado en varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utilizan el mismo almacén de administración de datos.  
  
5.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en otra instancia y realice una de las acciones siguientes:  
  
    -   Use el Asistente para configurar el almacén de administración de datos a fin de configurar la recopilación de datos para el almacén de administración de datos existente.  
  
    -   Haga clic con el botón derecho en **Recopilación de datos**y luego haga clic en **Propiedades**. En la pestaña **General** , especifique el almacén de administración de datos existente y el servidor en que está instalado.  
  
6.  Repita el paso 5 hasta que todas las instancias de base de datos que utilizan el recopilador de datos estén configuradas para cargar datos en el almacén de administración de datos compartido.  
  
####  <a name="Wizard"></a> Asistente para configurar el almacén de administración de datos  
 **Página Asistente**  
  
 La página de bienvenida es la página de inicio del Asistente para configurar la recopilación de datos. El usuario decide si desea que se muestre.  
  
 **No volver a mostrar esta página.**  
 Seleccione esta opción para suprimir esta página la próxima vez que ejecute el Asistente para configurar la recopilación de datos.  
  
 **Página Configurar almacenamiento del almacén de administración de datos**  
  
 Utilice esta página para seleccionar un servidor de bases de datos y un almacén de administración de datos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El almacén de administración de datos es una base de datos relacional que almacenará los datos recopilados.  
  
> [!NOTE]  
>  Debe tener el nivel de permisos adecuado para crear el almacén de administración de datos en el servidor. Para obtener más información, vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). También debe tener el nivel de permisos adecuado para crear inicios de sesión para los roles del almacén de administración de datos.  
  
 **Nombre del servidor**  
 Especifica el nombre del servidor que hospedará el almacén de administración de datos.  
  
 Al configurar un almacén de administración de datos, **Nombre del servidor** es siempre el nombre del servidor local y no se puede modificar.  
  
 **Nombre de la base de datos**  
 Especifica la base de datos relacional que almacenará los datos recopilados. Utilice la lista para seleccionar una base de datos existente o haga clic en **Nueva** para crear una nueva base de datos mediante el cuadro de diálogo **Nueva base de datos** .  
  
 La opción **Nueva** solo está disponible al configurar un conjunto de recopilación de datos.  
  
 **Página Asignar inicios de sesión y usuarios**  
  
 Utilice esta página para asignar inicios de sesión a roles de usuario de base de datos para el almacén de administración de datos.  
  
 **Usuarios asignados a este inicio de sesión**  
 Muestra los inicios de sesión existentes en el servidor que hospedará el almacén de administración de datos. Cada fila contiene una casilla **Asignar** modificable, un nombre de **Inicio de sesión** y un **Tipo** de inicio de sesión.  
  
 Especifique un inicio de sesión activando la casilla **Asignar** para el inicio de sesión.  
  
 **Miembros del rol de base de datos para:** *\<nombre del almacenamiento de datos>*  
 Seleccione el rol del almacén de administración de datos al que se ha asignado el inicio de sesión haciendo clic en la casilla correspondiente a una o varias de las opciones siguientes:  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **Nuevo inicio de sesión**  
 Abra el cuadro de diálogo **Inicio de sesión - Nuevo** y cree un nuevo inicio de sesión para el almacén de administración de datos.  
  
 **Página Finalización del asistente**  
  
 Utilice esta página para comprobar y completar la configuración de la recopilación de datos. El árbol mostrado en la ventana de vista muestra las configuraciones que se aplicarán, así como las acciones que tendrán lugar al hacer clic en **Finalizar**.  
  
 **Página Progreso del Asistente para configurar la recopilación de datos**  
  
 Utilice esta página para ver los resultados de cada paso de configuración.  
  
 **Detalles**  
 Muestra cada paso de configuración como una fila en la cuadrícula **Detalles** . Cada fila contiene una columna **Acción** que describe el paso y una columna **Estado** que indica si el paso se ha realizado correctamente o no. Si hay un error, aparece un mensaje en la columna **Mensaje** .  
  
 **Detener**  
 Detiene el procesamiento del asistente.  
  
 **Informe**  
 Muestra un informe de la configuración de la recopilación de datos. Se proporcionan las opciones de informe siguientes:  
  
-   Ver informe  
  
-   Guardar informe en archivo  
  
-   Copiar informe al Portapapeles  
  
-   Enviar informe como correo electrónico  
  
 **Cerrar**  
 Cierra el asistente.  
  
## <a name="see-also"></a>Ver también  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Administrar la recopilación de datos](../../relational-databases/data-collection/manage-data-collection.md)  
  
  

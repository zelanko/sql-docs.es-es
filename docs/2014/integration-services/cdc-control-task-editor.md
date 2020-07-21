---
title: Editor de la tarea control CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 35d20d475b8f6da9c899c389419233f8e90bf555
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439022"
---
# <a name="cdc-control-task-editor"></a>Editor de la tarea Control de CDC
  Use el cuadro de diálogo **Editor de la tarea Control CDC** para configurar la tarea Control CDC. La configuración de la tarea Control CDC incluye la definición de una conexión a la base de datos CDC, la operación de tarea CDC y la información sobre la administración de estados.  
  
 Para obtener más información acerca de la tarea Control CDC, vea [CDC Control Task](control-flow/cdc-control-task.md).  
  
 **Para abrir el Editor de la tarea Control CDC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete de [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene la tarea Control CDC.  
  
2.  En la pestaña **Flujo de control** , haga doble clic en la tarea Control CDC.  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de ADO.NET para la base de datos CDC de SQL Server**  
 Seleccione un administrador de conexiones existente de la lista o haga clic en **Nueva** para crear una nueva conexión. Es preciso realizar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] habilitada para CDC y donde se encuentre la tabla de cambios seleccionada.  
  
 **Operación de Control CDC**  
 Seleccione la operación que vaya a ejecutar para esta tarea. Todas las operaciones usan la variable de estado que se almacena en una variable de paquete SSIS donde se almacena el estado y lo pasa entre los distintos componentes del paquete.  
  
-   **Marcar comienzo de carga inicial**: esta operación se usa cuando se ejecuta una carga inicial desde una base de datos activa sin una instantánea. Se invoca al comienzo de un paquete de carga inicial para registrar el LSN actual en la base de datos de origen antes de que el paquete de carga inicial comience a leer las tablas de origen. Esto requiere una conexión a la base de datos de origen.  
  
     Si selecciona **Mark Initial Load Start** (Marcar comienzo de carga inicial) cuando trabaja en CDC de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser  **db_owner** o **sysadmin**.  
  
-   **Marcar final de carga inicial**: esta operación se usa al ejecutar una carga inicial desde una base de datos activa sin una instantánea. Se invoca al final de un paquete de carga inicial para registrar el LSN actual en la base de datos de origen después de que el paquete de carga inicial termine de leer las tablas de origen. Este LSN se determina mediante el registro de la hora en el momento en que se produjo esta operación y, posteriormente, mediante consulta a la tabla de asignación de `cdc.lsn_time_`de la base de datos CDC en busca de un cambio que hubiera tenido lugar después de dicha hora.  
  
     Si selecciona **Mark Initial Load End** (Marcar final de carga inicial) cuando trabaja en CDC de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser  **db_owner** o **sysadmin**.  
  
-   **Marcar comienzo de CDC**: esta operación se utiliza cuando la carga inicial se realiza desde una base de datos de base de datos de instantánea o desde una base de datos de inactividad. Se invoca en cualquier punto del paquete de carga inicial. La operación acepta un parámetro que puede ser un LSN de instantánea, un nombre de una base de datos de instantánea (desde la que el LSN de instantánea se deriva automáticamente) o se puede dejar vacío, en cuyo caso el LSN de la base de datos actual se usa como el LSN de inicio para el paquete de procesamiento de cambios.  
  
     Esta operación se usa en lugar de las operaciones Marcar comienzo/final de carga inicial.  
  
     Si selecciona **Mark CDC Start** (Marcar comienzo de CDC) cuando trabaja en CDC de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser  **db_owner** o **sysadmin**.  
  
-   **Obtener intervalo de procesamiento**: esta operación se usa en un paquete de procesamiento de cambios antes de invocar el flujo de datos que usa el flujo de datos de origen de CDC. Establece un intervalo de LSN que lee el flujo de datos de origen de CDC cuando se invoca. El intervalo se almacena en una variable de paquete SSIS que usa el origen de CDC durante el procesamiento del flujo de datos.  
  
     Para obtener más información sobre los posibles estados CDC que se almacenan, vea [Definir una variable de estado](data-flow/define-a-state-variable.md).  
  
-   **Marcar intervalo procesado**: esta operación se usa en un paquete de procesamiento de cambios al final de una ejecución CDC (después de que el flujo de datos CDC se complete correctamente) para registrar el último LSN que se haya procesado totalmente en la ejecución CDC. La próxima vez que se ejecute `GetProcessingRange` , esta posición determinará el inicio del siguiente intervalo de procesamiento.  
  
-   **Restablecer estado CDC**: esta operación se usa para restablecer el estado CDC persistente asociado al contexto CDC actual. Después de ejecutar esta operación, el LSN máximo actual de la tabla de `sys.fn_cdc_get_max_lsn` de la marca de tiempo de LSN se convierte en el inicio del intervalo para el siguiente intervalo de procesamiento. Esta operación requiere una conexión a la base de datos de origen.  
  
     Un ejemplo de uso de esta operación es cuando se desea procesar solo los registros de cambios creados recientemente y omitir todos los registros de cambios anteriores.  
  
 **Variable que contiene el estado CDC**  
 Seleccione la variable del paquete SSIS que almacena la información sobre el estado de la operación de la tarea. Debe definir una variable antes de empezar. Si selecciona **Persistencia de estado automática**, la variable de estado se carga y guarda automáticamente.  
  
 Para obtener más información sobre cómo se define la variable de estado, vea [Definir una variable de estado](data-flow/define-a-state-variable.md).  
  
 **LSN de SQL Server para iniciar el nombre de CDC/instantánea:**  
 Especifique el LSN de la base de datos de origen actual o el nombre de la base de datos de instantánea de la carga inicial desde donde se realizará la carga inicial con el fin de determinar dónde se inicia CDC. Esto solo está disponible si se establece **Operación de Control CDC** en **Marcar comienzo de CDC**.  
  
 Para obtener más información acerca de estas operaciones, vea [CDC Control Task](control-flow/cdc-control-task.md).  
  
 **Almacenar automáticamente el estado en una tabla de base de datos**  
 Active esta casilla para que la tarea Control CDC controle automáticamente la carga y el almacenamiento del estado de CDC en una tabla de estado que se encuentre en una base de datos especificada. Si no se ha activado, el desarrollador debe cargar el estado de CDC cuando el paquete se inicie y guardarlo cada vez que cambie el estado de CDC.  
  
 **Administrador de conexiones para la base de datos donde se almacena el estado**  
 Seleccione un administrador de conexiones de ADO.NET existente de la lista o haga clic en Nueva para crear una nueva conexión. Esta conexión es a una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contenga la tabla de estado. La tabla de estado contiene la información sobre el estado.  
  
 Esto solo está disponible si se ha seleccionado **Persistencia de estado automática** y es un parámetro obligatorio.  
  
 **Tabla que se va a usar para almacenar el estado**  
 Escriba el nombre de la tabla de estado que se va a usar para almacenar el estado de CDC. La tabla especificada debe tener dos columnas denominadas **nombre** y **estado** y ambas columnas deben ser del tipo de datos **varchar (256)**.  
  
 Opcionalmente, puede seleccionar **Nueva** para obtener un script SQL que cree una nueva tabla de estado con las columnas necesarias. Cuando se selecciona **Persistencia de estado automática** , el desarrollador debe crear una tabla de estado según los requisitos descritos anteriormente.  
  
 Esto solo está disponible si se ha seleccionado **Persistencia de estado automática** y es un parámetro obligatorio.  
  
 **Nombre del estado**  
 Escriba un nombre para asociar al estado CDC persistente. Los paquetes de carga completa y CDC que funcionan con el mismo contexto CDC especificarán un nombre común para el estado. Este nombre se usa para buscar la fila de estado en la tabla de estado.  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades personalizadas de la tarea de control CDC](control-flow/cdc-control-task-custom-properties.md)  
  
  

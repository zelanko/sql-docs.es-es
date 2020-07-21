---
title: Tarea Control CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb3d85e8617e3e2e84ea205d6c47bd3422a0ce7f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433782"
---
# <a name="cdc-control-task"></a>Tarea Control CDC
  La tarea Control CDC se usa para controlar el ciclo de vida de los paquetes de captura de datos modificados (CDC). Controla la sincronización de paquetes CDC con el paquete de carga inicial, la administración de los intervalos de número de secuencia de registro (LSN) que se procesan en una ejecución de un paquete CDC. Además, la tarea Control CDC se ocupa de los escenarios de error y de la recuperación.  
  
 La tarea Control CDC mantiene el estado del paquete CDC en una variable de paquete SSIS y también puede conservarlo en una tabla de base de datos para mantener el estado a través de las activaciones de paquete y entre varios paquetes que realizan conjuntamente un proceso CDC común (por ejemplo, una tarea puede ser responsable de la carga inicial y otro de las actualizaciones de fuente de generación).  
  
 La tarea Control CDC admite dos grupos de operaciones. Un grupo controla la sincronización del procesamiento de los cambios y la carga inicial y el otro administra el intervalo de procesamiento de los cambios de los LSN para una ejecución de un paquete CDC y realiza el seguimiento de lo que se procesó correctamente.  
  
 Las siguientes operaciones controlan la sincronización de la carga inicial y el procesamiento de cambios:  
  
|Operación|Descripción|  
|---------------|-----------------|  
|ResetCdcState|Esta operación se usa para restablecer el estado CDC persistente asociado al contexto CDC actual. Después de ejecutar esta operación, el LSN máximo actual de la tabla de `sys.fn_cdc_get_max_lsn` de la marca de tiempo de LSN se convierte en el inicio del intervalo para el siguiente intervalo de procesamiento. Esta operación requiere una conexión a la base de datos de origen.|  
|MarkInitialLoadStart|Esta operación se usa al comienzo de un paquete de carga inicial para registrar el LSN actual en la base de datos de origen antes de que el paquete de carga inicial comience a leer las tablas de origen. Esto requiere una conexión a la base de datos de origen para llamar a `sys.fn_cdc_get_max_lsn`.<br /><br /> Si selecciona MarkInitialLoadStart cuando trabaja en CDC de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser db_owner o sysadmin.|  
|MarkInitialLoadEnd|Esta operación se usa al final de un paquete de carga inicial para registrar el LSN actual en la base de datos de origen después de que el paquete de carga inicial termine de leer las tablas de origen. Este LSN se determina mediante el registro de la hora en el momento en que se produjo esta operación y, posteriormente, mediante consulta a la tabla de asignación de `cdc.lsn_time_`de la base de datos CDC en busca de un cambio que hubiera tenido lugar después de dicha hora.<br /><br /> Si selecciona MarkInitialLoadEnd cuando trabaja en CDC de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser db_owner o sysadmin.|  
|MarkCdcStart|Esta operación se usa cuando la carga inicial se realiza desde una base de datos de instantáneas. En este caso, el procesamiento de cambios debe iniciarse inmediatamente después del LSN de la instantánea. Puede especificar el nombre de la base de datos de instantáneas que se usará y la tarea Control CDC consulta a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el LSN de la instantánea. También tiene la opción de especificar directamente el LSN de la instantánea<br /><br /> Si selecciona MarkCdcStart cuando trabaja en CDC de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (es decir, no en Oracle), el usuario especificado en el administrador de conexiones debe ser db_owner o sysadmin.|  
  
 Las operaciones siguientes se usan para administrar el intervalo de procesamiento:  
  
|Operación|Descripción|  
|---------------|-----------------|  
|GetProcessingRange|Esta operación se usa antes de invocar el flujo de datos que usa el flujo de datos origen de CDC. Establece un intervalo de LSN que lee el flujo de datos de origen de CDC cuando se invoca. El intervalo se almacena en una variable de paquete SSIS que usa el origen de CDC durante el procesamiento del flujo de datos.<br /><br /> Para obtener más información sobre los estados que se almacenan, vea [Definir una variable de estado](../data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|: esta operación se ejecuta después de cada ejecución de CDC (después de que el flujo de datos de CDC se completa correctamente) para registrar el último LSN que se ha procesado totalmente en la ejecución de CDC. La próxima vez que se ejecute GetProcessingRange, esta posición será el inicio del intervalo de procesamiento.|  
  
## <a name="handling-cdc-state-persistency"></a>Controlar la persistencia de estado CDC  
 La tarea Control CDC mantiene un estado persistente entre las activaciones. La información almacenada en el estado CDC se usa para determinar y mantener el intervalo de procesamiento del paquete CDC y para detectar condiciones de error. El estado persistente se almacena como una cadena. Para obtener más información, consulte [Definir una variable de estado](../data-flow/define-a-state-variable.md).  
  
 La tarea Control CDC admite dos tipos de persistencia de estado  
  
-   Persistencia de estado manual: en este caso, la tarea Control CDC administra el estado almacenado en una variable de paquete pero el desarrollador del paquete debe leer la variable desde un almacén persistente antes de llamar al Control CDC y después escribirla de nuevo en el almacén persistente cuando el Control CDC se llame por última vez y la ejecución del CDC se complete.  
  
-   Persistencia de estado automática: el estado del CDC se almacena en una tabla de una base de datos. El estado se almacena con un nombre proporcionado en la propiedad **StateName** en una tabla denominada en la propiedad **Tabla para Storing State** , que se encuentra en un administrador de conexiones seleccionado para almacenar el estado. El valor predeterminado es el administrador de conexiones de origen pero la práctica común es que sea el administrador de conexiones de destino. La tarea Control CDC actualiza el valor de estado en la tabla de estados y esta se confirma como parte de la transacción ambiente.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 La tarea Control CDC puede notificar un error cuando:  
  
-   No se puede leer el estado CDC persistente o cuando la actualización del estado persistente da error.  
  
-   No puede leer la información del LSN actual desde la base de datos de origen.  
  
-   Lectura del estado CDC no es coherente.  
  
 En todos estos casos, la tarea Control CDC notifica un error que se puede controlar igual que SSIS controla los errores de flujo de control.  
  
 La tarea Control CDC también puede notificar una advertencia cuando la operación del intervalo de procesamiento Get se invoca directamente después de otra operación de intervalo de procesamiento Get sin llamar a Marcar intervalo de procesamiento. Esta es una indicación de que la ejecución anterior dio error o de que otro paquete CDC puede estar ejecutándose con el mismo nombre del estado CDC.  
  
## <a name="configuring-the-cdc-control-task"></a>Configurar la tarea Control CDC  
 Puede establecer propiedades a través del Diseñador de SSIS o mediante programación.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Editor de la tarea Control de CDC](../cdc-control-task-editor.md)  
  
-   [Propiedades personalizadas de la tarea de control CDC](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir una variable de estado](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico [Instalar la captura de datos modificados Microsoft SQL Server 2012 para Oracle de Attunity](https://go.microsoft.com/fwlink/?LinkId=252958), en social.technet.microsoft.com.  
  
-   Artículo técnico [Solucionar problemas de configuración de la captura de datos modificados de Microsoft para Oracle de Attunity](https://go.microsoft.com/fwlink/?LinkId=252960), en social.technet.microsoft.com.  
  
-   Artículo técnico [Solucionar problemas de errores de instancias de CDC de la captura de datos modificados de Microsoft para Oracle de Attunity](https://go.microsoft.com/fwlink/?LinkId=252961), en social.technet.microsoft.com.  
  
  

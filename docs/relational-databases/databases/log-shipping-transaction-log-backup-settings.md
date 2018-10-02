---
title: Configuración de copias de seguridad de trasvase de registros de transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 880dbc43daf8e236f1e424968b5ec4ff9d8b0107
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642063"
---
# <a name="log-shipping-transaction-log-backup-settings"></a>Configuración de copias de seguridad de trasvase de registros de transacciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice este cuadro de diálogo para configurar y modificar los parámetros de copia de seguridad de registros de transacciones para una configuración de trasvase de registros.  
  
 Para obtener una explicación de los conceptos relacionados con el trasvase de registros, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opciones  
 **Ruta de red a esta carpeta de copia de seguridad**  
 Escriba en este cuadro el recurso compartido de red para la carpeta de copia de seguridad. La carpeta local donde se guardan las copias de seguridad de registros de transacciones deben estar compartidas, de forma que los trabajos de copia del trasvase de registros puedan copiar estos archivos en el servidor secundario. Debe conceder permisos de lectura para este recurso compartido de red a la cuenta de proxy con la que se ejecuta el trabajo de copia en la instancia del servidor secundario. De forma predeterminada, ésta es la cuenta de servicio SQLServerAgent de la instancia del servidor secundario; el administrador puede elegir otra cuenta de proxy para el trabajo.  
  
 **Si la carpeta de copia de seguridad se encuentra en el servidor principal, escriba la ruta de acceso local a la carpeta.**  
 Escriba la letra de unidad local y la ruta de acceso a la carpeta de copia de seguridad si ésta se encuentra en el servidor principal. Si la carpeta no se encuentra en el servidor principal, puede dejar este campo en blanco.  
  
 Si especifica una ruta de acceso local, el comando BACKUP utilizará esta ruta para crear las copias de seguridad de registros de transacciones; si no se especifica una ruta local, el comando utilizará la ruta de acceso de red especificada en el cuadro **Ruta de red a esta carpeta de copia de seguridad** .  
  
> [!NOTE]  
>  Si la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta con la cuenta local del sistema en el servidor principal, debe crear la carpeta de copia de seguridad en el servidor principal y especificar la ruta de acceso local a esta carpeta. La cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la instancia del servidor principal debe contar con permisos de lectura/escritura en esta carpeta.  
  
 **Eliminar archivos con más de**  
 Especifique el tiempo que deben permanecer en el directorio de copia de seguridad las copias de seguridad de registros de transacciones antes de ser eliminadas.  
  
 **Mostrar una alerta si no se produce una copia de seguridad tras**  
 Especifique el tiempo que el trasvase de registros debe esperar antes de mostrar una alerta para indicar que no se han producido copias de seguridad de registros de transacciones.  
  
 **Nombre del trabajo**  
 Muestra el nombre del trabajo del Agente SQL Server utilizado para crear las copias de seguridad de registros de transacciones para el trasvase de registros. Cuando crea el trabajo, puede escribir en el cuadro para modificar el nombre.  
  
 **Programación**  
 Muestra la programación actual para hacer una copia de seguridad de los registros de transacciones de la base de datos principal. Antes de crear el trabajo de copia de seguridad, puede modificar esta programación si hace clic en el botón **Programar...**. Después de crear el trabajo, puede modificar esta programación si hace clic en el botón **Editar trabajo...**.  
  
### <a name="backup-job"></a>Trabajo de copia de seguridad  
 **Programar...**  
 Modifique la programación establecida durante la creación del trabajo del Agente SQL Server.  
  
 **Editar trabajo...**  
 Modifique los parámetros del trabajo del Agente SQL Server que realiza copias de seguridad de registros de transacciones en la base de datos principal.  
  
 **Deshabilitar este trabajo**  
 Impide que el trabajo del Agente SQL Server cree copias de seguridad de registros de transacciones.  
  
### <a name="compression"></a>Compresión  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o las versiones posteriores) admiten la [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Establecer la compresión de copia de seguridad**  
 En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o una versión posterior), seleccione uno de los valores de compresión de copia de seguridad siguientes para las copias de seguridad de registros de esta configuración de trasvase de registros:  
  
|||  
|-|-|  
|**Usar la configuración de servidor predeterminada**|Haga clic para utilizar el valor predeterminado de nivel de servidor.<br /><br /> La opción de la configuración del servidor **Compresión de copia de seguridad predeterminada** establece este valor predeterminado. Para obtener más información sobre cómo ver la configuración actual de esta opción, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Comprimir copia de seguridad**|Haga clic para comprimir la copia de seguridad, sin tener en cuenta el valor predeterminado de nivel de servidor.<br /><br /> **\*\* Importante \*\*** De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar negativamente a las operaciones simultáneas. Por tanto, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.|  
|**No comprimir copia de seguridad**|Haga clic para crear una copia de seguridad sin comprimir, independientemente del valor predeterminado de nivel de servidor.|  
  
## <a name="see-also"></a>Ver también  
 [Configurar un usuario para crear y administrar trabajos del Agente SQL Server](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  

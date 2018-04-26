---
title: Realizar copias de seguridad de la base de datos (página Opciones de copia de seguridad) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
caps.latest.revision: 62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17db454343bb9af8558db1f6c24f9073fc9ddf80
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="back-up-database-backup-options-page"></a>Copia de seguridad de la base de datos (página Opciones de copia de seguridad)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice la página  **Opciones de copia de seguridad** del cuadro de diálogo **Copia de seguridad de base de datos** para ver o modificar las opciones de copia de seguridad de la base de datos.  
  
 **Para crear una copia de seguridad mediante SQL Server Management Studio**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Puede definir un plan de mantenimiento de base de datos para crear copias de seguridad. Para obtener más información, vea [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md) y [Usar el Asistente para planes de mantenimiento](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Cuando especifica una tarea de copia de seguridad con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [BACKUP](../../t-sql/statements/backup-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente si hace clic en el botón **Script** y, después, selecciona un destino para el script.  
  
## <a name="options"></a>Opciones  
  
### <a name="backup-set"></a>Conjunto de copia de seguridad  
 Las opciones del panel **Conjunto de copia de seguridad** permiten especificar información adicional acerca del conjunto de copia de seguridad creado en la operación de copia de seguridad.  
  
 **Nombre**  
 Especifique el nombre del conjunto de copia de seguridad. El sistema sugiere automáticamente un nombre predeterminado basándose en el nombre de la base de datos y el tipo de copia de seguridad.  
  
 Para obtener más información sobre los conjuntos de copia de seguridad, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 **Descripción**  
 Escriba una descripción del conjunto de copia de seguridad.  
  
 **El conjunto de copia de seguridad expira**  
 Elija una de las siguientes opciones de expiración. Esta opción se deshabilita si la opción **Dirección URL** se elige como destino de la copia de seguridad.  
  
|||  
|-|-|  
|**Después**|Especifique el número de días que debe transcurrir antes de que el conjunto de copia de seguridad expire y se pueda sobrescribir. Este valor puede estar entre 0 y 99999 días; el valor 0 significa que el conjunto de copia de seguridad no expirará nunca.<br /><br /> El valor predeterminado para la expiración de la copia de seguridad es el valor configurado en la opción **Tiempo predeterminado de retención de medios de copia de seguridad (días)** . Para tener acceso a esta opción, haga clic con el botón derecho en el nombre del servidor en el Explorador de objetos y seleccione **Propiedades**; luego, haga clic en la página **Configuración de base de datos** del cuadro de diálogo **Propiedades del servidor** .|  
|**Activado**|Especifique una fecha determinada en la que el conjunto de copias de seguridad expire y se pueda sobrescribir.|  
  
### <a name="compression"></a>Compresión  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o las versiones posteriores) admiten la [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Establecer la compresión de copia de seguridad**  
 En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o en versiones posteriores), seleccione uno de los siguientes valores de compresión de copia de seguridad:  
  
|||  
|-|-|  
|**Usar la configuración de servidor predeterminada**|Haga clic para utilizar el valor predeterminado de nivel de servidor.<br /><br /> La opción de la configuración del servidor **Compresión de copia de seguridad predeterminada** establece este valor predeterminado. Para obtener más información sobre cómo ver la configuración actual de esta opción, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Comprimir copia de seguridad**|Haga clic para comprimir la copia de seguridad, sin tener en cuenta el valor predeterminado de nivel de servidor.<br /><br /> **\*\* Importante \*\*** De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar negativamente a las operaciones simultáneas. Por consiguiente, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.|  
|**No comprimir copia de seguridad**|Haga clic para crear una copia de seguridad sin comprimir, independientemente del valor predeterminado de nivel de servidor.|  
  
### <a name="encryption"></a>Cifrado  
 Para crear un archivo de copia de seguridad, active la casilla **Cifrar copia de seguridad** . Seleccione un algoritmo de cifrado para usar para el paso de cifrado y proporcione un certificado o clave asimétrica de una lista de los certificados existentes o de claves asimétricas. Los algoritmos disponibles para el cifrado son:  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
> [!TIP]  
>  La opción de cifrado se deshabilita si seleccionó anexar en un conjunto de copia de seguridad existente.  
>   
>  Es una práctica recomendada hacer copias de seguridad del certificado o las claves y almacenarlas en una ubicación diferente que la copia de seguridad que cifró.  
>   
>  Solo se admiten las claves que residen en Administración extensible de claves (EKM).  
  
## <a name="see-also"></a>Ver también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  

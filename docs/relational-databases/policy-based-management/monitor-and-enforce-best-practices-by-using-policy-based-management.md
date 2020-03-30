---
title: Procedimientos recomendados para la supervisión y aplicación mediante la administración basada en directivas
description: La administración basada en directivas proporciona un conjunto de archivos de directivas que puede importar como directivas de procedimientos recomendados y, después, evaluar las directivas con un conjunto de destinos que incluye instancias, objetos, bases de datos u objetos de base de datos.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54fdfe36da0d590fa2225ab7cc99af640727b000
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75557704"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La administración basada en directivas permite supervisar los procedimientos recomendados de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un conjunto de archivos de directivas que puede importar como directivas de procedimientos recomendados y después evalúa las directivas con un conjunto de destinos que incluye instancias, objetos de instancia, bases de datos u objetos de base de datos. Evalúe manualmente las directivas y establecer directivas para evaluar un conjunto de destinos según una programación o para evaluar un conjunto de destinos según un evento. Para obtener más información sobre la administración basada en directivas, vea [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Directivas y reglas para el motor de base de datos  
 En la tabla siguiente se muestran las directivas incluidas con la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se ofrece información sobre las reglas de los procedimientos recomendados que evalúa cada directiva. Las directivas se almacenan como archivos XML y se deben importar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre cómo importar directivas, vea [Importar una directiva de administración basada en directivas](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md).  
  
|Nombre de la directiva|Regla de práctica recomendada|  
|-----------------|------------------------|  
|Algoritmo de cifrado de claves asimétricas|[Intensidad del cifrado de claves asimétricas](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|Ubicación de copia de seguridad y archivo de datos|[Los archivos de copia de seguridad deben estar en dispositivos independientes de los archivos de base de datos](https://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|Ubicación de datos y archivo de registro|[Colocar los datos y los archivos de registro en unidades independientes](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|Cerrar automáticamente la base de datos|[Establecer en OFF la opción de base de datos AUTO_CLOSE](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|Reducir automáticamente la base de datos|[Establecer la opción de base de datos AUTO_SHRINK en OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|Intercalación de base de datos|[Establecer la intercalación de bases de datos definidas por el usuario para que coincidan con las de las bases de datos modelo y maestra](https://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|Comprobación de página de la base de datos|[Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|Estado de la página de la base de datos|[Comprobar la integridad de una base de datos con páginas sospechosas](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Permisos de invitado|[Permisos de invitado en bases de datos de usuario](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|Fecha de la última copia de seguridad correcta|[Copia de seguridad no actualizada](../../relational-databases/policy-based-management/outdated-backup.md)|  
|Permisos de servidor público no concedidos|[Permisos públicos de servidor](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|Solapamiento de máscara de afinidad de SQL Server de 64 bits|[Superposición correcta de la máscara de afinidad y la máscara de entrada y salida de afinidad](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Máscara de afinidad de SQL Server|[Mantener el valor predeterminado de la máscara de afinidad](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|Umbral de procesos bloqueados de SQL Server|[Aumentar o deshabilitar el umbral de procesos bloqueados](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|Seguimiento predeterminado de SQL Server|[Archivos de registro de seguimiento predeterminados deshabilitados](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|Bloqueos dinámicos de SQL Server|[Mantener el valor predeterminado de la opción de configuración Bloqueos](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|Agrupación ligera de SQL Server|[Deshabilitar la agrupación ligera](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|Modo de inicio de sesión de SQL Server|[Elegir un modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md)|  
|Grado máximo de paralelismo de SQL Server|[Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2000 de 32 bits|[Comprobar el valor de Máximo de subprocesos de trabajo](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2000 de 64 bits|[Comprobar el valor de Máximo de subprocesos de trabajo](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2005 y versiones posteriores|[Comprobar el valor de Máximo de subprocesos de trabajo](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Tamaño de paquete de red de SQL Server|[El tamaño de paquete de red no debería superar 8060 bytes](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|Expiración de contraseña de SQL Server|[Expiración de contraseña de inicio de sesión de SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|Directiva de contraseñas de SQL Server|[Seguridad de la contraseña de inicio de sesión de SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|Cifrado de claves simétricas para bases de datos de usuario|[Claves simétricas en bases de datos de usuario](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|Clave simétrica para base de datos maestra|[Claves simétricas en bases de datos del sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Clave simétrica para bases de datos del sistema|[Claves simétricas en bases de datos del sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Base de datos de confianza|[Bit de confianza](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Error por daños en recursos de disco de clúster del registro de eventos de Windows|[Detectar problemas de adaptadores de host SCSI](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Error del control de controlador de dispositivo del registro de eventos de Windows|[Error de control del controlador de dispositivo](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Error por dispositivo no listo del registro de eventos de Windows|[Error por dispositivo no listo](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Error en comprobación de solicitud de E/S del registro de eventos de Windows|[Detect Failed Input and Output Requests](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Advertencia por retraso de E/S del registro de eventos de Windows|[Comprobación del subsistema de entrada y salida de disco para problemas de retraso de E/S](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Error de E/S durante error de página en disco del registro de eventos de Windows|[Error de entrada y salida durante otro error de página en disco](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Error por reintento de lectura del registro de evento de Windows|[Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Error por superación de tiempo de espera de E/S en sistema de registro de eventos de Windows|[Tiempo de espera de entrada y salida del sistema de almacenamiento](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Error del sistema del registro de eventos de Windows|[Errores del sistema inesperados](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con facetas de administración basada en directivas](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  

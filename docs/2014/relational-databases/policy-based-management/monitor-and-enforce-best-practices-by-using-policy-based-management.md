---
title: Supervisión y aplicación de las prácticas recomendadas usando la administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e21317e2019fe1530e346567a5767a1dfc18c329
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165425"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas
  La administración basada en directivas permite supervisar los procedimientos recomendados para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proporciona un conjunto de archivos de directivas que puede importar como mejor las directivas de prácticas y, a continuación, evalúa las directivas con un conjunto de destinos que incluye instancias, objetos de instancia, bases de datos u objetos de base de datos. Puede evaluar manualmente las directivas y establecer directivas para evaluar un conjunto de destinos según una programación o para evaluar un conjunto de destinos según un evento. Para obtener más información sobre la administración basada en directivas, vea [Administrar servidores mediante administración basada en directivas](administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Directivas y reglas para el motor de base de datos  
 En la tabla siguiente se muestra las directivas que se incluyen con la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e incluye información sobre las reglas de prácticas recomendadas que evalúa cada directiva. Las directivas se almacenan como archivos XML y se deben importar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre cómo importar directivas, vea [Importar una directiva de administración basada en directivas](import-a-policy-based-management-policy.md).  
  
|Nombre de la directiva|Regla de práctica recomendada|  
|-----------------|------------------------|  
|Algoritmo de cifrado de claves asimétricas|[Intensidad del cifrado de claves asimétricas](asymmetric-keys-encryption-strength.md)|  
|Ubicación de copia de seguridad y archivo de datos|[Los archivos de copia de seguridad deben estar en dispositivos independientes de los archivos de base de datos](../../database-engine/backup-files-must-be-on-separate-devices-from-the-database-files.md)|  
|Ubicación de datos y archivo de registro|[Colocar los datos y los archivos de registro en unidades independientes](place-data-and-log-files-on-separate-drives.md)|  
|Cerrar automáticamente la base de datos|[Establecer en OFF la opción de base de datos AUTO_CLOSE](set-the-auto-close-database-option-to-off.md)|  
|Reducir automáticamente la base de datos|[Establecer la opción de base de datos AUTO_SHRINK en OFF](set-the-auto-shrink-database-option-to-off.md)|  
|Intercalación de base de datos|[Establecer la intercalación de bases de datos definidas por el usuario para que coincidan con las de las bases de datos modelo y maestra](../../database-engine/set-collation-user-defined-databases-match-master-model-databases.md)|  
|Comprobación de página de la base de datos|[Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.](set-the-page-verify-database-option-to-checksum.md)|  
|Estado de la página de la base de datos|[Comprobar la integridad de una base de datos con páginas sospechosas](check-integrity-of-database-with-suspect-pages.md)|  
|Permisos de invitado|[Permisos de invitado en bases de datos de usuario](guest-permissions-on-user-databases.md)|  
|Fecha de la última copia de seguridad correcta|[Copia de seguridad no actualizada](outdated-backup.md)|  
|Permisos de servidor público no concedidos|[Permisos públicos de servidor](server-public-permissions.md)|  
|Superposición de máscara de afinidad de 32 bits SQL Server|[Máscara de afinidad correcto y superposición de máscara de afinidad de entrada y salida](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Solapamiento de máscara de afinidad de SQL Server de 64 bits|[Máscara de afinidad correcto y superposición de máscara de afinidad de entrada y salida](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Máscara de afinidad de SQL Server|[Mantener el valor predeterminado de la máscara de afinidad](keep-the-affinity-mask-default-value.md)|  
|Umbral de procesos bloqueados de SQL Server|[Aumentar o deshabilitar el umbral de procesos bloqueados](increase-or-disable-blocked-process-threshold.md)|  
|Seguimiento predeterminado de SQL Server|[Archivos de registro de seguimiento predeterminados deshabilitados](default-trace-log-files-disabled.md)|  
|Bloqueos dinámicos de SQL Server|[Mantener el valor predeterminado de la opción de configuración Bloqueos](keep-the-locks-configuration-option-default-value.md)|  
|Agrupación ligera de SQL Server|[Deshabilitar la agrupación ligera](disable-lightweight-pooling.md)|  
|Modo de inicio de sesión de SQL Server|[Elegir un modo de autenticación](../security/choose-an-authentication-mode.md)|  
|Grado máximo de paralelismo de SQL Server|[Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo](set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2000 de 32 bits|[Comprobar el valor de Máximo de subprocesos de trabajo](verify-max-worker-threads-setting.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2000 de 64 bits|[Comprobar el valor de Máximo de subprocesos de trabajo](verify-max-worker-threads-setting.md)|  
|Máximo de subprocesos de trabajo de SQL Server para SQL Server 2005 y versiones posteriores|[Comprobar el valor de Máximo de subprocesos de trabajo](verify-max-worker-threads-setting.md)|  
|Tamaño de paquete de red de SQL Server|[El tamaño de paquete de red no debería superar 8060 bytes](network-packet-size-should-not-exceed-8060-bytes.md)|  
|Expiración de contraseña de SQL Server|[Expiración de contraseña de inicio de sesión de SQL Server](sql-server-login-password-expiration.md)|  
|Directiva de contraseñas de SQL Server|[Seguridad de la contraseña de inicio de sesión de SQL Server](sql-server-login-password-strength.md)|  
|Cifrado de claves simétricas para bases de datos de usuario|[Claves simétricas en bases de datos de usuario](symmetric-keys-on-user-databases.md)|  
|Clave simétrica para base de datos maestra|[Claves simétricas en bases de datos del sistema](symmetric-keys-on-system-databases.md)|  
|Clave simétrica para bases de datos del sistema|[Claves simétricas en bases de datos del sistema](symmetric-keys-on-system-databases.md)|  
|Base de datos de confianza|[Bit de confianza](trustworthy-bit.md)|  
|Error por daños en recursos de disco de clúster del registro de eventos de Windows|[Detectar problemas de adaptadores de host SCSI](detect-scsi-host-adapter-issues.md)|  
|Error del control de controlador de dispositivo del registro de eventos de Windows|[Error de control del controlador de dispositivo](device-driver-control-error.md)|  
|Error por dispositivo no listo del registro de eventos de Windows|[Error por dispositivo no listo](device-not-ready-error.md)|  
|Error en comprobación de solicitud de E/S del registro de eventos de Windows|[Detectar solicitud de entrada y salida con error](detect-failed-input-and-output-requests.md)|  
|Advertencia por retraso de E/S del registro de eventos de Windows|[Comprobación del subsistema de entrada y salida de disco para problemas de retraso de E/S](check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Error de E/S durante error de página en disco del registro de eventos de Windows|[Error de entrada y salida durante otro error de página en disco](input-and-output-error-during-hard-page-fault.md)|  
|Error por reintento de lectura del registro de evento de Windows|[Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco](check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Error por superación de tiempo de espera de E/S en sistema de registro de eventos de Windows|[Tiempo de espera de entrada y salida del sistema de almacenamiento](storage-system-input-output-time-out.md)|  
|Error del sistema del registro de eventos de Windows|[Errores del sistema inesperados](unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con facetas de administración basada en directivas](working-with-policy-based-management-facets.md)  
  
  

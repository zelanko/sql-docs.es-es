---
title: Controlador OLE DB para características de SQL Server | Documentos de Microsoft
description: Controlador de OLE DB para características de SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66f48a985dd0ddafc6f147c45b3fc3be76f7ec19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="ole-db-driver-for-sql-server-features"></a>Controlador OLE DB para características de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Además de exponer las características de datos de Access Components (WDAC) de Windows (Microsoft), controlador de OLE DB para SQL Server implementa también muchas otras características para exponer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funcionalidad.  
  
## <a name="in-this-section"></a>En esta sección    
 [Usar la creación de reflejo de bases de datos](../../oledb/features/using-database-mirroring.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con el uso de bases de datos reflejadas, que es la capacidad para mantener una copia, o reflejo, de una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos en un servidor en espera.  
  
 [Realizar operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)  
 Describe cómo el controlador OLE DB para SQL Server admite operaciones asincrónicas, que es la capacidad de devolver resultados inmediatamente sin bloquear el subproceso que realiza la llamada.  
  
 [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con conjuntos de resultados activos múltiples (MARS). MARS permite ejecutar y recibir varios conjuntos de resultados mediante una conexión a una base de datos única.  
  
 [Utilizar tipos de datos XML](../../oledb/features/using-xml-data-types.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con el tipo de datos XML, que es un tipo de datos basado en XML que puede usarse como un tipo de columna, el tipo de variable, el tipo de parámetro o el tipo de valor devuelto de función.  
  
 [Usar tipos definidos por el usuario](../../oledb/features/using-user-defined-types.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con definidos por el usuario tipos (UDT), que amplía el sistema de tipos SQL al permitirle almacenar objetos y estructuras de datos personalizadas en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos.  
  
 [Uso de tipos de valores grandes](../../oledb/features/using-large-value-types.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con los tipos de datos de valor grande, que son tipos de datos de objetos grandes (LOB).  
  
 [Cambiar las contraseñas mediante programación](../../oledb/features/changing-passwords-programmatically.md)  
 Describe cómo controlador OLE DB para SQL Server admite el tratamiento de las contraseñas han expirado para que ahora se pueden cambiar las contraseñas en el cliente sin intervención del administrador.  
  
 [Trabajar con aislamiento de instantánea](../../oledb/features/working-with-snapshot-isolation.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con la mejora de las versiones de fila que mejora el rendimiento de la base de datos evitando situaciones de bloqueo de lector y escritor.  
  
 [Trabajar con notificaciones de consulta](../../oledb/features/working-with-query-notifications.md)  
 Describe cómo controlador OLE DB para SQL Server admite notificaciones al consumidor a la modificación del conjunto de filas.  
  
 [Realizar operaciones de copia masiva](../../oledb/features/performing-bulk-copy-operations.md)  
 Describe cómo el controlador OLE DB para SQL Server es compatible con operaciones de copia masiva que permiten la transferencia de grandes cantidades de datos dentro o fuera de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla o vista.  
  
 [Utilizar el cifrado sin validación](../../oledb/features/using-encryption-without-validation.md)  
 Describe cómo usar el controlador OLE DB para SQL Server para cifrar los datos enviados al servidor sin validar el certificado.  
  
 [Parámetros con valores de tabla &#40;controlador OLE DB para SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Describe el controlador OLE DB para la compatibilidad con SQL Server para los parámetros con valores de tabla.  
  
 [Tipos definidos por el usuario de CLR grandes](../../oledb/features/large-clr-user-defined-types.md)  
 Explica la compatibilidad con los tipos definidos por el usuario (UDT) de Common Language Runtime (CLR) grandes.  
  
 [Compatibilidad con FILESTREAM](../../oledb/features/filestream-support.md)  
 Describe el controlador OLE DB para la compatibilidad con SQL Server para la característica mejorada FILESTREAM.  
  
 [Nombre Principal de servicio &#40;SPN&#41; compatibilidad con conexiones de cliente](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Explica cómo se ha ampliado la compatibilidad con los nombres principales de servicio (SPN) para habilitar la autenticación mutua en todos los protocolos.  
  
 [Compatibilidad de columnas dispersas con el controlador OLE DB para SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Describe el controlador OLE DB para SQL Server admiten columnas dispersas.  
  
 [Mejoras en la fecha y la hora](../../oledb/features/date-and-time-improvements.md)  
 Describe la compatibilidad agregada para el controlador OLE DB para SQL Server para los tipos de datos de fecha y hora.  
  
 [Detección de metadatos](../../oledb/features/metadata-discovery.md)  
 Describe las mejoras en la detección de metadatos realizadas en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Compatibilidad de UTF-16 con el controlador OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Describe un cambio de comportamiento presentado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Si se proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y la **wchar** carácter escrito en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un par suplente y si la siguiente **wchar** carácter es un punto de código suplente bajo, el controlador OLE DB para SQL Server no agregará el punto de código suplente alto en el búfer.  
  
 [Controlador OLE DB para la compatibilidad de SQL Server con la alta disponibilidad y la recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Describe cómo se puede configurar la aplicación para aprovechar las ventajas de la recuperación ante desastres de alta disponibilidad y funciones de agregan en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Describe las mejoras en el controlador de OLE DB para SQL Server y el seguimiento de datos que proporciona acceso a información de diagnóstico en el búfer de anillo y el registro de XEvents.  
  
 [Controlador OLE DB para la compatibilidad de SQL Server con LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Describe el controlador OLE DB para la compatibilidad con SQL Server para la característica LocalDB.  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [Temas "Cómo..." de OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalación del controlador OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  

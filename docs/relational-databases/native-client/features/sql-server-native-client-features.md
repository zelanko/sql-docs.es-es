---
title: Características
description: Además de exponer las características de los componentes de Windows Data Access, SQL Server Native Client implementa otras características para exponer SQL Server funcionalidad.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec878229524d048969acbf3ca1af7cca4e318084
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008994"
---
# <a name="sql-server-native-client-features"></a>Características de SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Además de exponer las características de Windows (Microsoft en versiones anteriores) Data Access Components (WDAC), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa también muchas otras características para exponer la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Describe un cambio de comportamiento a partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Usar la creación de reflejo de bases de datos](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el uso de bases de datos reflejadas, que es la capacidad de mantener una copia, o reflejo, de una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos en un servidor en espera.  
  
 [Realizar operaciones asincrónicas](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con operaciones asincrónicas, que es la capacidad de devolver resultados inmediatamente sin bloquear el subproceso de llamada.  
  
 [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 Explica cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite varios conjuntos de resultados activos (MARS). MARS permite ejecutar y recibir varios conjuntos de resultados mediante una conexión a una base de datos única.  
  
 [Usar tipos de datos XML](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con el tipo de datos XML, que es un tipo de datos basado en XML que se puede utilizar como un tipo de columna, un tipo de variable, un tipo de parámetro o un tipo de valor devuelto por una función.  
  
 [Usar tipos definidos por el usuario](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite tipos definidos por el usuario (UDT), que amplía el sistema de tipos SQL permitiéndole almacenar objetos y estructuras de datos personalizadas en una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos.  
  
 [Usar tipos de valor grande](../../../relational-databases/native-client/features/using-large-value-types.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con tipos de datos de valor grande, que son tipos de datos de objetos grandes (LOB).  
  
 [Cambiar las contraseñas mediante programación](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con el control de contraseñas que han expirado para que las contraseñas se puedan cambiar ahora en el cliente sin implicación del administrador.  
  
 [Trabajar con aislamiento de instantánea](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con la mejora de las versiones de fila que aumenta el rendimiento de la base de datos evitando situaciones de bloqueo de lectura/escritura.  
  
 [Trabajar con notificaciones de consulta](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 Explica cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el envío de notificaciones al consumidor si se modifica el conjunto de filas.  
  
 [Realizar operaciones de copia masiva](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite operaciones de copia masiva que permiten la transferencia de grandes cantidades de datos a o desde una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla o vista.  
  
 [Utilizar el cifrado sin validación](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 Explica cómo utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para cifrar los datos enviados al servidor sin validar el certificado.  
  
 [Parámetros con valores de tabla &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los parámetros con valores de tabla agregados.  
  
 [Tipos definidos por el usuario de CLR grandes](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 Explica la compatibilidad con los tipos definidos por el usuario (UDT) de Common Language Runtime (CLR) grandes.  
  
 [Compatibilidad con FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md)  
 Describe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la compatibilidad de Native Client con la característica mejorada FileStream.  
  
 [Compatibilidad con Nombre de entidad de seguridad de servicio &#40;SPN&#41; en conexiones cliente](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 Explica cómo se ha ampliado la compatibilidad con los nombres principales de servicio (SPN) para habilitar la autenticación mutua en todos los protocolos.  
  
 [Compatibilidad con columnas dispersas en SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con columnas dispersas.  
  
 [Mejoras de fecha y hora](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 Explica la mayor compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los tipos de datos de fecha y hora.  
  
 [Detección de metadatos](../../../relational-databases/native-client/features/metadata-discovery.md)  
 Describe las mejoras en la detección de metadatos realizadas en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 Describe un cambio de comportamiento presentado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Si proporciona un búfer de longitud fija al enlazar un parámetro de salida o resultado de columna y si el carácter **WCHAR** escrito en el búfer antes del carácter de terminación es un punto de código suplente alto de un par suplente, y si el siguiente carácter **WCHAR** es un punto de código suplente bajo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará el punto de código suplente alto al búfer.  
  
 [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Describe cómo se puede configurar una aplicación para aprovechar las características de alta disponibilidad con recuperación ante desastres que se han agregado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Obtener acceso a la información de diagnóstico en el registro de eventos extendidos](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Describe las mejoras realizadas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y en el seguimiento de datos que le ofrecen acceso a la información de diagnóstico del búfer de anillo y del registro de XEvents.  
  
 [Compatibilidad de SQL Server Native Client con LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con la característica mejorada LocalDB.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Temas de procedimientos de ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Temas de procedimientos de OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalar SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  

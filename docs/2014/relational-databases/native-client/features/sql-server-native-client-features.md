---
title: Características SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 093d40734b88cc370e0c08a8f9a8b86312409e6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074925"
---
# <a name="sql-server-native-client-features"></a>Características de SQL Server Native Client
  Además de exponer las características de Windows (Microsoft en versiones anteriores) Data Access Components (WDAC), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa también muchas otras características para exponer la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres](odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Describe un cambio de comportamiento a partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Usar la creación de reflejo de bases de datos](using-database-mirroring.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el uso de bases de datos reflejadas, que es la capacidad para mantener una copia, o reflejo, de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos en un servidor en espera.  
  
 [Realizar operaciones asincrónicas](performing-asynchronous-operations.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con operaciones asincrónicas, que es la capacidad de devolver resultados inmediatamente sin bloquear el subproceso de llamada.  
  
 [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](using-multiple-active-result-sets-mars.md)  
 Explica cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite varios conjuntos de resultados activos (MARS). MARS permite ejecutar y recibir varios conjuntos de resultados mediante una conexión a una base de datos única.  
  
 [Utilizar tipos de datos XML](using-xml-data-types.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con el tipo de datos XML, que es un tipo de datos basado en XML que se puede utilizar como un tipo de columna, un tipo de variable, un tipo de parámetro o un tipo de valor devuelto por una función.  
  
 [Usar tipos definidos por el usuario](using-user-defined-types.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite definidas por el usuario tipos (UDT), que amplía el sistema de tipos SQL al permitirle almacenar objetos y estructuras de datos personalizadas en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos.  
  
 [Usar tipos de valor grande](using-large-value-types.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con tipos de datos de valor grande, que son tipos de datos de objetos grandes (LOB).  
  
 [Cambiar las contraseñas mediante programación](changing-passwords-programmatically.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con el control de contraseñas que han expirado para que las contraseñas se puedan cambiar ahora en el cliente sin implicación del administrador.  
  
 [Trabajar con aislamiento de instantánea](working-with-snapshot-isolation.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con la mejora de las versiones de fila que aumenta el rendimiento de la base de datos evitando situaciones de bloqueo de lectura/escritura.  
  
 [Trabajar con notificaciones de consulta](working-with-query-notifications.md)  
 Explica cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite el envío de notificaciones al consumidor si se modifica el conjunto de filas.  
  
 [Realizar operaciones de copia masiva](performing-bulk-copy-operations.md)  
 Describe cómo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite operaciones de copia masiva que permiten la transferencia de grandes cantidades de datos dentro o fuera de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla o vista.  
  
 [Utilizar el cifrado sin validación](using-encryption-without-validation.md)  
 Explica cómo utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para cifrar los datos enviados al servidor sin validar el certificado.  
  
 [Parámetros con valores de tabla &#40;SQL Server Native Client&#41;](table-valued-parameters-sql-server-native-client.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los parámetros con valores de tabla agregados.  
  
 [Tipos definidos por el usuario de CLR grandes](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Explica la compatibilidad con los tipos definidos por el usuario (UDT) de Common Language Runtime (CLR) grandes.  
  
 [Compatibilidad con FILESTREAM](filestream-support.md)  
 Describe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con la característica mejorada FILESTREAM.  
  
 [Compatibilidad con Nombre de entidad de seguridad de servicio &#40;SPN&#41; en conexiones cliente](service-principal-name-spn-support-in-client-connections.md)  
 Explica cómo se ha ampliado la compatibilidad con los nombres principales de servicio (SPN) para habilitar la autenticación mutua en todos los protocolos.  
  
 [Compatibilidad con columnas dispersas en SQL Server Native Client](sparse-columns-support-in-sql-server-native-client.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con columnas dispersas.  
  
 [Mejoras en la fecha y la hora](date-and-time-improvements.md)  
 Explica la mayor compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los tipos de datos de fecha y hora.  
  
 [Detección de metadatos](metadata-discovery.md)  
 Describe las mejoras en la detección de metadatos realizadas en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Compatibilidad con UTF-16 en SQL Server Native Client 11.0](utf-16-support-in-sql-server-native-client-11-0.md)  
 Describe un cambio de comportamiento presentado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Si proporciona un búfer de longitud fija al enlazar un parámetro de salida o el resultado de una columna y si el carácter `wchar` escrito en el búfer antes del carácter de terminación es un punto de código que actúa como suplente superior de un par de suplentes y el carácter `wchar` siguiente es un punto de código que actúa como suplente inferior, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará al búfer el punto de código que actúa como suplente superior.  
  
 [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Describe cómo se puede configurar una aplicación para aprovechar las características de alta disponibilidad con recuperación ante desastres que se han agregado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](accessing-diagnostic-information-in-the-extended-events-log.md)  
 Describe las mejoras realizadas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y en el seguimiento de datos que le ofrecen acceso a la información de diagnóstico del búfer de anillo y del registro de XEvents.  
  
 [Compatibilidad de SQL Server Native Client con LocalDB](sql-server-native-client-support-for-localdb.md)  
 Explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con la característica mejorada LocalDB.  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Temas de procedimientos de ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Temas de procedimientos de OLE DB](../../native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalar SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  

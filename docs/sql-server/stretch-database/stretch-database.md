---
title: Stretch Database | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3dab64f6d7c2067eea1c2e5249fc3a7089eda6bc
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch Database migra los datos inactivos de forma clara y segura a la nube de Microsoft Azure.  
  
 Consulte [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)si su intención es comenzar a usar inmediatamente Stretch Database.  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>¿Cuáles son las ventajas de Stretch Database?  
 Stretch Database reporta las siguientes ventajas:  
  
 **Permite disponer de los datos inactivos de forma provechosa**  
 Use SQL Server Stretch Database para ampliar dinámicamente los datos transaccionales tanto activos como inactivos desde SQL Server a Microsoft Azure. A diferencia de lo que suele ocurrir en el almacenamiento de datos inactivos, los datos siempre estarán en línea y disponibles para consultarlos. Además, se pueden establecer escalas de tiempo de retención de datos más prolongadas, sin que ello interrumpa el banco de tablas grandes como el historial de pedidos de cliente. Aproveche el bajo costo de Azure en lugar de escalar a un almacenamiento local prohibitivo. Será usted quien elija el plan de tarifa y configure las opciones que quiera en el Portal de Azure para tener los precios y costos bajo control. Escale o reduzca verticalmente según le convenga. Visite la página de [precios de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) para obtener información pormenorizada.  
  
 **No hay que cambiar las consultas ni las aplicaciones**  
 Disfrute de acceso a los datos de SQL Server sin problemas, independientemente de si están almacenados localmente o extendidos a la nube.  Solo tiene que establecer la directiva que defina dónde se almacenan los datos y SQL Server se encargará del movimiento de datos en segundo plano. La tabla entera estará siempre en línea y lista para consultarse. Además, Stretch Database no requiere ningún cambio en las consultas o aplicaciones existentes: la ubicación de los datos es completamente clara para la aplicación.  
  
 **Agiliza el mantenimiento de los datos locales**  
 Reduzca el almacenamiento y mantenimiento local de los datos. mientras que las de los datos locales son más rápidas y finalizan dentro del período de mantenimiento. Las copias de seguridad de los datos almacenados en la nube se hacen automáticamente, Sus necesidades de almacenamiento local se reducirán considerablemente. El almacenamiento de Azure puede ser hasta un 80 % más asequible que recurrir a una SSD local.  
  
 **Los datos se mantienen seguros incluso durante la migración**  
 Relájese mientras extiende las aplicaciones más importantes a la nube sin correr ningún tipo de riesgo. Always Encrypted de SQL Server permite cifrar los datos en movimiento. La seguridad de nivel de fila y otras características de seguridad avanzadas de SQL Server funcionan también con Stretch Database para proteger los datos.  
  
## <a name="what-does-stretch-database-do"></a>¿Qué hace Stretch Database?  
 Después de habilitar Stretch Database en al menos una tabla, una base de datos y una instancia de SQL Server, comenzará a migrar silenciosamente los datos inactivos a Azure.  
  
-   Si los datos inactivos están almacenados en otra tabla, puede migrarla entera.  
  
-   Si la tabla contiene datos activos e inactivos, puede especificar una función de filtro para seleccionar las filas que se migrarán.

**No es necesario cambiar las consultas ni las aplicaciones cliente existentes.** Seguirá disfrutando de un acceso sin fisuras a los datos locales y remotos, incluso durante la migración de datos. En las consultas remotas es posible percibir una cierta latencia, pero solamente al consultar datos inactivos.

**Con Stretch Database, no se perderá ningún dato** si se produce un error durante la migración. Este producto está dotado, además, de una lógica de reintento que aborda los problemas de conexión que se pueden producir durante la migración. Una vista de administración dinámica indica el estado de la migración.

**La migración de datos se puede pausar** para solucionar problemas en el servidor local o para maximizar el ancho de banda de red disponible.  
  
 ![Información general de la base de datos de Stretch](../../sql-server/stretch-database/media/stretch-overview.png "Información general de la base de datos de Stretch")  
  
## <a name="is-stretch-database-for-you"></a>¿Cómo sé si Stretch Database se ajusta a mis necesidades?  
 Si se siente identificado con alguna de las siguientes afirmaciones, Stretch Database puede ayudarle a satisfacer sus requisitos y a solucionar problemas.  
  
|Soy un responsable de la toma de decisiones y...|Soy un administrador de base de datos y...|  
|--------------------------------|---------------------|  
|Tengo que conservar los datos transaccionales durante mucho tiempo.|El tamaño de las tablas empieza a ser desbordante.|  
|A veces tengo que consultar los datos inactivos.|Mis usuarios afirman que quieren tener acceso a los datos inactivos, pero en realidad apenas si los usan.|  
|Tengo aplicaciones, incluidas aplicaciones antiguas, que no quiero actualizar.|Estoy constantemente adquiriendo y agregando más espacio de almacenamiento.|  
|Quiero encontrar una manera de ahorrar dinero en almacenamiento.|No puedo restaurar unas tablas tan grandes ni hacerles copias de seguridad dentro de los términos del contrato de nivel de servicio.|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>¿Qué tipos de tablas y bases de datos son aptos para Stretch Database?  
 Stretch Database está pensado para bases de datos transaccionales con grandes cantidades de datos inactivos que suelen almacenarse en un número reducido de tablas. Estas tablas pueden contener millones y millones de filas.  
  
 Si usa la característica de tabla temporal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use Stretch Database para migrar total o parcialmente la tabla de historial asociada a un almacenamiento rentable en Azure. Para obtener más información, vea [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).  
  
 Use el Asesor de Stretch Database (una característica del Asesor de actualizaciones de SQL Server 2016) para saber qué bases de datos y tablas son adecuadas para Stretch Database. Para obtener más información, vea [Identificar bases de datos y tablas para Stretch Database al ejecutar el Asesor de Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md). Para obtener más información sobre los posibles problemas de bloqueo, vea [Limitaciones de Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  

## <a name="test-drive-stretch-database"></a>Versión de prueba de Stretch Database  
 **Use la versión de prueba de Stretch Database con la base de datos de ejemplo de AdventureWorks.** Para obtener la base de datos de ejemplo de AdventureWorks, descargue al menos el archivo de base de datos y el archivo de ejemplos y scripts [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=49502). Después de restaurar la base de datos de ejemplo en una instancia de SQL Server 2016, descomprima el archivo de ejemplos y abra el archivo Stretch DB Samples de la carpeta Stretch DB. Ejecute los scripts de este archivo para comprobar el espacio que ocupan los datos antes y después de habilitar Stretch Database, para realizar un seguimiento del progreso de la migración de datos y para confirmar que puede seguir consultando los datos existentes e insertar otros nuevos durante y tras la migración de datos.  
  
## <a name="next-step"></a>Paso siguiente  
 **Identifique las bases de datos y tablas aptas para Stretch Database.** Descargue el Asesor de actualizaciones de SQL Server 2016 y ejecute el Asesor de Stretch Database para saber qué bases de datos y tablas son aptas para Stretch Database. El Asesor de Stretch Database también detecta problemas de bloqueo. Para obtener más información, vea [Identificar bases de datos y tablas para Stretch Database al ejecutar el Asesor de Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md).  
  
  


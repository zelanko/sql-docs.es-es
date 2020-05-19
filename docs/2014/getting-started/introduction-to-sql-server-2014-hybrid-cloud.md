---
title: Introducción a la nube híbrida de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a005ab43ff33023827ea57fc6dbd9584c8da1f2d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706913"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introducción a la nube híbrida de SQL Server 2014
 La mayoría de las aplicaciones presentan algunos desafíos importantes, como alta eficacia, valor empresarial, configuraciones de hardware complejas, picos masivos a petición, y cumplimiento con las normativas del sector y corporativas. Tener en cuenta todos estos factores y generar una tecnología de clase empresarial puede resultar muy complicado. La estrategia de nube híbrida de Microsoft proporciona compatibilidad con los entornos tradicional, de nube privada, de nube pública y de nube híbrida para superar estos desafíos. 
 
 Cuando su empresa requiere una infraestructura de TI flexible que se pueda escalar a petición, puede crear una nube privada en su centro de datos o en una nube pública en centros de datos globales de Azure. Al extender su centro de datos a la nube pública, se crea un modelo de nube híbrida. 
 
 En este tema se presentan las características de SQL Server 2014 que admiten escenarios de nube híbrida. Para obtener información detallada sobre la estrategia de nube híbrida de Microsoft y SQL Server, vea el sitio web [TI híbrida de SQL Server](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure y la nube híbrida 
 Con las tecnologías de Microsoft, puede ejecutar código tanto de forma local como en la nube, en la nube con datos locales o completamente en la nube aprovechando más de un centro de datos. Por tanto, puede mover sus aplicaciones a la nube a su propio ritmo mientras conserva el valor de las inversiones de TI existentes. 
 
 En este artículo, nos centraremos en los escenarios de nube híbrida que abarcan las ofertas de SQL Server local a la nube pública de Azure: [SQL Server en Azure virtual machines](https://msdn.microsoft.com/library/azure/jj823132.aspx) y [Azure Storage](https://www.azure.com/documentation/services/storage/). En concreto, trataremos los escenarios siguientes: 
 
-  [Copia de seguridad y restauración de bases de datos a y desde Azure Storage](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Mantenimiento de réplicas de base de datos en Azure Virtual Machines](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Almacenar archivos de datos de SQL Server en Azure Storage](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Migre las bases de datos de SQL Server existentes a Azure Virtual Machines](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Escenarios de nube híbrida para SQL Server y Microsoft Azure 
 
#### <a name="backup-and-restore-databases-tofrom-azure-storage"></a><a name="backup"></a>Copia de seguridad y restauración de bases de datos a y desde Azure Storage 
 Una de las tareas más fundamentales de los administradores consiste en hacer copia de seguridad y restaurar bases de datos. Con SQL Server y Azure, puede realizar copias de seguridad de las bases de datos en la nube de forma segura. 
 
 Entre las ventajas principales de usar las capacidades de copia de seguridad y restauración de SQL Server con Azure Storage como destino de copia de seguridad se incluyen: 
 
-  Almacenamiento ilimitado de bajo costo 
 
-  Almacenamiento de alta disponibilidad (replicado geográficamente para asegurar que no haya pérdida de datos) 
 
-  Almacenamiento externo que puede admitir requisitos de cumplimiento y de recuperación ante desastres 
 
-  Proceso remoto de copia de seguridad y restauración simplificado 
 
 A continuación se muestra una lista de capacidades de copia de seguridad y restauración de SQL Server para escenarios en la nube y locales: 
 
-  La característica [SQL Server copia de seguridad en dirección URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) le permite realizar una copia de seguridad en Azure Storage especificando la dirección URL como destino de la copia de seguridad. Con esta característica, puede realizar una copia de seguridad manual o configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones externas. 
 
-  La característica de [cifrado de copia de seguridad](../relational-databases/backup-restore/backup-encryption.md) le permite cifrar los datos mientras crea una copia de seguridad para los destinos de almacenamiento: local y Azure Storage. 
 
-  La característica de [compresión de copia de seguridad (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) le permite crear una copia de seguridad, que es menor que una copia de seguridad sin comprimir de los mismos datos. La compresión de una copia de seguridad necesita menos E/S de dispositivo, lo que suele aumentar la velocidad considerablemente. Esto puede aportar grandes ventajas al almacenar archivos de copia de seguridad en Azure Storage. 
 
-  La característica [SQL Server copia de seguridad administrada en Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) permite hacer copia de seguridad automáticamente de las bases de datos SQL Server en [Azure Storage](https://www.azure.com/documentation/services/storage/). Con esta característica, puede configurar SQL Server para administrar la estrategia de copia de seguridad y programar las copias de seguridad de una sola base de datos, o de varias, o establecer los valores predeterminados en el nivel de instancia. 
 
-  La [herramienta copia de seguridad de SQL Server en Azure](https://www.microsoft.com/download/details.aspx?id=40740) permite que la copia de seguridad Azure BLOB Storage y cifra y comprime SQL Server copias de seguridad almacenadas localmente o en la nube. Esta herramienta hace posible tener una única estrategia de copia de seguridad en la nube en varias versiones de SQL Server, como SQL Server 2005, 2008, 2008 R2 y 2014. 
 
#### <a name="maintain-database-replicas-on-azure-virtual-machines"></a><a name="replica"></a>Mantenimiento de réplicas de base de datos en Azure Virtual Machines 
 Tener una solución de recuperación ante desastres estable para las bases de datos es esencial para el éxito de su empresa. La mayoría de los clientes necesitan configurar un sitio de recuperación ante desastres y adquirir hardware adicional para las réplicas de las bases de datos. Con SQL Server y Azure, puede mantener una o varias réplicas de las bases de datos en la nube. 
 
 Entre las ventajas principales de mantener réplicas secundarias en Azure se incluyen: 
 
-  Solución de bajo costo de recuperación ante desastres 
 
-  Conmutación por error transparente de la aplicación 
 
-  Réplicas disponibles para descargar las cargas de trabajo de lectura y las copias de seguridad 
 
 Puede mantener las réplicas secundarias en Azure mediante cualquiera de las técnicas siguientes: 
 
-  El [Asistente para agregar réplica de Azure](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) permite implementar una o varias réplicas de las bases de datos en una máquina virtual de Azure para la recuperación ante desastres. 
 
-  Grupos de disponibilidad AlwaysOn, creación de reflejo de la base de datos y trasvase de registros son las tecnologías más comunes que puede usar para satisfacer las necesidades de alta disponibilidad y recuperación ante desastres de su aplicación. Para obtener más información, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en Azure virtual machines](https://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store-sql-server-data-files-in-azure-storage"></a><a name="store"></a>Almacenar archivos de datos de SQL Server en Azure Storage 
 El almacenamiento de archivos de datos de SQL Server local en Azure Storage proporciona un almacenamiento fuera de la ubicación flexible, confiable e ilimitado para las bases de datos. A partir de SQL Server 2014, puede usar [SQL Server archivos de datos en Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) para almacenar archivos de base de datos de SQL Server en Azure Storage. Con esta característica, puede trasladar los archivos de datos y de registro de la base de datos local a Azure Storage, manteniendo el nodo de proceso de SQL Server ejecutándose en el entorno local. Esta característica permite tener una capacidad de almacenamiento ilimitada en Azure Storage. 
 
 Entre las ventajas principales de almacenar archivos de datos de SQL Server Azure Storage se incluyen: 
 
-  Almacenamiento ilimitado de bajo costo en Azure Storage 
 
-  Más indicado para traspasar las cargas de trabajo de lectura históricas en la nube con el fin de admitir aplicaciones de informes locales 
 
-  Facilite la recuperación ante desastres separando la instancia de proceso (una instancia de SQL Server) y los datos (archivos de datos de SQL Server). Esto le permite adjuntar fácilmente la base de datos a otra instancia de SQL Server en un entorno local o en una máquina virtual de Azure en caso de desastre. 
 
#### <a name="migrate-existing-sql-server-databases-to-azure-virtual-machines"></a><a name="migrate"></a>Migre las bases de datos de SQL Server existentes a Azure Virtual Machines 
 La informática en nube aporta algunas ventajas importantes a las empresas, como la disponibilidad de recursos virtualizados ilimitados según un modelo de pago por uso; puede aprovechar los centros de datos en la nube que están disponibles de forma pública en lugar de crear y administrar sus propios centros de datos, por lo que puede reducir los costos de TI y de hardware. 
 
 Con [SQL Server en azure virtual machines](https://msdn.microsoft.com/library/azure/jj823132.aspx), puede trasladar las aplicaciones locales existentes a Azure con cambios mínimos en el código. Los administradores y los desarrolladores pueden seguir usando las mismas herramientas de desarrollo y administración que tienen disponibles de forma local. 
 
 Mover una base de datos de SQL Server local a SQL Server que se ejecuta en una máquina virtual de Azure suele tomar una de estas rutas de acceso: 
 
-  **Mover solo la base de datos:** Hay varias herramientas y técnicas disponibles para migrar bases de datos locales existentes a SQL Server en Azure Virtual Machines. Para obtener instrucciones y recomendaciones sobre la migración a SQL Server en Azure Virtual Machines, consulte [preparación para migrar a SQL Server en azure virtual machines](https://msdn.microsoft.com/library/dn133142.aspx) y [migración a SQL Server en una máquina virtual de Azure](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   Además, a partir de SQL Server 2014, hay disponible un nuevo Asistente para [implementar una base de datos de SQL Server en una máquina virtual de Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) para implementar la base de datos en otra instancia de SQL Server que se ejecute en una máquina virtual de Azure. 
 
-  **Mover toda la máquina virtual:** Puede traer sus propias SQL Server máquinas virtuales a Azure o crear una con la imagen de la plataforma. Después, puede cargar y conectar a la máquina virtual un disco de datos que ya contenga datos, o conectar un disco vacío a la máquina. Tener una instancia de datos de SQL Server en Azure Virtual Machines con discos de datos conectados proporciona otro almacenamiento persistente para los archivos de datos y los datos de la aplicación. Para obtener información completa y procedimientos, consulte [SQL Server implementación en Azure virtual machines](https://msdn.microsoft.com/library/dn133141.aspx). 
 
 Si tiene previsto trasladar las capas de aplicación (como el nivel de presentación, el nivel empresarial y el nivel de base de datos) a Azure Virtual Machines, se recomienda que revise las recomendaciones proporcionadas en el artículo [patrones de aplicaciones y estrategias de desarrollo para SQL Server en azure virtual machines](https://msdn.microsoft.com/library/dn574746.aspx) . El objetivo de este artículo es proporcionar a los desarrolladores y arquitectos de soluciones una base para la buena arquitectura y diseño de aplicaciones, que pueden seguir al migrar las aplicaciones existentes a Azure, así como al desarrollar nuevas aplicaciones en Azure. Para cada patrón de aplicación, el artículo describe un escenario local, su solución habilitada para la nube correspondiente y las recomendaciones técnicas relacionadas. Además, el artículo describe estrategias de desarrollo específicas de Azure para que pueda diseñar sus aplicaciones correctamente. 
 
## <a name="see-also"></a>Consulte también: 
 [Guía del producto SQL Server 2014 CTP2](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Series de blogs de nube híbrida de Microsoft SQL Server](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [Migración de aplicaciones centradas en datos a Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 

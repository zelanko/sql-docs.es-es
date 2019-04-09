---
title: Introducción a la nube híbrida SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89344537c53c4caf066536804557451c965e4596
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241623"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introducción a la nube híbrida de SQL Server 2014
 La mayoría de las aplicaciones presentan algunos desafíos importantes, como alta eficacia, valor empresarial, configuraciones de hardware complejas, picos masivos a petición, y cumplimiento con las normativas del sector y corporativas. Tener en cuenta todos estos factores y generar una tecnología de clase empresarial puede resultar muy complicado. La estrategia de nube híbrida de Microsoft proporciona compatibilidad con los entornos tradicional, de nube privada, de nube pública y de nube híbrida para superar estos desafíos. 
 
 Cuando su empresa requiere una infraestructura de TI flexible que puede escalar a petición, puede crear una nube privada en su centro de datos o una nube pública en los centros de datos globales de Azure. Al extender su centro de datos a la nube pública, se crea un modelo de nube híbrida. 
 
 En este tema se presentan las características de SQL Server 2014 que admiten escenarios de nube híbrida. Para obtener información detallada sobre la estrategia de nube híbrida de Microsoft y SQL Server, vea el sitio web [TI híbrida de SQL Server](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure y la nube híbrida 
 Con las tecnologías de Microsoft, puede ejecutar código tanto de forma local como en la nube, en la nube con datos locales o completamente en la nube aprovechando más de un centro de datos. Por tanto, puede mover sus aplicaciones a la nube a su propio ritmo mientras conserva el valor de las inversiones de TI existentes. 
 
 En este artículo, nos centraremos en los escenarios de nube híbrida que abarcan desde un entorno local de SQL Server a las ofertas de nube pública de Azure: [SQL Server en máquinas virtuales de Azure](https://msdn.microsoft.com/library/azure/jj823132.aspx) y [almacenamiento de Azure](http://www.azure.com/documentation/services/storage/). En concreto, trataremos los escenarios siguientes: 
 
-  [Copia de seguridad y restaurar bases de datos hacia y desde Azure Storage](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Mantener las réplicas de base de datos en Azure Virtual Machines](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Store los archivos de datos SQL Server en Azure Storage](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Migrar bases de datos de SQL Server existentes a Azure Virtual Machines](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Escenarios de nube híbrida para SQL Server y Microsoft Azure 
 
#### <a name="backup"></a> Copia de seguridad y restaurar bases de datos hacia y desde Azure Storage 
 Una de las tareas más fundamentales de los administradores consiste en hacer copia de seguridad y restaurar bases de datos. Con SQL Server y Azure, con seguridad hacer una copia de las bases de datos en la nube. 
 
 Las principales ventajas de usar las capacidades de copia de seguridad y restauración de SQL Server con Azure Storage como destino de copia de seguridad incluyen: 
 
-  Almacenamiento ilimitado de bajo costo 
 
-  Almacenamiento de alta disponibilidad (replicado geográficamente para asegurar que no haya pérdida de datos) 
 
-  Almacenamiento externo que puede admitir requisitos de cumplimiento y de recuperación ante desastres 
 
-  Proceso remoto de copia de seguridad y restauración simplificado 
 
 A continuación se muestra una lista de capacidades de copia de seguridad y restauración de SQL Server para escenarios en la nube y locales: 
 
-  El [copias de seguridad de SQL Server a URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) característica le permite realizar copias de seguridad en Azure Storage mediante la especificación de dirección URL como destino de copia de seguridad. Con esta característica, puede realizar una copia de seguridad manual o configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones externas. 
 
-  El [copia de seguridad cifrado](../relational-databases/backup-restore/backup-encryption.md) característica le permite cifrar los datos mientras crea una copia de seguridad para los destinos de almacenamiento: de forma local y Azure Storage. 
 
-  El [compresión de copia de seguridad (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) característica le permite crear una copia de seguridad, que es menor que una copia de seguridad sin comprimir de los mismos datos. La compresión de una copia de seguridad necesita menos E/S de dispositivo, lo que suele aumentar la velocidad considerablemente. Esto puede aportar grandes ventajas al almacenar archivos de copia de seguridad en Azure Storage. 
 
-  El [SQL Server Managed Backup en Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) característica permite la copia de seguridad automáticamente bases de datos de SQL Server para [Azure Storage](http://www.azure.com/documentation/services/storage/). Con esta característica, puede configurar SQL Server para administrar la estrategia de copia de seguridad y programar las copias de seguridad de una sola base de datos, o de varias, o establecer los valores predeterminados en el nivel de instancia. 
 
-  El [copias de seguridad de SQL Server para Azure Tool](https://www.microsoft.com/download/details.aspx?id=40740) permite la copia de seguridad en Azure Blob Storage y cifra y comprime las copias de seguridad de SQL Server almacenadas localmente o en la nube. Esta herramienta hace posible tener una única estrategia de copia de seguridad en la nube en varias versiones de SQL Server, como SQL Server 2005, 2008, 2008 R2 y 2014. 
 
#### <a name="replica"></a> Mantener las réplicas de base de datos en Azure Virtual Machines 
 Tener una solución de recuperación ante desastres estable para las bases de datos es esencial para el éxito empresarial. La mayoría de los clientes necesitan configurar un sitio de recuperación ante desastres y adquirir hardware adicional para las réplicas de las bases de datos. Con SQL Server y Azure, puede mantener una o varias réplicas de las bases de datos en la nube. 
 
 Las ventajas claves de mantener las réplicas secundarias de Azure incluyen: 
 
-  Solución de bajo costo de recuperación ante desastres 
 
-  Conmutación por error transparente de la aplicación 
 
-  Réplicas disponibles para descargar las cargas de trabajo de lectura y las copias de seguridad 
 
 Puede mantener las réplicas secundarias de Azure mediante cualquiera de las técnicas siguientes: 
 
-  El [Asistente para agregar réplica de Azure](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) le permite implementar una o varias réplicas de las bases de datos a una máquina virtual en Azure para la recuperación ante desastres. 
 
-  Grupos de disponibilidad AlwaysOn, creación de reflejo de base de datos y trasvase de registros son las tecnologías más comunes que puede usar para abordar la alta disponibilidad de su aplicación y necesidades de recuperación ante desastres. Para obtener información, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store"></a> Store los archivos de datos SQL Server en Azure Storage 
 Almacenar archivos de datos de SQL Server local en Azure Storage proporciona un almacenamiento externo flexible, confiable e ilimitado para las bases de datos. A partir de SQL Server 2014, puede usar [archivos de datos de SQL Server en Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) para almacenar los archivos de base de datos de SQL Server en Azure Storage. Con esta característica, puede mover los datos y los archivos de registro de base de datos de forma local en el almacenamiento de Azure, manteniendo el nodo de proceso de SQL Server que se ejecutan en local. Esta característica permite tener capacidad de almacenamiento ilimitada en almacenamiento de Azure. 
 
 Las principales ventajas de almacenar archivos de datos de SQL Server Azure Storage incluyen: 
 
-  Almacenamiento ilimitado de bajo costo en Azure Storage 
 
-  Más indicado para traspasar las cargas de trabajo de lectura históricas en la nube con el fin de admitir aplicaciones de informes locales 
 
-  Facilite la recuperación ante desastres separando la instancia de proceso (una instancia de SQL Server) y los datos (archivos de datos de SQL Server). Esto le permite adjuntar fácilmente la base de datos a otra instancia de SQL Server en un entorno local o en una máquina virtual de Azure en caso de desastre. 
 
#### <a name="migrate"></a> Migrar bases de datos de SQL Server existentes a Azure Virtual Machines 
 La informática en nube aporta algunas ventajas importantes a las empresas, como la disponibilidad de recursos virtualizados ilimitados según un modelo de pago por uso; puede aprovechar los centros de datos en la nube que están disponibles de forma pública en lugar de crear y administrar sus propios centros de datos, por lo que puede reducir los costos de TI y de hardware. 
 
 Con [SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj823132.aspx), puede mover las aplicaciones locales existentes a Azure con el mínimo o ningún código cambia. Los administradores y los desarrolladores pueden seguir usando las mismas herramientas de desarrollo y administración que tienen disponibles de forma local. 
 
 Mover una base de datos desde un entorno local de SQL Server a SQL Server en una máquina Virtual de Azure normalmente toma una de estas rutas de acceso: 
 
-  **Mover la base de datos:** Hay varias herramientas y técnicas mover bases de datos locales existentes a SQL Server en Azure Virtual Machines. Para obtener instrucciones y recomendaciones sobre la migración a SQL Server en Azure Virtual Machines, consulte [preparar la migración a SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/dn133142.aspx) y también [migrar a SQL Server en una máquina Virtual de Azure ](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   Además, a partir de SQL Server 2014, un nuevo asistente, [implementar una base de datos de SQL Server a una máquina Virtual de Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) está disponible para que pueda implementar la base de datos a otra instancia de SQL Server que se ejecuta en una máquina Virtual de Azure. 
 
-  **Mover toda la máquina virtual:** Puede traer sus propias máquinas virtuales de SQL Server a Azure o crear uno mediante el uso de la imagen de plataforma. Después, puede cargar y conectar a la máquina virtual un disco de datos que ya contenga datos, o conectar un disco vacío a la máquina. Tener una instancia de datos de SQL Server en Azure Virtual Machines con discos de datos conectados proporciona otro almacenamiento persistente para los archivos de datos y los datos de la aplicación. Para obtener información completa y procedimientos, consulte [implementación de SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/dn133141.aspx). 
 
 Si va a mover los niveles de aplicación (por ejemplo, el nivel de presentación, el nivel de empresa y el nivel de base de datos) a Azure Virtual Machines, se recomienda que revise las recomendaciones proporcionadas en el [desarrollo y patrones de aplicación Estrategias para SQL Server en Azure Virtual Machines](https://msdn.microsoft.com/library/dn574746.aspx) artículo. El objetivo de este artículo es ofrecer a los desarrolladores y arquitectos de soluciones una base para aplicación buena arquitectura y diseño, que pueden seguir al migrar aplicaciones existentes a Azure, así como desarrollar nuevas aplicaciones en Azure. Para cada patrón de aplicación, el artículo describe un escenario local, su solución habilitada para la nube correspondiente y las recomendaciones técnicas relacionadas. Además, el artículo describe las estrategias de desarrollo específicas de Azure para que pueda diseñar sus aplicaciones correctamente. 
 
## <a name="see-also"></a>Vea también 
 [Guía del producto SQL Server 2014 CTP2](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Series de blogs de nube híbrida de Microsoft SQL Server](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [Migrar aplicaciones centradas en datos a Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
 

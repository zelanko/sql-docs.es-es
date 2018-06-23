---
title: Introducción a la nube híbrida SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fc36b9e907a9399a47b2d4f3a743e3f83bfa7a31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102911"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introducción a la nube híbrida de SQL Server 2014
 La mayoría de las aplicaciones presentan algunos desafíos importantes, como alta eficacia, valor empresarial, configuraciones de hardware complejas, picos masivos a petición, y cumplimiento con las normativas del sector y corporativas. Tener en cuenta todos estos factores y generar una tecnología de clase empresarial puede resultar muy complicado. La estrategia de nube híbrida de Microsoft proporciona compatibilidad con los entornos tradicional, de nube privada, de nube pública y de nube híbrida para superar estos desafíos. 
 
 Cuando su empresa requiere una infraestructura de TI flexible que pueda escalar a petición, puede crear una nube privada en su centro de datos o una nube pública en centros de datos globales de Azure. Al extender su centro de datos a la nube pública, se crea un modelo de nube híbrida. 
 
 En este tema se presentan las características de SQL Server 2014 que admiten escenarios de nube híbrida. Para obtener información detallada sobre la estrategia de nube híbrida de Microsoft y SQL Server, vea el sitio web [TI híbrida de SQL Server](http://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure y la nube híbrida 
 Con las tecnologías de Microsoft, puede ejecutar código tanto de forma local como en la nube, en la nube con datos locales o completamente en la nube aprovechando más de un centro de datos. Por tanto, puede mover sus aplicaciones a la nube a su propio ritmo mientras conserva el valor de las inversiones de TI existentes. 
 
 En este artículo, nos centraremos en los escenarios de nube híbrida que abarcan desde el servidor local de SQL a las ofertas de nube pública de Azure: [SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/azure/jj823132.aspx) y [el almacenamiento de Azure](http://www.azure.com/documentation/services/storage/). Concretamente, trataremos los escenarios siguientes: 
 
-  [Copia de seguridad y restaurar bases de datos de almacenamiento de Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Mantener réplicas de base de datos en máquinas virtuales de Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Almacenar archivos de datos SQL Server en almacenamiento de Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Migrar bases de datos de SQL Server existentes a máquinas virtuales de Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Escenarios de nube híbrida para SQL Server y Microsoft Azure 
 
#### <a name="backup"></a> Copia de seguridad y restaurar bases de datos de almacenamiento de Azure 
 Una de las tareas más fundamentales de los administradores consiste en hacer copia de seguridad y restaurar bases de datos. Con SQL Server y Azure, sin ningún riesgo hacer una copia de las bases de datos en la nube. 
 
 Las ventajas principales de usar las capacidades de copia de seguridad y restauración de SQL Server con almacenamiento de Azure como destino de copia de seguridad incluyen: 
 
-  Almacenamiento ilimitado de bajo costo 
 
-  Almacenamiento de alta disponibilidad (replicado geográficamente para asegurar que no haya pérdida de datos) 
 
-  Almacenamiento externo que puede admitir requisitos de cumplimiento y de recuperación ante desastres 
 
-  Proceso remoto de copia de seguridad y restauración simplificado 
 
 A continuación se muestra una lista de capacidades de copia de seguridad y restauración de SQL Server para escenarios en la nube y locales: 
 
-  El [copias de seguridad de SQL Server a URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) característica permite realizar una copia al almacenamiento de Azure especificando la dirección URL como destino de la copia de seguridad. Con esta característica, puede realizar una copia de seguridad manual o configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones externas. 
 
-  El [copia de seguridad cifrado](../relational-databases/backup-restore/backup-encryption.md) característica le permite cifrar los datos mientras crea una copia de seguridad para los destinos de almacenamiento: local y el almacenamiento de Azure. 
 
-  El [compresión de copia de seguridad (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) característica le permite crear una copia de seguridad, que es menor que una copia de seguridad sin comprimir de los mismos datos. La compresión de una copia de seguridad necesita menos E/S de dispositivo, lo que suele aumentar la velocidad considerablemente. Esto puede aportar grandes ventajas al almacenar archivos de copia de seguridad en el almacenamiento de Azure. 
 
-  El [SQL Server Managed Backup to Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) característica permite a la copia de seguridad automáticamente bases de datos de SQL Server a [el almacenamiento de Azure](http://www.azure.com/documentation/services/storage/). Con esta característica, puede configurar SQL Server para administrar la estrategia de copia de seguridad y programar las copias de seguridad de una sola base de datos, o de varias, o establecer los valores predeterminados en el nivel de instancia. 
 
-  El [copias de seguridad de SQL Server a Azure herramienta](http://www.microsoft.com/download/details.aspx?id=40740) permite la copia de seguridad en almacenamiento de blobs de Azure y cifra y comprime las copias de seguridad de SQL Server almacenadas localmente o en la nube. Esta herramienta hace posible tener una única estrategia de copia de seguridad en la nube en varias versiones de SQL Server, como SQL Server 2005, 2008, 2008 R2 y 2014. 
 
#### <a name="replica"></a> Mantener réplicas de base de datos en máquinas virtuales de Azure 
 Tener una solución estable de recuperación ante desastres para las bases de datos es esencial para el éxito empresarial. La mayoría de los clientes necesitan configurar un sitio de recuperación ante desastres y adquirir hardware adicional para las réplicas de las bases de datos. Con SQL Server y Azure, puede mantener una o varias réplicas de las bases de datos en la nube. 
 
 Las ventajas principales de mantener réplicas secundarias en Azure se incluyen: 
 
-  Solución de bajo costo de recuperación ante desastres 
 
-  Conmutación por error transparente de la aplicación 
 
-  Réplicas disponibles para descargar las cargas de trabajo de lectura y las copias de seguridad 
 
 Puede conservar réplicas secundarias en Azure mediante cualquiera de las técnicas siguientes: 
 
-  El [Asistente para agregar réplica de Azure](http://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) le permite implementar una o varias réplicas de las bases de datos a una máquina virtual en Azure para la recuperación ante desastres. 
 
-  Los grupos de disponibilidad AlwaysOn, la creación de reflejo de la base de datos, y el trasvase de registros son las tecnologías más frecuentes que se emplean para satisfacer las necesidades de alta disponibilidad y recuperación ante desastres de la aplicación. Para obtener información, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store"></a> Almacenar archivos de datos SQL Server en almacenamiento de Azure 
 Almacenar archivos de datos de SQL Server local en el almacenamiento de Azure proporciona un almacenamiento externo flexible, confiable e ilimitado para las bases de datos. A partir de SQL Server 2014, puede usar [archivos de datos de SQL Server en Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) para almacenar archivos de base de datos de SQL Server en almacenamiento de Azure. Con esta característica, puede mover los datos y archivos de registro de base de datos local en el almacenamiento de Azure, manteniendo el nodo de proceso de SQL Server que se ejecutan de forma local. Esta característica permite tener capacidad de almacenamiento ilimitada en almacenamiento de Azure. 
 
 Las ventajas principales de almacenar archivos de datos de SQL Server el almacenamiento de Azure incluyen: 
 
-  Almacenamiento ilimitado de bajo costo en almacenamiento de Azure 
 
-  Más indicado para traspasar las cargas de trabajo de lectura históricas en la nube con el fin de admitir aplicaciones de informes locales 
 
-  Facilite la recuperación ante desastres separando la instancia de proceso (una instancia de SQL Server) y los datos (archivos de datos de SQL Server). Esto le permite adjuntar fácilmente la base de datos a otra instancia de SQL Server en un entorno local o en una máquina virtual de Azure en el caso de un desastre. 
 
#### <a name="migrate"></a> Migrar bases de datos de SQL Server existentes a máquinas virtuales de Azure 
 La informática en nube aporta algunas ventajas importantes a las empresas, como la disponibilidad de recursos virtualizados ilimitados según un modelo de pago por uso; puede aprovechar los centros de datos en la nube que están disponibles de forma pública en lugar de crear y administrar sus propios centros de datos, por lo que puede reducir los costos de TI y de hardware. 
 
 Con [SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/azure/jj823132.aspx), puede mover las aplicaciones locales existentes a Azure con una o no cambia de ningún código. Los administradores y los desarrolladores pueden seguir usando las mismas herramientas de desarrollo y administración que tienen disponibles de forma local. 
 
 Mover una base de datos de local de SQL Server a SQL Server que se ejecuta en una máquina Virtual de Azure suele toma una de estas rutas de acceso: 
 
-  **Mover la base de datos:** hay varias herramientas y técnicas mover locales existentes bases de datos a SQL Server en máquinas virtuales de Azure. Para obtener instrucciones y recomendaciones sobre la migración a SQL Server en máquinas virtuales de Azure, consulte [preparar la migración a SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/dn133142.aspx) y también [migrar a SQL Server en una máquina Virtual de Azure ](http://msdn.microsoft.com/library/jj156165.aspx). 
 
   Además, a partir de SQL Server 2014, un nuevo asistente, [implementar una base de datos de SQL Server a una máquina Virtual de Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) está disponible para que pueda implementar la base de datos a otra instancia de SQL Server que se ejecuta en una máquina Virtual de Azure. 
 
-  **Mover toda la máquina virtual:** puede llevar sus propias máquinas virtuales de SQL Server en Azure o crear uno mediante la imagen de plataforma. Después, puede cargar y conectar a la máquina virtual un disco de datos que ya contenga datos, o conectar un disco vacío a la máquina. Tener una instancia de datos de SQL Server en máquinas virtuales de Azure con discos de datos conectados proporciona otro almacenamiento persistente para los archivos de datos y los datos de la aplicación. Para obtener información completa y procedimientos, consulte [implementación de SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/dn133141.aspx). 
 
 Si tiene previsto mover máquinas virtuales de Azure de las capas de aplicación (por ejemplo, el nivel de presentación, el nivel empresarial y el nivel de base de datos), se recomienda que revise las recomendaciones proporcionadas en el [patrones de aplicación y desarrollo Estrategias para SQL Server en máquinas virtuales Azure](http://msdn.microsoft.com/library/dn574746.aspx) artículo. El objetivo de este artículo es proporcionar una base de arquitectos de soluciones y a los desarrolladores de arquitectura de aplicaciones buenos y diseño, que puede seguir al migrar aplicaciones existentes a Azure, así como desarrollar nuevas aplicaciones en Azure. Para cada patrón de aplicación, el artículo describe un escenario local, su solución habilitada para la nube correspondiente y las recomendaciones técnicas relacionadas. Además, el artículo describe las estrategias de desarrollo específicas de Azure para que pueda diseñar aplicaciones correctamente. 
 
## <a name="see-also"></a>Vea también 
 [Guía de producto SQL Server 2014 CTP2](http://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](http://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Serie de blogs de nube híbrida de Microsoft SQL Server](http://blogs.msdn.com/b/azure/archive/2013/10/16/microsoft-sql-server-hybrid-cloud-blog-series.aspx)  
 [Migrar aplicaciones centradas en datos a Azure](http://msdn.microsoft.com/library/jj156154.aspx) 
 
 
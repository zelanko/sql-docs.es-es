---
title: Servicio de almacenamiento de blobs de SQL Server Backup and Restore con Windows Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 98f774809a3b6bb1d37836c3e7c216f1058a9ec1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103587"
---
# <a name="sql-server-backup-and-restore-with-windows-azure-blob-storage-service"></a>Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage
  Este tema se presentan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copias de seguridad y restaurar desde el [servicio de almacenamiento de blobs de Windows Azure](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). También se proporciona un resumen de las ventajas de usar Microsoft Azure Blob service para almacenar copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 SQL Server permite almacenar las copias de seguridad del servicio de almacenamiento Blob de Windows Azure de las maneras siguientes:  
  
-   **Administrar las copias de seguridad de Windows Azure:** con los mismos métodos usados para copia de seguridad en disco y cinta, ahora hacer copias de seguridad en el almacenamiento de Windows Azure especificando la dirección URL como destino de la copia de seguridad.  Puede utilizar esta característica para realizar la copia de seguridad manualmente o para configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones fuera de las instalaciones. Esta característica también se conoce como **Copia de seguridad en URL de SQL Server**. Para obtener más información, vea [SQL Server Backup to URL](sql-server-backup-to-url.md). Esta característica está disponible en SQL Server 2012 SP1 CU2 o posterior.  
  
    > [!NOTE]  
    >  En las versiones de SQL Server anteriores a SQL Server 2014, puede utilizar el complemento de la herramienta de Microsoft Azure Copia de seguridad de SQL Server para crear rápida y fácilmente copias de seguridad del Almacenamiento de Microsoft Azure. Para obtener más información, vea [centro de descarga](http://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Permitir que copias de seguridad de administración de SQL Server en Windows Azure:** Configure SQL Server para administrar las copias de seguridad estrategia y la programación de copia de seguridad para una sola base de datos o varias bases de datos, o establecer los valores predeterminados en el nivel de instancia. Esta característica se conoce como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**. Para obtener más información, consulte [SQL Server Managed Backup to Windows Azure](sql-server-managed-backup-to-microsoft-azure.md). Esta característica está disponible en SQL Server 2014 o posterior.  
  
## <a name="benefits-of-using-the-windows-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Ventajas de usar el servicio Blob de Microsoft Azure para las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Almacenamiento externo flexible, confiable e ilimitado: el almacenamiento de las copias de seguridad en Microsoft Azure Blob service puede ser una opción externa cómoda, flexible y de fácil acceso. La creación de almacenamiento externo para las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser tan sencillo como modificar los scripts y trabajos existentes. Normalmente, el almacenamiento externo debe estar suficientemente alejado de la ubicación de la base de datos de producción para impedir que un desastre afecte a las ubicaciones de las bases de datos externa y de producción. La elección de la replicación geográfica en el almacenamiento de blobs permite disponer de un nivel de protección adicional en caso de que se produzca un desastre que pueda afectar a toda la región. Además, las copias de seguridad están disponibles desde cualquier lugar y en cualquier momento y se puede tener acceso a ellas fácilmente para las restauraciones.  
  
-   Archivado de copias de seguridad: el servicio Azure Blob Storage ofrece una alternativa mejor que la opción de cinta que se suele usar para archivar copias de seguridad. El almacenamiento en cinta puede requerir el transporte físico a una instalación externa y medidas para proteger los medios. El almacenamiento de las copias de seguridad en el servicio de almacenamiento Blob de Windows Azure proporciona una opción de archivado instantánea, de alta disponibilidad y duradera.  
  
-   Sin sobrecarga de administración de hardware: no existe ninguna sobrecarga de administración de hardware con los servicios de Windows Azure. Los servicios de Windows Azure administran el hardware y proporcionan replicación geográfica para ofrecer redundancia y protección frente a errores de hardware.  
  
-   Actualmente, para las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en una máquina virtual de Windows Azure, se pueden realizar copias de seguridad en los servicios de almacenamiento de Windows Azure Blob mediante la creación de discos conectados. Sin embargo, hay un límite en cuanto al número de discos que puede conectar a una máquina virtual de Windows Azure. Este límite es de 16 discos para una instancia muy grande e inferior para instancias menores. Al habilitar una copia de seguridad directa en el almacenamiento de blobs de Windows Azure, puede eludir el límite de 16 discos.  
  
     Además, el archivo de copia de seguridad que ahora se almacena en el servicio de almacenamiento Blob de Windows Azure está disponible directamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local o en otro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en una máquina virtual de Windows Azure, sin necesidad de adjuntar/separar bases de datos o de descargar y conectar el disco duro virtual.  
  
-   Ventajas de costo: solo se paga por el servicio que se emplea. Puede ser rentable como opción de archivado externo y de copia de seguridad. Consulte la [consideraciones sobre facturación de Windows Azure](#Billing) sección para obtener más información y vínculos.  
  
##  <a name="Billing"></a> Consideraciones sobre la facturación de Microsoft Azure:  
 Entender los costos de almacenamiento de Windows Azure permite prever el costo de crear y almacenar copias de seguridad en Windows Azure.  
  
 El [Calculadora de precios de Windows Azure](http://go.microsoft.com/fwlink/?LinkId=277060) puede ayudarle a calcular los costos.  
  
 **Almacenamiento** : los cargos se basan en el espacio usado y se calculan según una escala graduada y el nivel de redundancia. Para obtener más detalles e información actualizada, vea la sección **Administración de datos** del artículo [Detalles de precios](http://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Las transferencias de datos:** las transferencias de datos de entrada en Windows Azure son gratuitas. Las transferencias salientes se cobran por el uso de ancho de banda y se calculan según una escala graduada específica de la región. Para obtener más detalles, vea la sección [Transferencias de datos](http://go.microsoft.com/fwlink/?LinkId=277061) del artículo Detalles de precios.  
  
## <a name="see-also"></a>Vea también  
 [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: SQL Server Backup and Restore a Windows Azure Blob Storage Service](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [Copia de seguridad en URL de SQL Server](sql-server-backup-to-url.md)  
  
  
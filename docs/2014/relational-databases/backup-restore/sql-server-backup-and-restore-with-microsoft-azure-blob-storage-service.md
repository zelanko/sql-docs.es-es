---
title: SQL Server copias de seguridad y restauración con Azure Blob Storage servicio | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38c92e397c971f6e9976bb857c63410fa60b7e85
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232431"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage
  En este tema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se presentan las copias de seguridad y la restauración desde el [servicio de almacenamiento de blobs de Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). También se ofrece un resumen de las ventajas de usar Azure Blob service para almacenar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copias de seguridad.  
  
 SQL Server admite el almacenamiento de copias de seguridad en el servicio de almacenamiento de blobs de Azure de las siguientes maneras:  
  
-   **Administre las copias de seguridad en Azure:** Con los mismos métodos usados para hacer una copia de seguridad en disco y cinta, ahora puede realizar una copia de seguridad en Azure Storage especificando la dirección URL como destino de la copia de seguridad.  Puede utilizar esta característica para realizar la copia de seguridad manualmente o para configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones fuera de las instalaciones. Esta característica también se conoce como **Copia de seguridad en URL de SQL Server**. Para obtener más información, vea [Copia de seguridad en URL de SQL Server](sql-server-backup-to-url.md). Esta característica está disponible en SQL Server 2012 SP1 CU2 o posterior.  
  
    > [!NOTE]  
    >  En el caso de las versiones de SQL Server anteriores a SQL Server 2014, puede usar el complemento SQL Server la herramienta copia de seguridad en Azure para crear de forma rápida y sencilla copias de seguridad en Azure Storage. Para obtener más información, vea [centro de descarga](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Permita SQL Server administrar las copias de seguridad en Azure:** Configure SQL Server para administrar la estrategia de copia de seguridad y programar las copias de seguridad de una sola base de datos, o de varias, o establecer los valores predeterminados en el nivel de instancia. Esta característica se conoce como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**. Para obtener más información, consulte [SQL Server copia de seguridad administrada en Azure](sql-server-managed-backup-to-microsoft-azure.md). Esta característica está disponible en SQL Server 2014 o posterior.  
  
## <a name="benefits-of-using-the-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Ventajas de usar el servicio BLOB de Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para copias de seguridad  
  
-   Almacenamiento fuera de la ubicación flexible, confiable e ilimitado: el almacenamiento de las copias de seguridad en Azure Blob service puede ser una opción externa cómoda, flexible y fácil de acceder. La creación de almacenamiento externo para las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser tan sencillo como modificar los scripts y trabajos existentes. El almacenamiento externo normalmente debe estar lo suficientemente alejado de la base de datos de producción como para impedir que un solo desastre pueda afectar tanto a las ubicaciones de la base de datos de producción como a la externa. La elección de la replicación geográfica en el almacenamiento de blobs permite disponer de un nivel de protección adicional en caso de que se produzca un desastre que pueda afectar a toda la región. Además, las copias de seguridad están disponibles desde cualquier lugar y en cualquier momento y se puede tener acceso a ellas fácilmente para las restauraciones.  
  
-   Archivo de copia de seguridad: el servicio de Azure Blob Storage ofrece una mejor alternativa a la opción de cinta que se suele usar para archivar las copias de seguridad. El almacenamiento en cintas puede requerir transporte físico a unas instalaciones externas y medidas para proteger los soportes. Almacenar las copias de seguridad en Azure Blob Storage ofrece una opción de archivado instantánea, altamente disponible y resistente.  
  
-   Sin sobrecarga de administración de hardware: no existe ninguna sobrecarga de administración de hardware con los servicios de Azure. Los servicios de Azure administran el hardware y ofrecen replicación geográfica para conseguir redundancia y protección contra los errores del hardware.  
  
-   Actualmente, en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caso de instancias de que se ejecutan en una máquina virtual de Azure, se pueden realizar copias de seguridad de los servicios de almacenamiento de blobs de Azure mediante la creación de discos conectados. Sin embargo, existe un límite en cuanto al número de discos que puede conectar a una máquina virtual de Azure. Este límite es de 16 discos para una instancia muy grande e inferior para las instancias menores. Al habilitar una copia de seguridad directa en Azure Blob Storage, puede omitir el límite de 16 discos.  
  
     Además, el archivo de copia de seguridad que ahora se almacena en el servicio de almacenamiento de blobs de Azure está disponible directamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entorno local o en otro que se ejecuta en una máquina virtual de Azure, sin necesidad de adjuntar o separar bases de datos o de descargar y adjuntar el VHD.  
  
-   Ventajas de costo: solo se paga por el servicio que se emplea. Puede ser tan rentable como una opción de archivado de copias de seguridad externa. Consulte la sección [consideraciones de facturación de Azure](#Billing) para obtener más información y vínculos.  
  
##  <a name="Billing"></a>Consideraciones sobre la facturación de Azure:  
 La comprensión de los costos de almacenamiento de Azure le permite predecir el costo de crear y almacenar copias de seguridad en Azure.  
  
 La [calculadora de precios de Azure](https://go.microsoft.com/fwlink/?LinkId=277060) puede ayudar a estimar los costos.  
  
 **Almacenamiento:** Los cargos se basan en el espacio usado y se calculan según una escala graduada y el nivel de redundancia. Para obtener más detalles e información actualizada, vea la sección **Administración de datos** del artículo [Detalles de precios](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Transferencias de datos:** Las transferencias de datos de entrada a Azure son gratis. Las transferencias salientes se cobran por el uso de ancho de banda y se calculan según una escala graduada específica de la región. Para obtener más detalles, vea la sección [Transferencias de datos](https://go.microsoft.com/fwlink/?LinkId=277061) del artículo Detalles de precios.  
  
## <a name="see-also"></a>Véase también  
 [SQL Server procedimientos recomendados y solución de problemas de copia de seguridad en URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: SQL Server copias de seguridad y restauración en Azure Blob Storage Service](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server copia de seguridad en URL](sql-server-backup-to-url.md)  
  

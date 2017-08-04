---
title: "Configuración de clúster de disco compartido para SQL Server en Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Clúster de discos compartidos para SQL Server en Linux

Puede configurar un clúster de alta disponibilidad de almacenamiento compartido con Linux para permitir que la instancia de SQL Server para la conmutación por error de un nodo a otro. En un clúster típico dos o más servidores están conectados al almacenamiento compartido. Los servidores son los nodos del clúster. Los clústeres de conmutación por error proporcionan protección a nivel de instancia para mejorar el tiempo de recuperación gracias a permitir la conmutación por error entre dos o más nodos de SQL Server. Pasos de configuración dependen de la distribución de Linux y soluciones de agrupación en clústeres. En la tabla siguiente identifica los pasos específicos para soluciones de clúster validado.  

|Distribución |Tema 
|----- |-----
|**Red Hat Enterprise Linux con el complemento de alta disponibilidad** |[Configurar](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server con el complemento de alta disponibilidad** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Pasos siguientes



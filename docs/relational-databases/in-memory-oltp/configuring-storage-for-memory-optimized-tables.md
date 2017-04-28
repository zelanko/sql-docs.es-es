---
title: "Configuración del almacenamiento para las tablas con optimización para memoria | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0250c8370960dc17adf13c020c51bfc603b111c8
ms.lasthandoff: 04/11/2017

---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configurar el almacenamiento para las tablas con optimización para memoria
  Debe configurar la capacidad de memoria y las operaciones de entrada/salida por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidad de almacenamiento  
 Use la información de [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para calcular el tamaño en memoria de las tablas durables con optimización para memoria de la base de datos. Puesto que los índices no se conservan en las tablas con optimización para memoria, no incluya el tamaño de los índices. Una vez que determine el tamaño, necesita proporcionar una cantidad de espacio en disco que sea cuatro veces el tamaño de tablas durables en memoria.  
  
## <a name="storage-iops"></a>E/S de almacenamiento por segundo  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] puede aumentar considerablemente el rendimiento de las cargas de trabajo. Por tanto, es importante asegurarse de que la entrada/salida no es un cuello de botella.  
  
-   Al migrar tablas basadas en disco a tablas con optimización para memoria, asegúrese de que el registro de transacciones esté en un medio de almacenamiento que pueda admitir mayor actividad del registro de transacciones. Por ejemplo, si el medio de almacenamiento admite operaciones del registro de transacciones a 100 MB/s, y las tablas con optimización para memoria producen un rendimiento cinco veces mayor, el medio de almacenamiento del registro de transacciones debe poder admitir una mejora del rendimiento cinco veces mayor para evitar que la actividad del registro de transacciones se convierta en un cuello de botella.  
  
-   Las tablas con optimización para memoria se conservan en archivos distribuidos en uno o varios contenedores. Cada contenedor se debe asignar normalmente a su propio eje, y se usa tanto para aumentar la capacidad de almacenamiento como para mejorar las E/S por segundo. Debe asegurarse que la IOPS secuencial del medio de almacenamiento puede admitir que se triplique el rendimiento del registro de transacciones.  
  
     Por ejemplo, si las tablas con optimización para memoria generan 500 MB/s de actividad en el registro de transacciones, el almacenamiento de las tablas con optimización para memoria debe admitir 1,5 GB/s de E/S por segundo. La necesidad de admitir el triple de rendimiento del registro de transacciones procede de la observación de que los pares de archivos de datos y delta se escriben primero con los datos iniciales y después se deben leer/volver a escribir como parte de una operación de mezcla.  
  
     Otro factor que hay que tener en cuenta para las E/S por segundo del almacenamiento es el tiempo de recuperación de las tablas con optimización para memoria. Los datos de las tablas durables se deben leer en memoria antes de que una base de datos esté a disposición de las aplicaciones. Normalmente, la carga de datos en las tablas con optimización para memoria se puede realizar a la velocidad de la IOPS. Por tanto, si el almacenamiento total de las tablas durables con optimización para memoria es de 60 GB y desea poder cargar estos datos en 1 minuto, la IOPS para el almacenamiento se debe establecer en 1 GB/s.  
  
-   Si tiene un número par de ejes, a diferencia de SQL Server 2014, los archivos de punto de control se distribuirán uniformemente a través de todos los ejes.  
  
## <a name="encryption"></a>Cifrado  
 En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se cifrará el almacenamiento de tablas con optimización para memoria como parte de la habilitación de TDE en la base de datos. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  

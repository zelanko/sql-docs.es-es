---
title: "Dispositivo de copia de seguridad (página Contenido de los medios) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.backupdevice.contents.f1
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bfa385cab6527c16e62e2e631b9ffa1b96e0d10
ms.lasthandoff: 04/11/2017

---
# <a name="backup-device-media-contents-page"></a>Dispositivo de copia de seguridad (página Contenido de los medios)
  Utilice el cuadro de diálogo **Dispositivo de copia de seguridad** para ver la información acerca de la copia de seguridad. Esta información describe el dispositivo, el medio, el conjunto de medios y los conjuntos de copias de seguridad.  
  
 **Para utilizar SQL Server Management Studio a fin de ver el contenido de un dispositivo de copia de seguridad**  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opciones  
 Vea la información acerca del medio individual, el conjunto de medios y los conjuntos de copias de seguridad.  
  
 **Multimedia**  
 Disco o conjunto de cintas donde se almacena la información de la copia de seguridad.  
  
 **Secuencia del medio**  
 Proporciona el número de secuencia del medio, el número de secuencia de la familia y el identificador del reflejo, si existe alguno. El medio físico de copia de seguridad se etiqueta con un número de secuencia que indica el orden en el que se utilizó el medio. El medio de copia de seguridad inicial se etiqueta con 1, el segundo (la primera cinta de continuación) se etiqueta con 2, y así sucesivamente. Cuando restaure el conjunto de copias de seguridad, asegúrese de que el operador que restaura la copia de seguridad coloca los medios correctos en el orden correcto.  
  
 **Creado el**  
 Muestra la fecha y la hora de creación del conjunto de medios.  
  
 **Conjunto de medios**  
 Un conjunto de medios es una colección ordenada de medios de copia de seguridad en la que se han grabado una o más operaciones de copia de seguridad mediante un número constante de dispositivos pertinentes.  
  
 **Nombre**  
 Muestra el nombre del conjunto de medios, si existe alguno.  
  
 **Descripción**  
 Muestra la descripción del conjunto de medios, si existe alguno.  
  
 **Recuento de la familia de medios**  
 Muestra el número de familias del conjunto de medios. Cada conjunto de medios es una colección de una o más familias de medios. Toda la salida a un único dispositivo de copia de seguridad determinado (o grupo de dispositivos de copia de seguridad reflejados) forma una única familia de medios. Cada conjunto de medios contiene una familia de medios por dispositivo (o grupo de dispositivos reflejados); por ejemplo, si un conjunto de medios utiliza dos dispositivos de copia de seguridad no reflejos, el conjunto de medios contiene dos familias de medios.  
  
 **Conjuntos de copia de seguridad**  
 Muestra la información acerca del conjunto o conjuntos de copia de seguridad que contiene el medio. Un conjunto de copia de seguridad es el resultado de una operación de copia de seguridad correcta, cuyo contenido se distribuye entre los medios del conjunto de dispositivos de copia de seguridad.  
  
|Encabezado|Valores|  
|------------|------------|  
|**Nombre**|Nombre del conjunto de copia de seguridad.|  
|**Tipo**|Objeto del que se realizó una copia de seguridad: Base de datos, Archivo o *en blanco>\<* (para registros de transacciones).|  
|**Componente**|Tipo de copia de seguridad realizada: Completa, Diferencial o Registro de transacciones.|  
|**Server**|Nombre de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la operación de copia de seguridad.|  
|**Base de datos**|Nombre de la base de datos de la que se realizó la copia de seguridad.|  
|**Posición**|Posición del conjunto de copias de seguridad en el volumen.|  
|**Date**|Fecha y hora en la que finalizó la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
|**Tamaño**|Tamaño del conjunto de copias de seguridad, en bytes.|  
|**Nombre de usuario**|Nombre del usuario que realizó la operación de copia de seguridad.|  
|**Expiración**|Fecha y hora de expiración del conjunto de copias de seguridad.|  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

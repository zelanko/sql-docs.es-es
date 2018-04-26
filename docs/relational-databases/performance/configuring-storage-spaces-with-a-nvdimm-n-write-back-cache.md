---
title: Configuración de espacios de almacenamiento con una caché con reescritura de NVDIMM-N | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d24f8c39d4ab76c7887fb100a6235a1a8d775279
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>Configuring Storage Spaces with a NVDIMM-N write-back cache (Configuración de espacios de almacenamiento con una caché con reescritura de NVDIMM-N)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows Server 2016 es compatible con dispositivos de NVDIMM-N que permiten operaciones de entrada y salida (E/S) extremadamente rápidas. Una manera atractiva de usar dichos dispositivos es usarlos como una memoria caché con reescritura para obtener latencias de escritura bajas. En este tema se describe cómo configurar un espacio de almacenamiento reflejado con una caché con reescritura reflejada de NVDIMM-N como una unidad virtual para almacenar el registro de transacciones de SQL Server. Si quiere usarlo también para almacenar tablas de datos u otros datos, puede incluir más discos en el grupo de almacenamiento o crear varios grupos si el aislamiento es importante.  
  
 Para ver un vídeo de Channel 9 con esta técnica, vea [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016 (Usar una memoria no volátil (NVDIMM-N) como almacenamiento en bloque en Windows Server 2016)](https://channel9.msdn.com/Events/Build/2016/P466).  
  
## <a name="identifying-the-right-disks"></a>Identificación de los discos correctos  
 La configuración de los espacios de almacenamiento en Windows Server 2016, especialmente con las características avanzadas como las memorias caché con reescritura, se consigue más fácilmente mediante PowerShell. El primer paso es identificar qué discos deben formar parte del grupo de espacios de almacenamiento del que se creará el disco virtual. Los NVDIMM-N tienen un tipo de medio y un tipo de bus de SCM (memoria de clase de almacenamiento), que puede consultarse mediante el cmdlet Get-PhysicalDisk de PowerShell.  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  Con los dispositivos de NVDIMM-N, ya no necesitará seleccionar específicamente los dispositivos que pueden ser destinos de memoria caché con reescritura.  
  
 Para crear un disco virtual reflejado con una memoria caché con reescritura reflejada, se necesitan al menos 2 NVDIMM-N y otros 2 discos. Asignar los discos físicos deseados a una variable antes de crear el grupo facilita el proceso.  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 La captura de pantalla muestra la variable $pd y las 2 SSD, y 2 NVDIMM-N que se asignan para devolverse con el siguiente cmdlet de PowerShell.  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Select FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## <a name="creating-the-storage-pool"></a>Crear el grupo de almacenamiento  
 Al usar la variable $pd que contiene los discos físicos, es sencillo crear el grupo de almacenamiento mediante el cmdlet New-StoragePool de PowerShell.  
  
```  
New-StoragePool –StorageSubSystemFriendlyName “Windows Storage*” –FriendlyName NVDIMM_Pool –PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>Crear el disco virtual y el volumen  
 Ahora que se ha creado un grupo, el siguiente paso es delimitar un disco virtual y aplicarle formato. En este caso, solo se creará un disco virtual y el cmdlet New-Volume de PowerShell puede usarse para simplificar este proceso:  
  
```  
New-Volume –StoragePool (Get-StoragePool –FriendlyName NVDIMM_Pool) –FriendlyName Log_Space –Size 300GB –FileSystem NTFS –AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 El disco virtual se ha creado, inicializado y se le ha aplicado formato con NTFS. La siguiente captura de pantalla muestra que tiene un tamaño de 300 GB y un tamaño de memoria caché de escritura de 1 GB, que se hospedará en los NVDIMM-N.  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 Ahora puede ver este nuevo volumen en su servidor. Ahora puede usar esta unidad para el registro de transacciones de SQL Server.  
  
 ![Log_Space Drive](../../relational-databases/performance/media/log-space-drive.png "Log_Space Drive")  
  
## <a name="see-also"></a>Ver también  
 [Espacios de almacenamiento en Windows 10](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)   
 [Introducción a los espacios de almacenamiento](https://technet.microsoft.com/en-us/library/hh831739.aspx)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  

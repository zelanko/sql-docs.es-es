---
title: Dispositivo de copia de seguridad (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a4f23fd3d6d8208410c520676ee4e0c8bbe00fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922146"
---
# <a name="backup-device-general-page"></a>Dispositivo de copia de seguridad (página General)
  Utilice la página **General** para especificar o ver las propiedades generales de un dispositivo lógico de copia de seguridad.  
  
 **Para utilizar SQL Server Management Studio a fin de ver el contenido de un dispositivo de copia de seguridad**  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opciones  
 **Nombre de dispositivo**  
 Muestra el nombre de un dispositivo lógico de copia de seguridad existente o especifica el nombre de un dispositivo lógico de copia de seguridad nuevo.  
  
 **Cinta**  
 Muestra o selecciona el dispositivo de cinta de destino en la lista **Cinta** . Esta opción solo está disponible si hay una unidad de cinta conectada al equipo que ejecuta la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  Los dispositivos de copia de seguridad en cinta de equipos remotos no son destinos de copia de seguridad válidos.  
  
 **Archivo**  
 Muestra el archivo de destino de un dispositivo lógico de copia de seguridad existente o especifica un archivo de destino para un dispositivo lógico de copia de seguridad nuevo.  
  
-   En un dispositivo lógico de copia de seguridad existente, se muestra la ruta de acceso del archivo de copia de seguridad. El campo **Archivo** no se puede editar y el botón Examinar no está disponible.  
  
-   En un dispositivo lógico de copia de seguridad nuevo, debe proporcionar la ruta de acceso del archivo de copia de seguridad para el que define dicho dispositivo lógico. Este archivo no tiene por qué existir aún.  
  
     Para especificar un archivo de copia de seguridad local, puede hacer clic en el botón Examinar, situado a la derecha del cuadro de texto **Archivo** . A continuación, en el cuadro de diálogo **Buscar archivos de base de datos** , puede navegar a cualquier ubicación de las unidades fijas del equipo que ejecuta la instancia del servidor. Si el archivo de copia de seguridad no existe aún, debe escribir el nombre de archivo que desea utilizar en el campo **Nombre de archivo** del cuadro de diálogo.  
  
     Asimismo, puede editar el campo **Archivo** manualmente para reemplazar la ruta de acceso, el nombre de archivo y la extensión predeterminados. Para especificar un archivo remoto como destino de copia de seguridad, escriba su nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md).  
  
    > [!IMPORTANT]  
    >  La realización de copias de seguridad de datos a través de una red está expuesta a errores; una vez completada, es recomendable comprobar la operación de copia de seguridad. Para obtener más información, vea [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
## <a name="remarks"></a>Observaciones  
 Las copias de seguridad de uno o varios dispositivos de copia de seguridad constituyen un solo conjunto de medios. Un *conjunto de medios* es una colección ordenada de medios de copia de seguridad, cintas o archivos de disco en la que se han escrito una o más operaciones de copia de seguridad mediante un tipo y un número fijos de dispositivos de copia de seguridad. Para obtener más información sobre los conjuntos de medios, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 El dispositivo físico de copia de seguridad correspondiente a un dispositivo lógico de copia de seguridad se inicializa cuando la primera copia de seguridad del conjunto de medios se escribe en el dispositivo lógico. Si el dispositivo físico de copia de seguridad es un archivo que aún no existe, se crea en ese momento.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

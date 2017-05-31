---
title: Seleccionar destino de la copia de seguridad | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dd0f291ca7863b653546243d18c3a289f1551a41
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="select-backup-destination"></a>Seleccionar destino de la copia de seguridad
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Utilice el cuadro de diálogo **Seleccionar destino de la copia de seguridad** para seleccionar un dispositivo como destino de la copia de seguridad. Un destino de la copia de seguridad puede ser un disco o un dispositivo lógico de copia de seguridad.  
  
 **Para utilizar SQL Server Management Studio a fin de realizar una copia de seguridad de una base de datos**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Opciones  
 Las opciones de este cuadro de diálogo dependen de si ha seleccionado o no un destino en disco o en cinta.  
  
 **Destinos en disco**  
 Para especificar un destino de copia de seguridad, elija una de las opciones siguientes:  
  
|||  
|-|-|  
|**Nombre de archivo**|Elija esta opción para especificar un archivo local o remoto como destino de la copia de seguridad en el cuadro de texto para:<br /><br /> Especificar un archivo local, haga clic en el botón Examinar a la derecha del cuadro de texto y navegue hasta un archivo de las unidades fijas del equipo en el que se ejecuta el servidor, o bien especifique directamente la ruta de acceso completa y el nombre de archivo; por ejemplo, `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Especificar un archivo remoto como destino de copia de seguridad, escriba su nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).<br /><br /> <br /><br /> **\*\* Importante \*\*** La realización de copias de seguridad de datos a través de una red está expuesta a errores; una vez completada, es recomendable comprobar la operación de copia de seguridad. Para obtener más información, vea [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).|  
|**Dispositivo de copia de seguridad**|Elija esta opción para seleccionar un dispositivo lógico de copia de seguridad.<br /><br /> Nota: Para obtener más información sobre cómo crear un dispositivo de copia de seguridad de disco, vea [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Destinos en cinta**  
 Especifique un destino de la copia de seguridad en una unidad de cinta, conectada físicamente al equipo en el que se ejecuta el servidor (es decir, la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Elija una de las opciones siguientes:  
  
|||  
|-|-|  
|**Unidad de cinta**|Elija esta opción para seleccionar una unidad de cinta como destino de la copia de seguridad en la lista de unidades de cinta, conectadas físicamente al equipo en el que se ejecuta la instancia del servidor.<br /><br /> Nota: Los dispositivos de copia de seguridad en cinta de equipos remotos no son destinos de copia de seguridad válidos.|  
|**Dispositivo de copia de seguridad**|Elija esta opción para seleccionar un dispositivo lógico de copia de seguridad existente. Estos dispositivos lógicos de copia de seguridad corresponden a unidades de cinta que están físicamente conectadas al equipo en el que se ejecuta la instancia del servidor.<br /><br /> Nota: Para obtener más información sobre cómo crear un dispositivo de copia de seguridad de cinta, vea [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

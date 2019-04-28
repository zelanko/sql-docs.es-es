---
title: Seleccionar destino de la copia de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d9b4a0e07f32e074ff7e8875c263615bcebc12d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874880"
---
# <a name="select-backup-destination"></a>Seleccionar destino de la copia de seguridad
  Utilice el cuadro de diálogo **Seleccionar destino de la copia de seguridad** para seleccionar un dispositivo como destino de la copia de seguridad. Un destino de la copia de seguridad puede ser un disco o un dispositivo lógico de copia de seguridad.  
  
 **Para utilizar SQL Server Management Studio a fin de realizar una copia de seguridad de una base de datos**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Opciones  
 Las opciones de este cuadro de diálogo dependen de si ha seleccionado o no un destino en disco o en cinta.  
  
 **Destinos en disco**  
 Para especificar un destino de copia de seguridad, elija una de las opciones siguientes:  
  
|||  
|-|-|  
|**Nombre de archivo**|Elija esta opción para especificar un archivo local o remoto como destino de la copia de seguridad en el cuadro de texto.<br /><br /> Para especificar un archivo local, haga clic en el botón Examinar a la derecha del cuadro de texto y navegar a un archivo en las unidades fijas del equipo que ejecuta el servidor o escriba la ruta de acceso completa y nombre de archivo directamente; Por ejemplo, `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Para especificar un archivo remoto como destino de copia de seguridad, escriba su nombre UNC (convención de nomenclatura universal) completo. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md).<br /><br /> **\*\* Importante \*\*** La realización de copias de seguridad de datos a través de una red está expuesta a errores; una vez completada, es recomendable comprobar la operación de copia de seguridad. Para obtener más información, vea [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).|  
|**Dispositivo de copia de seguridad**|Elija esta opción para seleccionar un dispositivo lógico de copia de seguridad.<br /><br /> Nota: Para obtener información acerca de cómo crear un dispositivo de copia de seguridad de disco, consulte [definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Destinos en cinta**  
 Especifique un destino de la copia de seguridad en una unidad de cinta, conectada físicamente al equipo en el que se ejecuta el servidor (es decir, la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Elija una de las opciones siguientes:  
  
|||  
|-|-|  
|**Unidad de cinta**|Elija esta opción para seleccionar una unidad de cinta como destino de la copia de seguridad en la lista de unidades de cinta, conectadas físicamente al equipo en el que se ejecuta la instancia del servidor.<br /><br /> Nota: Los dispositivos de copia de seguridad en cinta de equipos remotos no son destinos de copia de seguridad válidos.|  
|**Dispositivo de copia de seguridad**|Elija esta opción para seleccionar un dispositivo lógico de copia de seguridad existente. Estos dispositivos lógicos de copia de seguridad corresponden a unidades de cinta que están físicamente conectadas al equipo en el que se ejecuta la instancia del servidor.<br /><br /> Nota: Para obtener información acerca de cómo crear un dispositivo de copia de seguridad en cinta, consulte [definir un dispositivo lógico de copia de seguridad para una unidad de cinta &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

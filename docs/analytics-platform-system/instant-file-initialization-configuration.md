---
title: Configurar la inicialización instantánea de archivos - Analytics Platform System | Microsoft Docs
description: Configure la inicialización instantánea de archivos en Analytics Platform System. Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298116"
---
# <a name="instant-file-initialization-configuration"></a>Configuración de la inicialización instantánea de archivos
Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente. Activando la casilla para activar la inicialización instantánea de archivos mejorará el rendimiento de SQL Server PDW. Sin embargo, si esto supone un riesgo de seguridad para usted empresariales, a continuación, deje la casilla desactivada.  
  
> [!IMPORTANT]  
> Cuando se habilita la inicialización instantánea de archivos, SQL Server no sobrescribe los bits eliminados con ceros.  Este comportamiento podría producir una vulnerabilidad de seguridad si usuarios no autorizados obtienen acceso a los datos eliminados. Sin embargo, SQL Server PDW mitiga este riesgo asegurándose de que los archivos de copia de seguridad y la base de datos de SQL Server siempre se asocia a una instancia de SQL Server; solo la cuenta de servicio de SQL Server y el administrador local pueden tener acceso a los datos eliminados en PDW de SQL Server.  
  
La inicialización instantánea de archivos no está disponible cuando el TDE está habilitado.  
  
## <a name="add-permission-for-the-backup-account"></a>Agregue el permiso para la cuenta de copia de seguridad  
El proceso de copia de seguridad requiere una credencial de red (cuenta de usuario de Windows) que puede tener acceso a la ubicación de almacenamiento de copia de seguridad. Autorizar PDW para utilizar la cuenta mediante el [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento. Consulte [copia de seguridad de la base de datos](../t-sql/statements/backup-database-parallel-data-warehouse.md) para todo el proceso de copia de seguridad. Para usar la inicialización instantánea de archivos, la cuenta de copia de seguridad debe tener el `Perform volume maintenance tasks` permiso.  
  
1.  En el servidor de copia de seguridad, abra el **directiva de seguridad Local** aplicación (`secpol.msc`).  
  
2.  En el panel izquierdo, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel derecho, haga doble clic en **Realizar tareas de mantenimiento del volumen**.  
  
4.  Haga clic en **Agregar usuario o grupo** y añada las cuentas de usuario que se utilicen para las copias de seguridad.  
  
5.  Haga clic en **Aplicar**y, a continuación, cierre todos los cuadros de diálogo de **Directiva de seguridad local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para activar o desactivar la inicialización instantánea de archivos  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, haga clic en **inicialización instantánea de archivos**.  
  
3.  Para activar la inicialización instantánea de archivos, active la casilla junto a **habilitar la inicialización instantánea de archivos en todos los nodos**. Para desactivar la inicialización instantánea de archivos, desactive la casilla junto a **habilitar la inicialización instantánea de archivos en todos los nodos**.  
  
    > [!WARNING]  
    > Cuando se desactiva la inicialización instantánea de archivos, la consideración de seguridad descrita anteriormente para la característica todavía puede aplicarse a los archivos eliminados mientras se habilitaba la inicialización instantánea de archivos.  
  
4.  Haga clic en **Aplicar**. El cambio se propagará a través de las instancias de SQL Server en PDW de SQL Server la próxima vez que se reinician los servicios del dispositivo. Para reiniciar los servicios del dispositivo, consulte [estado de servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Es posible que desea repetir los pasos descritos anteriormente como **agregar permisos para la cuenta de copia de seguridad** para quitar el **realizar tareas de mantenimiento de volumen** permiso.  
  
![Inicialización de archivos instantánea PDW del dispositivo de DWConfig](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obtener más información sobre la inicialización instantánea de archivos, consulte [inicialización instantánea de archivos](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  

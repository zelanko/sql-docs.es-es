---
title: Configurar la inicialización instantánea de archivos - sistema de la plataforma de análisis | Documentos de Microsoft
description: Configurar la inicialización instantánea de archivos de sistema de la plataforma de análisis. Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f2c1e0e17e2cbfb5816632a25ecdebe5d92ee024
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34706753"
---
# <a name="instant-file-initialization-configuration"></a>Configuración de la inicialización instantánea de archivos
Inicialización instantánea de archivos es una característica de SQL Server que permite que las operaciones de archivo de datos se ejecute más rápidamente. Seleccione la casilla para activar la inicialización instantánea de archivos mejorará el rendimiento de SQL Server PDW. Sin embargo, si esto supone un riesgo de seguridad para su negocio, a continuación, deje la casilla desactivada.  
  
> [!IMPORTANT]  
> Cuando se habilita la inicialización instantánea de archivos, SQL Server no se sobrescribe bits eliminadas con ceros.  Este comportamiento podría crear una vulnerabilidad de seguridad si usuarios no autorizados obtienen acceso a los datos eliminados. Sin embargo, SQL Server PDW mitiga este riesgo asegurándose de que los archivos de copia de seguridad y la base de datos de SQL Server siempre se asocia a una instancia de SQL Server; sólo la cuenta de servicio de SQL Server y al administrador local en el que se pueden tener acceso a los datos eliminados en PDW de SQL Server.  
  
La inicialización instantánea de archivos no está disponible cuando el TDE está habilitado.  
  
## <a name="add-permission-for-the-backup-account"></a>Agregue el permiso para la cuenta de copia de seguridad  
El proceso de copia de seguridad requiere una credencial de red (cuenta de usuario de Windows) que puede tener acceso a la ubicación de almacenamiento de copia de seguridad. Autorizar PDW para utilizar la cuenta mediante la [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento. Vea [copia de seguridad de la base de datos](../t-sql/statements/backup-database-parallel-data-warehouse.md) para todo el proceso de copia de seguridad. Para usar la inicialización instantánea de archivos, la cuenta de copia de seguridad debe tener el `Perform volume maintenance tasks` permiso.  
  
1.  En el servidor de copia de seguridad, abra el **directiva de seguridad Local** aplicación (`secpol.msc`).  
  
2.  En el panel izquierdo, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel derecho, haga doble clic en **Realizar tareas de mantenimiento del volumen**.  
  
4.  Haga clic en **Agregar usuario o grupo** y añada las cuentas de usuario que se utilicen para las copias de seguridad.  
  
5.  Haga clic en **Aplicar**y, a continuación, cierre todos los cuadros de diálogo de **Directiva de seguridad local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para activar o desactivar la inicialización instantánea de archivos  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, haga clic en **Instant File Initialization**.  
  
3.  Para activar la inicialización instantánea de archivos, active la casilla junto a **habilitar la inicialización instantánea de archivos en todos los nodos**. Para desactivar la inicialización instantánea de archivos, desactive la casilla junto a **habilitar la inicialización instantánea de archivos en todos los nodos**.  
  
    > [!WARNING]  
    > Al desactivar la inicialización instantánea de archivos, la consideración de seguridad descrita anteriormente para la característica aún puede aplicarse a los archivos eliminados mientras se habilitaba la inicialización instantánea de archivos.  
  
4.  Haga clic en **Aplicar**. El cambio se propagará a través de las instancias de SQL Server en PDW de SQL Server la próxima vez que se reinicien los servicios del dispositivo. Para reiniciar los servicios del dispositivo, consulte [estado de los servicios PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Puede repetir los pasos descritos anteriormente como **agregar permisos para la cuenta de copia de seguridad** para quitar el **realizar tareas de mantenimiento del volumen** permiso.  
  
![Dispositivo de DWConfig PDW momento de inicialización de archivos](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obtener más información sobre la inicialización instantánea de archivos, consulte [Instant File Initialization](http://technet.microsoft.com/library/ms175935(v=SQL.105).aspx).  
  

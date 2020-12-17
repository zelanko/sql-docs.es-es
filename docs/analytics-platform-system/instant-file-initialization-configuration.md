---
title: Configurar la inicialización instantánea de archivos
description: Configure la inicialización instantánea de archivos en Analytics Platform System. La inicialización instantánea de archivos es una característica SQL Server que permite que las operaciones de archivo de datos se ejecuten más rápidamente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6843efa430fcd43149d048c9d21c5120954ab896
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/17/2020
ms.locfileid: "97637821"
---
# <a name="instant-file-initialization-configuration"></a>Configuración de inicialización instantánea de archivos
La inicialización instantánea de archivos es una característica SQL Server que permite que las operaciones de archivo de datos se ejecuten más rápidamente. Si activa la casilla para activar la inicialización instantánea de archivos, se mejorará el rendimiento de PDW de SQL Server. Sin embargo, si esto supone un riesgo de seguridad para su negocio, deje la casilla desactivada.  
  
> [!IMPORTANT]  
> Cuando la inicialización instantánea de archivos está habilitada, SQL Server no sobrescribe los bits eliminados con ceros.  Este comportamiento podría crear una vulnerabilidad de seguridad si los usuarios no autorizados obtienen acceso a los datos eliminados. Sin embargo, PDW de SQL Server mitiga este riesgo asegurándose de que los archivos de copia de seguridad y la base de datos de SQL Server siempre se adjunten a una instancia de SQL Server; solo la cuenta de servicio de SQL Server y el administrador local pueden tener acceso a los datos eliminados en PDW de SQL Server.  
  
La inicialización instantánea de archivos no está disponible cuando el TDE está habilitado.  
  
## <a name="add-permission-for-the-backup-account"></a>Agregar permiso para la cuenta de copia de seguridad  
El proceso de copia de seguridad requiere una credencial de red (cuenta de usuario de Windows) que puede tener acceso a la ubicación de almacenamiento de copia de seguridad. Puede autorizar a PDW para que use la cuenta mediante el procedimiento [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) . Vea [backup Database](../t-sql/statements/backup-transact-sql.md) para todo el proceso de copia de seguridad. Para usar la inicialización instantánea de archivos, se debe conceder el permiso a la cuenta de copia de seguridad `Perform volume maintenance tasks` .  
  
1.  En el servidor de copia de seguridad, abra la aplicación de **Directiva de seguridad local** ( `secpol.msc` ).  
  
2.  En el panel izquierdo, expanda **Directivas locales** y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel derecho, haga doble clic en **Realizar tareas de mantenimiento del volumen**.  
  
4.  Haga clic en **Agregar usuario o grupo** y añada las cuentas de usuario que se utilicen para las copias de seguridad.  
  
5.  Haga clic en **Aplicar** y, a continuación, cierre todos los cuadros de diálogo de **Directiva de seguridad local** .  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>Para activar o desactivar la inicialización instantánea de archivos  
  
1.  Inicie el Configuration Manager. Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Configuration Manager, haga clic en **inicialización instantánea de archivos**.  
  
3.  Para activar la inicialización instantánea de archivos, active la casilla situada junto a **Habilitar la inicialización instantánea de archivos en todos los nodos**. Para desactivar la inicialización instantánea de archivos, desactive la casilla situada junto a **Habilitar la inicialización instantánea de archivos en todos los nodos**.  
  
    > [!WARNING]  
    > Al desactivar la inicialización instantánea de archivos, es posible que la consideración de seguridad descrita anteriormente para la característica se siga aplicando a los archivos eliminados mientras se habilitaba la inicialización instantánea de archivos.  
  
4.  Haga clic en **Aplicar**. El cambio se propagará a través de las instancias de SQL Server en PDW de SQL Server la próxima vez que se reinicien los servicios de la aplicación. Para reiniciar los servicios del dispositivo ahora, consulte el estado de los [servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).  
  
5.  Puede que desee repetir los pasos descritos anteriormente como **permiso de agregar para la cuenta de copia de seguridad** para quitar el permiso **realizar tareas de mantenimiento del volumen** .  
  
![Inicialización instantánea de archivos PDW del dispositivo de DWConfig](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
Para obtener más información acerca de la inicialización instantánea de archivos, consulte [inicialización instantánea de archivos](/previous-versions/sql/sql-server-2008-r2/ms175935(v=sql.105)).  

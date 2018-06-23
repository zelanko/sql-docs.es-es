---
title: Propiedades del servidor (página Configuración de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9d44381ef0af703efb104a38f5eeebf99fc21ff7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107293"
---
# <a name="server-properties-database-settings-page"></a>Propiedades del servidor (página Configuración de base de datos)
  Utilice esta página para ver o modificar la configuración de la base de datos.  
  
## <a name="options"></a>Opciones  
 **Factor predeterminado de relleno de índices**  
 Especifica cuánto se debe llenar cada página de índice de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se crea un nuevo índice con los datos existentes. El factor de relleno influye en el rendimiento, ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe dedicar tiempo a dividir las páginas cuando se rellenan.  
  
 El valor predeterminado es 0; los valores válidos son los comprendidos entre 0 y 100. Un factor de relleno de 0 o 100 crea índices clúster con páginas de datos llenas e índices no clúster con páginas hoja llenas, pero deja algo de espacio en el nivel superior del árbol del índice. Los valores de factor de relleno 0 y 100 son idénticos en todos los sentidos.  
  
 El uso de valores pequeños para el factor de relleno hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cree índices con páginas que no están llenas. Cada uno de los índices ocupa más espacio de almacenamiento, lo que permite que haya espacio para las inserciones posteriores sin necesidad de dividir páginas.  
  
 **Esperar indefinidamente**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no superará nunca el tiempo de espera para una nueva cinta de copia de seguridad.  
  
 **Intentarlo una vez**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] superará el tiempo de espera si una cinta de copia de seguridad no está disponible cuando sea necesaria.  
  
 **Intentarlo durante (minutos)**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] superará el tiempo de espera si una cinta de copia de seguridad no está disponible en el período de tiempo especificado.  
  
 **Tiempo predeterminado de retención de medios de copia de seguridad (días)**  
 Proporciona un valor predeterminado para todo el sistema relativo a cuánto tiempo se conservará cada medio de copia de seguridad una vez que se haya utilizado para una copia de seguridad de base de datos o de registro de transacciones. Esta opción ayuda a proteger las copias de seguridad para que no puedan sobrescribirse hasta que haya transcurrido el número de días especificado.  
  
 **Comprimir copia de seguridad**  
 En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o versiones posteriores), indica el valor actual de la opción **compresión de copia de seguridad predeterminada** . Esta opción determina el valor predeterminado de nivel de servidor para comprimir copias de seguridad, como sigue:  
  
-   Si la casilla **Comprimir copia de seguridad** se deja en blanco, las nuevas copias de seguridad no se comprimirán de forma predeterminada.  
  
-   Si la casilla **Comprimir copia de seguridad** se activa, las nuevas copias de seguridad se comprimirán de forma predeterminada.  
  
    > [!IMPORTANT]  
    >  De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar adversamente a las operaciones simultáneas. Por consiguiente, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.  
  
 Si es miembro del rol fijo de servidor **sysadmin** o **serveradmin** , puede cambiar el valor haciendo clic en el cuadro **Comprimir copia de seguridad** .  
  
 Para obtener más información, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](view-or-configure-the-backup-compression-default-server-configuration-option.md) y [Compresión de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Intervalo de recuperación (min.)**  
 Establece el número máximo de minutos por base de datos para recuperar bases de datos. El valor predeterminado es 0, que indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]lo configura automáticamente. En la práctica, esto significa un tiempo de recuperación inferior a un minuto y un punto de comprobación aproximadamente cada minuto para bases de datos activas. Para más información, consulte [Configure the recovery interval Server Configuration Option](configure-the-recovery-interval-server-configuration-option.md).  
  
 **Data**  
 Especifica la ubicación predeterminada de los archivos de datos. Haga clic en el botón de examinar para navegar a la nueva ubicación predeterminada. No surte efecto hasta que se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Log**  
 Especifica la ubicación predeterminada de los archivos de registro. Haga clic en el botón de examinar para navegar a la nueva ubicación predeterminada. No surte efecto hasta que se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valores configurados**  
 Muestra los valores configurados para las opciones de este panel. Si cambia estos valores, haga clic en **Valores actuales** para comprobar si los cambios han surtido efecto. Si no han surtido efecto, deberá reiniciarse primero la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valores actuales**  
 Presenta los valores actuales de las opciones de este panel. Estos valores son de solo lectura.  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  
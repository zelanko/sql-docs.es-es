---
title: Ver el informe de trasvase de registros (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing log shipping reports
- displaying log shipping reports
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], viewing reports
ms.assetid: 3b549f2f-3683-45e5-b8e8-8095276c41ab
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8e0118573919f4ad1278bfc6b507769b92fe80ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102902"
---
# <a name="view-the-log-shipping-report-sql-server-management-studio"></a>Ver el informe de trasvase de registros (SQL Server Management Studio)
  En este tema se describe cómo ver el informe de estado de trasvase del registro de transacciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puede ejecutar un informe de estado en un servidor de supervisión, un servidor principal o un servidor secundario. Para obtener la información más completa sobre la configuración del trasvase del registro, vea el informe en la instancia del servidor de supervisión.  
  
 El informe muestra el estado de cualquier actividad de trasvase del registro cuyo estado esté disponible desde la instancia de servidor a la que esté conectado. Si esa instancia de servidor se utiliza en varias configuraciones con distintos roles (por ejemplo, actuar como servidor de supervisión para una base de datos y como secundario para otra base de datos), los resultados mostrados contendrán la información de cada configuración desde el punto de vista de cada rol. Si el procedimiento almacenado puede conectarse a la instancia de servidor de supervisión para determinada configuración del trasvase del registro, el informe muestra un estado adicional para dicha configuración.  
  
 Para cada rol que desempeñe la instancia de servidor actual se puede ver la siguiente información:  
  
|Rol|Información mostrada|  
|----------|---------------------------|  
|Monitor|El nombre y el estado de cada servidor principal y cada servidor secundario que utiliza esta instancia de servidor como su servidor de supervisión.|  
|Principal|Para cada base de datos principal, el nombre y el estado de la instancia de servidor actual (como servidor primario), junto con el nombre de la base de datos principal. El informe muestra el estado del trabajo de copia de seguridad (que se almacena localmente en el servidor principal).<br /><br /> El informe contiene además una fila por cada uno de los servidores secundarios correspondientes. Si la configuración utiliza un servidor de supervisión y el procedimiento almacenado puede conectarse a dicho servidor, estas filas muestran el estado de copia y el estado de restauración del registro de copia de seguridad más reciente.|  
|Secundario|Para cada base de datos secundaria, el nombre y el estado de la instancia de servidor actual (como servidor secundario), junto con el nombre de la base de datos secundaria.<br /><br /> El informe muestra el estado de los trabajos de copia y restauración en el servidor secundario.<br /><br /> El informe contiene además una fila para el servidor principal correspondiente. Si la configuración utiliza un servidor de supervisión y el procedimiento almacenado puede conectarse a dicho servidor, esta fila muestra el estado del registro de la copia de seguridad más reciente.|  
  
 La información mostrada depende de si la instancia de servidor es un servidor de supervisión, un servidor principal o un servidor secundario. Si no hay información disponible, las celdas correspondientes aparecen en gris.  
  
 El informe llama a **sp_help_log_shipping_monitor** para obtener los datos. Para obtener información sobre los permisos necesarios, vea [sp_help_log_shipping_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql).  
  
### <a name="to-display-the-transaction-log-shipping-status-report-on-a-server-instance"></a>Para mostrar el informe de estado de trasvase del registro de transacciones en una instancia de servidor  
  
1.  Conéctese a un servidor de supervisión, un servidor principal o un servidor secundario.  
  
2.  Haga clic con el botón derecho en la instancia del servidor del Explorador de objetos, seleccione **Informes**e **Informes estándar**.  
  
3.  Haga clic en **Estado de trasvase del registro de transacciones**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el trasvase de registros &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
  

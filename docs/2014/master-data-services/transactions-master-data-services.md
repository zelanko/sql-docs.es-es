---
title: Transacciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 33b5bab2bb9d812686b6afbc65e0a8292247634b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129055"
---
# <a name="transactions-master-data-services"></a>Transacciones (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], se registra una transacción cada vez que se realiza una acción en un miembro. Todos los usuarios pueden ver las transacciones y los administradores pueden invertirlas. Las transacciones muestran la fecha, la hora, el usuario que aplicó la acción y otros detalles. Los usuarios pueden agregar una anotación a una transacción para indicar por qué tuvo lugar una transacción.  
  
## <a name="when-transaction-are-recorded"></a>Cuándo se registran las transacciones  
 Las transacciones se registran cuando los miembros:  
  
-   se crean, eliminan o reactivan.  
  
-   se les cambian los valores de atributo.  
  
-   se cambian de lugar en una jerarquía.  
  
 No se graban las transacciones cuando las reglas de negocios cambian los valores de atributo.  
  
## <a name="view-and-manage-transactions"></a>Ver y administrar transacciones  
 En el área funcional del **Explorador** , puede ver y anotar (agregar comentarios a) las transacciones que haya realizado por sí mismo.  
  
 En el área funcional de **Administración de versiones** , los administradores pueden ver todas las transacciones de todos los usuarios para los modelos a los que tienen acceso e invertirlas.  
  
> [!NOTE]  
>  Los administradores pueden ver todas las transacciones de todos los usuarios siempre y cuando no tengan aplicado el nivel de permiso de solo lectura en el área funcional **Administración de versiones**. Por ejemplo, si se establece el nivel de permiso de solo lectura y el nivel de permiso de actualización para el administrador, este no podrá ver otras transacciones de usuario porque el permiso de solo lectura tendrá prioridad sobre el permiso de actualización.

## <a name="system-settings"></a>Configuración del sistema  
 Hay un valor en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que hace que las transacciones se graben o no cuando se cargan registros de almacenamiento provisional. Este valor solo afecta a SQL Server 2008 R2. Puede ajustar este valor en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o directamente en la tabla Configuración del sistema de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](system-settings-master-data-services.md).  
  
 Al importar los datos en esta versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede especificar si registrar o no las transacciones al iniciar el procedimiento almacenado. Para obtener más información, consulte [Procedimiento almacenado de almacenamiento provisional &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="concurrency"></a>Simultaneidad  
 Si un valor de entidad determinado se muestra de forma simultánea en más de una sesión del Explorador, es posible que se efectúen modificaciones en paralelo en el mismo valor. MDS no detecta las modificaciones simultáneas automáticamente. Esto puede producirse cuando hay varios usuarios que están utilizando MDS Explorer en el explorador web desde varias sesiones, por ejemplo, desde diversos equipos, diversas pestañas o ventanas del explorador o desde múltiples cuentas de usuario.  
  
 Varios usuarios pueden actualizar los mismos valores de entidad sin que se produzcan errores pese a que estén habilitadas transacciones. Por lo general, prevalecerá la última modificación a un valor en una secuencia temporal. El conflicto de modificación duplicada se puede observar en el historial de transacciones y lo puede corregir el administrador manualmente. El historial de transacciones mostrará las transacciones individuales para **Valor anterior** y **Valor nuevo** para el atributo relevante en cada sesión, pero no solucionará automáticamente el conflicto cuando haya varios **Valores nuevos** para el mismo valor antiguo.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Deshacer una acción invirtiendo una transacción (solo administradores).|[Invertir una transacción &#40;Master Data Services&#41;](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Los administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
-   [Las anotaciones &#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)  
  
  

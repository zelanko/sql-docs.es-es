---
title: Transacciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
caps.latest.revision: 15
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71fbe0edbb09334ad1c3a7f0f9f894c30dff93fd
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="transactions-master-data-services"></a>Transacciones (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]



--------------------------------------------------
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
  
 Puede configurar el tiempo que se conservan los datos del registro de transacciones; para ello, establezca la propiedad **Retención de registro en días** en la configuración del sistema para la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , y establezca **Log Retention Days** (Días de retención del registro) al crear o editar un modelo. Para obtener más información, consulte [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) y [Crear un modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
 El trabajo MDS_MDM_Sample_Log_Maintenace del Agente SQL Server desencadena la limpieza de los registros de transacciones y se ejecuta todas las noches. Puede usar el Agente SQL Server para modificar la programación de este trabajo.  
  
 También puede llamar a los procedimientos almacenados siguientes para limpiar los registros de transacciones.  
  
|Procedimiento almacenado|Description|  
|----------------------|-----------------|  
|mdm.udpTransactionsCleanup|Limpia el historial de transacciones.|  
|mdm.udpValidationsCleanup|Limpia el historial de validaciones.|  
|mdm.udpEntityStagingBatchTableCleanup|Limpia la tabla de almacenamiento provisional.|  
  
 **Ejemplo**  
  
```  
DECLARE @CleanupOlderThanDate date = '2014-11-11',  
@ModelID INT = 7  
--Clean up Transaction Logs  
EXEC mdm.udpTransactionsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up Validation History  
EXEC mdm.udpValidationsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up EBS tables  
EXEC mdm.udpEntityStagingBatchTableCleanup @ModelID, @CleanupOlderThanDate;  
  
```  
  
## <a name="system-settings"></a>Configuración del sistema  
 Hay un valor en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que hace que las transacciones se graben o no cuando se cargan registros de almacenamiento provisional. Puede ajustar este valor en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o directamente en la tabla Configuración del sistema de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
 Al importar los datos en esta versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede especificar si registrar o no las transacciones al iniciar el procedimiento almacenado. Para obtener más información, consulte [Procedimiento almacenado de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="concurrency"></a>Simultaneidad  
 Si un valor de entidad determinado se muestra de forma simultánea en más de una sesión del Explorador, es posible que se efectúen modificaciones en paralelo en el mismo valor. MDS no detecta las modificaciones simultáneas automáticamente. Esto puede producirse cuando hay varios usuarios que están utilizando MDS Explorer en el explorador web desde varias sesiones, por ejemplo, desde diversos equipos, diversas pestañas o ventanas del explorador o desde múltiples cuentas de usuario.  
  
 Varios usuarios pueden actualizar los mismos valores de entidad sin que se produzcan errores pese a que estén habilitadas transacciones. Por lo general, prevalecerá la última modificación a un valor en una secuencia temporal. El conflicto de modificación duplicada se puede observar en el historial de transacciones y lo puede corregir el administrador manualmente. El historial de transacciones mostrará las transacciones individuales para **Valor anterior** y **Valor nuevo** para el atributo relevante en cada sesión, pero no solucionará automáticamente el conflicto cuando haya varios **Valores nuevos** para el mismo valor antiguo.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Deshacer una acción invirtiendo una transacción (solo administradores).|[Invertir una transacción &#40;Master Data Services&#41;](../master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Transactions, Validation Issue and Staging table cleanup](http://go.microsoft.com/fwlink/p/?LinkId=615374)(Limpieza de la tabla de transacciones, de problemas de validación y de almacenamiento provisional), en msdn.com.  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   [Anotaciones &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)  
  
  

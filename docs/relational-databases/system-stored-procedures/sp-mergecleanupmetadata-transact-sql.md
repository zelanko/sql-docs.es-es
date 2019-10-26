---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0196993f863d973e14834f7eb3b93b797a825ac4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907324"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Solo debe utilizarse en topologías de replicación que incluyan servidores que ejecuten versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** permite a los administradores limpiar los metadatos en las tablas del sistema **MSmerge_genhistory**, **MSmerge_contents** y **MSmerge_tombstone** . Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` es el nombre de la publicación. *Publication* es de **tipo sysname y su**valor predeterminado es **%** , que limpia los metadatos de todas las publicaciones. La publicación debe existir, si se especifica explícitamente.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` especifica si se debe reinicializar el suscriptor. *Subscriber* es de tipo **nvarchar (5)** , puede ser **true** o **false**y su valor predeterminado es **true**. Si **es true**, las suscripciones se marcan para reinicializarse. Si **es false**, las suscripciones no se marcan para reinicializarlas.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_mergecleanupmetadata** solo debe utilizarse en topologías de replicación que incluyan servidores que ejecuten versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Las topologías que solo incluyan [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 o posterior deben usar la limpieza de metadatos basada en la retención automática. Al ejecutar este procedimiento almacenado, se debe tener en cuenta que el archivo de registro necesita y puede llegar a aumentar en gran medida en el equipo donde se está ejecutando el procedimiento almacenado.  
  
> [!CAUTION]
>  Después de ejecutar **sp_mergecleanupmetadata** , de forma predeterminada, todas las suscripciones en los suscriptores de publicaciones que tienen metadatos almacenados en **MSmerge_genhistory**, **MSmerge_contents** y **MSmerge_tombstone** se marcan para reinicialización, se pierden todos los cambios pendientes en el suscriptor y la instantánea actual se marca como obsoleta.  
> 
> [!NOTE]
>  Si hay varias publicaciones en una base de datos y cualquiera de estas publicaciones utiliza un período de retención de publicación infinita ( **\@retención**=**0**), la ejecución de **sp_mergecleanupmetadata** no limpia la combinación metadatos de seguimiento de cambios de replicación para la base de datos. Por ese motivo, debe utilizar con cuidado la retención infinita de publicaciones.  
  
 Al ejecutar este procedimiento almacenado, puede elegir si desea reinicializar los suscriptores estableciendo el\@parámetro **reinitialize_subscriber** en **true** (valor predeterminado) o **false**. Si **sp_mergecleanupmetadata** se ejecuta con el parámetro **\@Reinitialize_subscriber** establecido en **true**, se vuelve a aplicar una instantánea en el suscriptor incluso si la suscripción se creó sin una instantánea inicial (por ejemplo, si los datos y el esquema de instantáneas se aplicaron manualmente o ya existían en el suscriptor). El establecimiento del parámetro en **false** debe usarse con precaución, ya que si la publicación no se reinicializa, debe asegurarse de que los datos del publicador y del suscriptor estén sincronizados.  
  
 Independientemente del valor de **\@reinitialize_subscriber**, **sp_mergecleanupmetadata** produce un error si hay procesos de mezcla en curso que intentan cargar los cambios en un publicador o en un suscriptor de republicación en el momento en que se almacena el se invoca el procedimiento.  
  
 **Ejecutar sp_mergecleanupmetadata con \@reinitialize_subscriber = TRUE:**  
  
1.  Se recomienda, aunque no es obligatorio, detener todas las actualizaciones a las bases de datos de publicaciones y suscripciones. Si las actualizaciones continúan, al reinicializar la publicación se perderán todas las actualizaciones realizadas en el suscriptor desde la última mezcla, pero se mantendrá la convergencia de datos.  
  
2.  Ejecute una mezcla con el Agente de mezcla. Se recomienda usar la opción de línea de comandos del agente **-Validate** en cada suscriptor al ejecutar el agente de mezcla. Si está ejecutando mezclas en modo continuo, consulte las *consideraciones especiales para las combinaciones de modo continuo* más adelante en esta sección.  
  
3.  Una vez completadas todas las combinaciones, ejecute **sp_mergecleanupmetadata**.  
  
4.  Ejecute **sp_reinitmergepullsubscription** en todos los suscriptores con una suscripción de extracción anónima o con nombre para garantizar la convergencia de los datos.  
  
5.  Si está ejecutando mezclas en modo continuo, consulte las *consideraciones especiales para las combinaciones de modo continuo* más adelante en esta sección.  
  
6.  Vuelva a generar los archivos de instantáneas para todas las publicaciones de combinación afectadas a cualquier nivel. Si intenta mezclar sin volver a generar primero la instantánea, recibirá un aviso para que vuelva a generar la instantánea.  
  
7.  Realice una copia de seguridad de la base de datos de publicaciones. Si no se hace, se puede producir un error de mezcla después de restaurar la base de datos de publicación.  
  
 **Ejecutar sp_mergecleanupmetadata con \@reinitialize_subscriber = FALSE:**  
  
1.  Detenga **todas** las actualizaciones de las bases de datos de publicaciones y suscripciones.  
  
2.  Ejecute una mezcla con el Agente de mezcla. Se recomienda usar la opción de línea de comandos del agente **-Validate** en cada suscriptor al ejecutar el agente de mezcla. Si está ejecutando mezclas en modo continuo, consulte las *consideraciones especiales para las combinaciones de modo continuo* más adelante en esta sección.  
  
3.  Una vez completadas todas las combinaciones, ejecute **sp_mergecleanupmetadata**.  
  
4.  Si está ejecutando mezclas en modo continuo, consulte las *consideraciones especiales para las combinaciones de modo continuo* más adelante en esta sección.  
  
5.  Vuelva a generar los archivos de instantáneas para todas las publicaciones de combinación afectadas a cualquier nivel. Si intenta mezclar sin volver a generar primero la instantánea, recibirá un aviso para que vuelva a generar la instantánea.  
  
6.  Realice una copia de seguridad de la base de datos de publicaciones. Si no se hace, se puede producir un error de mezcla después de restaurar la base de datos de publicación.  

 **Consideraciones especiales para las combinaciones de modo continuo**  
  
 Si está ejecutando mezclas en modo continuo, debe:  
  
-   Detenga el Agente de mezcla y, a continuación, realice otra combinación sin el parámetro **-Continuous** especificado.  
  
-   Desactive la publicación con **sp_changemergepublication** para asegurarse de que se produzca un error en las mezclas en modo continuo que sondean el estado de la publicación.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Cuando haya completado el paso 3 de ejecutar **sp_mergecleanupmetadata**, reanude las mezclas en modo continuo en función de cómo las detuvo. Realice una de las acciones siguientes:  
  
-   Vuelva a agregar el parámetro **-Continuous** para el agente de mezcla.  
  
-   Reactive la publicación con **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_mergecleanupmetadata**.  
  
 Para utilizar este procedimiento almacenado, el publicador debe estar ejecutando [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Los suscriptores deben ejecutar [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0, Service Pack 2.  
  
## <a name="see-also"></a>Ver también  
 [MSmerge_genhistory &#40; Transact-&#41; SQL](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)  
 [ &#40;de Transact-&#41; SQL MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)  
 [MSmerge_tombstone &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  

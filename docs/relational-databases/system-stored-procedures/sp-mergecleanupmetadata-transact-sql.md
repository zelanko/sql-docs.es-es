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
manager: craigg
ms.openlocfilehash: 6924ef36c57036cf6cad6e25a6dc5cebfa5fa5f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63017850"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Debe usarse solo en topologías de replicación que incluyan servidores que ejecuten versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** permite a los administradores limpiar los metadatos de la **MSmerge_genhistory**, **MSmerge_contents** y **MSmerge_tombstone** las tablas del sistema. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**, que limpia los metadatos para todas las publicaciones. La publicación debe existir, si se especifica explícitamente.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` Especifica si se debe reinicializar el suscriptor. *suscriptor* es **nvarchar (5)**, puede ser **TRUE** o **FALSE**, su valor predeterminado es **TRUE**. Si **TRUE**, las suscripciones se marcan para reinicialización. Si **FALSE**, las suscripciones no se marcan para reinicialización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_mergecleanupmetadata** debe usarse solo en topologías de replicación que incluyan servidores que ejecuten versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Las topologías que solo incluyan [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 o posterior deben usar la limpieza de metadatos basada en la retención automática. Al ejecutar este procedimiento almacenado, se debe tener en cuenta que el archivo de registro necesita y puede llegar a aumentar en gran medida en el equipo donde se está ejecutando el procedimiento almacenado.  
  
> [!CAUTION]
>  Después de **sp_mergecleanupmetadata** se ejecuta de forma predeterminada, todas las suscripciones en los suscriptores de publicaciones que tienen metadatos almacenados en **MSmerge_genhistory**, **MSmerge_contents**  y **MSmerge_tombstone** se marcan para reinicialización, se pierden los cambios pendientes en el suscriptor y la instantánea actual está marcado como obsoleta.  
> 
> [!NOTE]
>  Si hay varias publicaciones en una base de datos y una de estas publicaciones utiliza un período de retención de publicación infinito (**@retention**=**0**), en ejecución  **sp_mergecleanupmetadata** no limpiará el cambio de la replicación de mezcla metadatos para la base de datos de seguimiento. Por ese motivo, debe utilizar con cuidado la retención infinita de publicaciones.  
  
 Al ejecutar este procedimiento almacenado, puede elegir si desea reinicializar los suscriptores estableciendo el **@reinitialize_subscriber** parámetro **TRUE** (valor predeterminado) o **FALSE**. Si **sp_mergecleanupmetadata** se ejecuta con la **@reinitialize_subscriber** parámetro establecido en **TRUE**, incluso si la suscripción es una instantánea se vuelve a aplicar en el suscriptor se crea sin una instantánea (por ejemplo, si los datos de instantánea y el esquema se han aplicado de forma manual o ya existían en el suscriptor) inicial. Valor del parámetro **FALSE** debe utilizarse con precaución, porque si no se reinicializa la publicación, debe asegurarse de que se sincronizan datos en el publicador y suscriptor.  
  
 Independientemente del valor de **@reinitialize_subscriber**, **sp_mergecleanupmetadata** se produce un error si hay en curso combinar los procesos que están intentando cargar los cambios en el publicador o un suscriptor de republicación en la hora en que se invoca el procedimiento almacenado.  
  
 **Ejecutar sp_mergecleanupmetadata con @reinitialize_subscriber = TRUE:**  
  
1.  Se recomienda, aunque no es obligatorio, detener todas las actualizaciones a las bases de datos de publicaciones y suscripciones. Si las actualizaciones continúan, al reinicializar la publicación se perderán todas las actualizaciones realizadas en el suscriptor desde la última mezcla, pero se mantendrá la convergencia de datos.  
  
2.  Ejecute una mezcla con el Agente de mezcla. Se recomienda que use el **-validar** opción de línea de comandos del agente en cada suscriptor cuando se ejecuta el agente de mezcla. Si está ejecutando mezclas en modo continuo, vea *consideraciones especiales para mezclas en modo continuo* más adelante en esta sección.  
  
3.  Cuando hayan terminado todas las mezclas, ejecute **sp_mergecleanupmetadata**.  
  
4.  Ejecutar **sp_reinitmergepullsubscription** en todos los suscriptores con suscripción de extracción con nombre o anónimo para garantizar la convergencia de los datos.  
  
5.  Si está ejecutando mezclas en modo continuo, vea *consideraciones especiales para mezclas en modo continuo* más adelante en esta sección.  
  
6.  Vuelva a generar los archivos de instantáneas para todas las publicaciones de combinación afectadas a cualquier nivel. Si intenta mezclar sin volver a generar primero la instantánea, recibirá un aviso para que vuelva a generar la instantánea.  
  
7.  Realice una copia de seguridad de la base de datos de publicaciones. Si no se hace, se puede producir un error de mezcla después de restaurar la base de datos de publicación.  
  
 **Ejecutar sp_mergecleanupmetadata con @reinitialize_subscriber = FALSE:**  
  
1.  Detener **todas** las actualizaciones de las bases de datos de publicaciones y suscripciones.  
  
2.  Ejecute una mezcla con el Agente de mezcla. Se recomienda que use el **-validar** opción de línea de comandos del agente en cada suscriptor cuando se ejecuta el agente de mezcla. Si está ejecutando mezclas en modo continuo, vea *consideraciones especiales para mezclas en modo continuo* más adelante en esta sección.  
  
3.  Cuando hayan terminado todas las mezclas, ejecute **sp_mergecleanupmetadata**.  
  
4.  Si está ejecutando mezclas en modo continuo, vea *consideraciones especiales para mezclas en modo continuo* más adelante en esta sección.  
  
5.  Vuelva a generar los archivos de instantáneas para todas las publicaciones de combinación afectadas a cualquier nivel. Si intenta mezclar sin volver a generar primero la instantánea, recibirá un aviso para que vuelva a generar la instantánea.  
  
6.  Realice una copia de seguridad de la base de datos de publicaciones. Si no se hace, se puede producir un error de mezcla después de restaurar la base de datos de publicación.  
  
 **Consideraciones especiales para mezclas en modo continuo**  
  
 Si está ejecutando mezclas en modo continuo, debe:  
  
-   Detenga el agente de mezcla y, a continuación, realizar otra mezcla sin el **-continua** los parámetros especificados.  
  
-   Desactivar la publicación con **sp_changemergepublication** para garantizar que las mezclas en modo continuo que sondeen el estado de publicación.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Cuando haya completado el paso 3 de la ejecución **sp_mergecleanupmetadata**, reanude las mezclas en modo continuo en función de cómo las haya detenido. Realice una de las acciones siguientes:  
  
-   Agregar el **-continua** parámetro nuevo para el agente de mezcla.  
  
-   Volver a activar la publicación con **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_mergecleanupmetadata**.  
  
 Para utilizar este procedimiento almacenado, el publicador debe estar ejecutando [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Los suscriptores deben ejecutar [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, Service Pack 2.  
  
## <a name="see-also"></a>Vea también  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  

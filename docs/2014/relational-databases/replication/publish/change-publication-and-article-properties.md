---
title: Cambio delas propiedades de la publicación y de los artículos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying article properties
- modifying publication properties
- administering replication, properties
- publications [SQL Server replication], changing properties
- articles [SQL Server replication], properties
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 207f934a9fba6e60bf1903544b12c88b4924dc23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021317"
---
# <a name="change-publication-and-article-properties"></a>Cambiar las propiedades de la publicación y de los artículos
  Una vez creada una publicación, la mayoría de las propiedades de la publicación y de los artículos se pueden cambiar, aunque algunas requieren la regeneración de la instantánea o la reinicialización de las suscripciones. En este tema se ofrece información sobre todas las propiedades que requieren una de estas acciones o las dos si se cambian.  
  
## <a name="publication-properties-for-snapshot-and-transactional-replication"></a>Propiedades de la publicación para replicación de instantáneas y replicación transaccional.  
  
|Descripción|Procedimiento almacenado|Propiedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Cambiar el formato de la instantánea|**sp_changepublication**|**sync_method**|Nueva instantánea.|  
|Cambiar la ubicación de la instantánea|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Nueva instantánea.|  
|Cambiar la ubicación de la instantánea|**sp_changedistpublisher**|**working_directory**|Nueva instantánea.|  
|Cambiar la compresión de la instantánea|**sp_changepublication**|**compress_snapshot**|Nueva instantánea.|  
|Cambiar una opción del protocolo de transferencia de archivos (FTP) de la instantánea|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Nueva instantánea.|  
|Cambiar la ubicación del script anterior o posterior a la instantánea|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Nueva instantánea (también requerida si cambia el contenido del script ).<br /><br /> Se requiere la reinicialización para aplicar el nuevo script en el suscriptor.|  
|Habilitar o deshabilitar la compatibilidad para los suscriptores que no sean de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|**sp_changepublication**|**is_enabled_for_het_sub**|Nueva instantánea.|  
|Cambiar los informes de conflictos para las suscripciones de actualización en cola|**sp_changepublication**|**centralized_conflicts**|Se puede cambiar únicamente si no hay suscripciones activas.|  
|Cambiar la directiva de resolución de conflictos para las suscripciones de actualización en cola|**sp_changepublication**|**conflict_policy**|Se puede cambiar únicamente si no hay suscripciones activas.|  
  
## <a name="article-properties-for-snapshot-and-transactional-replication"></a>Propiedades de los artículos para replicación de instantáneas y replicación transaccional  
  
|Descripción|Procedimiento almacenado|Propiedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Quitar un artículo|**sp_droparticle**|Todos los parámetros|Los artículos se pueden quitar antes de crear las suscripciones. Utilizando procedimientos almacenados es posible quitar una suscripción a un artículo; utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], es necesario quitar, volver a crear y sincronizar toda la suscripción. Para más información, vea [Agregar y quitar artículos de publicaciones existentes](add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Cambiar un filtro de columna|**sp_articlecolumn**|**@column**<br /><br /> **@operation**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Agregar un filtro de fila|**sp_articlefilter**|Todos los parámetros|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Quitar un filtro de fila|**sp_articlefilter**|**@article**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar un filtro de fila|**sp_articlefilter**|**@filter_clause**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar un filtro de fila|**sp_changearticle**|**filter**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar las opciones del esquema|**sp_changearticle**|**schema_option**|Nueva instantánea.|  
|Cambie el modo de controlar las tablas en el suscriptor antes de aplicar la instantánea.|**sp_changearticle**|**pre_creation_cmd**|Nueva instantánea.|  
|Cambiar el estado del artículo|**sp_changearticle**|**status**|Nueva instantánea.|  
|Cambiar los comandos UPDATE, INSERT o DELETE|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar el nombre de la tabla de destino|**sp_changearticle**|**dest_table**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar el propietario de la tabla de destino (esquema)|**sp_changearticle**|**destination_owner**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar las asignaciones de tipos de datos (se aplica solo a publicaciones de Oracle)|**sp_changearticlecolumndatatype**|**@type**<br /><br /> **@length**<br /><br /> **@precision**<br /><br /> **@scale**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
  
## <a name="publication-properties-for-merge-replication"></a>Propiedades de la publicación para replicación de mezcla  
  
|Descripción|Procedimiento almacenado|Propiedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Cambiar el formato de la instantánea|**sp_changemergepublication**|**sync_mode**|Nueva instantánea.|  
|Cambiar la ubicación de la instantánea|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Nueva instantánea.|  
|Cambiar la ubicación de la instantánea|**sp_changedistpublisher**|**working_directory**|Nueva instantánea.|  
|Cambiar la compresión de la instantánea|**sp_changemergepublication**|**compress_snapshot**|Nueva instantánea.|  
|Cambiar cualquiera de las opciones de FTP de la instantánea|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Nueva instantánea.|  
|Cambiar el script anterior o posterior a la instantánea|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Nueva instantánea (también requerida si cambia el contenido del script ).<br /><br /> Se requiere la reinicialización para aplicar el nuevo script en el suscriptor.|  
|Agregar un filtro de combinación o un registro lógico|**sp_addmergefilter**|Todos los parámetros|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Quitar un filtro de combinación o un registro lógico|**sp_dropmergefilter**|Todos los parámetros|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar un filtro de combinación o un registro lógico|**sp_changemergefilter**|**@property**<br /><br /> **@value**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Deshabilitar el uso de filtros con parámetros (habilitar los filtros con parámetros no requiere ninguna acción especial)|**sp_changemergepublication**|Un valor de **false** para **dynamic_filters**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Habilitar o deshabilitar el uso de particiones precalculadas|**sp_changemergepublication**|**use_partition_groups**|Nueva instantánea.|  
|Habilitar o deshabilitar la optimización de particiones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]|**sp_changemergepublication**|**keep_partition_changes**|Reinicialice las suscripciones.|  
|Habilitar o deshabilitar la validación de particiones del suscriptor|**sp_changemergepublication**|**validate_subscriber_info**|Reinicialice las suscripciones.|  
|Cambiar el nivel de compatibilidad de la publicación a 80sp3 o inferior|**sp_changemergepublication**|**publication_compatibility_level**|Nueva instantánea.|  
  
## <a name="article-properties-for-merge-replication"></a>Propiedades de los artículos para replicación de mezcla  
  
|Descripción|Procedimiento almacenado|Propiedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Quitar un artículo que tiene el último filtro con parámetros de la publicación|**sp_dropmergearticle**|Todos los parámetros|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Quitar un artículo que es primario en un filtro de combinación o registro lógico (esto tiene como efecto secundario la desaparición de la combinación)|**sp_dropmergearticle**|Todos los parámetros|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Quitar un artículo en las demás circunstancias|**sp_dropmergearticle**|Todos los parámetros|Nueva instantánea.|  
|Incluir un filtro de columna que no se publicó anteriormente|**sp_mergearticlecolumn**|**@column**<br /><br /> **@operation**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Agregar, quitar o cambiar un filtro de fila|**sp_changemergearticle**|**subset_filterclause**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.<br /><br /> Si se agrega, quita o modifica un filtro con parámetros, los cambios pendientes en el suscriptor no se pueden cargar en el publicador durante la reinicialización. Si desea cargar los cambios pendientes, sincronice todas las suscripciones antes de cambiar el filtro.<br /><br /> Si un artículo no participa en ninguno de los filtros de combinación, puede quitar el artículo y agregarlo de nuevo con un filtro de fila diferente. De este modo no será necesario reinicializar toda la suscripción. Para obtener información sobre cómo agregar y quitar artículos, vea [Agregar y quitar artículos de publicaciones existentes](add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Cambiar las opciones del esquema|**sp_changemergearticle**|**schema_option**|Nueva instantánea.|  
|Cambiar el seguimiento de columnas al seguimiento de filas (Cambiar el seguimiento de filas al seguimiento de columnas no requiere ninguna acción especial)|**sp_changemergearticle**|Un valor de **false** para **column_tracking**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Cambiar si los permisos se comprueban antes de que se apliquen en el publicador las instrucciones realizadas en el suscriptor|**sp_changemergearticle**|**check_permissions**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
|Habilitar o deshabilitar las suscripciones de solo descarga (cambiar otras opciones de carga no requiere ninguna acción especial)|**sp_changemergearticle**|Cambiar a o desde un valor de **2** para **subscriber_upload_options**|Reinicialice las suscripciones.|  
|Cambiar el propietario de la tabla de destino|**sp_changemergearticle**|**destination_owner**|Nueva instantánea.<br /><br /> Reinicialice las suscripciones.|  
  
## <a name="see-also"></a>Vea también  
 [Preguntas más frecuentes para administradores de replicación](../administration/frequently-asked-questions-for-replication-administrators.md)   
 [Crear y aplicar una instantánea](../create-and-apply-the-snapshot.md)   
 [Reinicializar suscripciones](../reinitialize-subscriptions.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)   
 [sp_articlefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)   
 [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)   
 [sp_changearticlecolumndatatype &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)   
 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)   
 [sp_droparticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql)   
 [sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)  
  
  

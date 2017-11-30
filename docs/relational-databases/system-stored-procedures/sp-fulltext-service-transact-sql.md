---
title: sp_fulltext_service (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
caps.latest.revision: "79"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac28028d1e888724417d1a313e229beb479e8ea2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spfulltextservice-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de servidor de la búsqueda de texto completo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@action=**] **'***acción***'**  
 Es la propiedad que se va a cambiar o restablecer. *acción* es **nvarchar (100),** no tiene ningún valor predeterminado. Para obtener una lista de un*c*ne propiedades, sus descripciones y los valores que se pueden establecer, vea la tabla en la *valor* argumento. Este argumento devuelve las propiedades siguientes: tipo de datos, valor actual, valor mínimo o máximo y estado de degradación, si procede.  
  
 [  **@value=**] *valor*  
 Es el valor de la propiedad especificada. *valor* es **sql_variant**, su valor predeterminado es null. Si @value es null, **sp_fulltext_service** devuelve el valor actual. En la siguiente tabla se muestran las propiedades de acción, sus descripciones y los valores que se pueden establecer.  
  
> [!NOTE]  
>  Las siguientes acciones se quitará en futuras versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **clean_up**, **connect_timeout**, **data_timeout**, y **resource_ uso de**. Evite su uso en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que las usan actualmente.  
  
|Acción|Tipo de datos|Description|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|Se admite únicamente por compatibilidad con versiones anteriores. El valor es siempre 0.|  
|**connect_timeout**|**int**|Se admite únicamente por compatibilidad con versiones anteriores. El valor es siempre 0.|  
|**data_timeout**|**int**|Se admite únicamente por compatibilidad con versiones anteriores. El valor es siempre 0.|  
|**load_os_resources**|**int**|Indica si los filtros, lematizadores y separadores de palabras del sistema operativo se registran y utilizan con esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una de las siguientes opciones:<br /><br /> 0 = Utiliza solo los filtros y separadores de palabras específicos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Cargar los filtros y separadores de palabras del sistema operativo.<br /><br /> De forma predeterminada, esta propiedad está deshabilitada para impedir cambios de comportamiento involuntarios por actualizaciones del sistema operativo. Habilitar el uso de recursos del sistema operativo proporciona acceso a recursos de idiomas y tipos de documento registrados en los Servicios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Index Server que no tienen instalado un recurso específico de la instancia. Si habilita la carga de recursos del sistema operativo, asegúrese de que los recursos del sistema operativo son archivos binarios firmados de confianza; en caso contrario, no pueden cargar cuando **verify_signature** (ver abajo) se establece en 1.|  
|**master_merge_dop**|**int**|Especifica el número de subprocesos que utilizará el proceso de mezcla maestra. Este valor no debe exceder el número de CPU o núcleos de CPU disponibles.<br /><br /> Cuando no se especifica este argumento, el servicio utiliza menos de 4, o el número de CPU o núcleos de CPU disponibles.|  
|**pause_indexing**|**int**|Especifica si se debe pausar la indización de texto completo, en caso de que se esté ejecutando actualmente, o si se debe reanudar, si está en pausa actualmente.<br /><br /> 0 = Reanuda las actividades de indización de texto completo para la instancia del servidor.<br /><br /> 1 = Pausa las actividades de indización de texto completo para la instancia del servidor.|  
|**resource_usage**|**int**|No tiene ninguna función en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, y se omite.|  
|**update_languages**|NULL|Actualiza la lista de idiomas y filtros registrados con búsqueda de texto completo. Los idiomas se especifican al configurar la indización y en las consultas de texto completo. El host de demonio de filtro utiliza filtros para extraer información textual de los formatos de archivo correspondientes, como .docx, almacenados en tipos de datos, como **varbinary**, **varbinary (max)**, **imagen** , o **xml**, para la indización de texto completo.<br /><br /> Para obtener más información, consulte [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).|  
|**upgrade_option**|**int**|Controla cómo se migran los índices de texto completo cuando se actualiza una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a una versión posterior. Esta propiedad se aplica a la actualización al adjuntar una base de datos, restaurar una copia de seguridad de base de datos, restaurar una copia de seguridad de archivo o copiar la base de datos mediante el Asistente para copiar bases de datos.<br /><br /> Una de las siguientes opciones:<br /><br /> 0 = Los catálogos de texto completo se vuelven a generar con los separadores de palabras nuevos y mejorados. La regeneración de los índices puede llevar cierto tiempo y, después de la actualización, podría ser necesaria una cantidad significativa de CPU y de memoria.<br /><br /> 1 = Los catálogos de texto completo se restablecen. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Los archivos de catálogo de texto completo se quitan, pero los metadatos de los catálogos de texto completo y los índices de texto completo se conservan. Después de actualizarse, todos los índices de texto completo quedan deshabilitados para el seguimiento de cambios y los rastreos no se inician de forma automática. El catálogo permanecerá vacío hasta que se emita manualmente un rellenado completo después de que se complete la actualización.<br /><br /> 2 = Se importan los catálogos de texto completo. Normalmente, el proceso de importación es significativamente más rápido que el de regeneración. Por ejemplo, si se usa solo una CPU, importar es aproximadamente 10 veces más rápido que volver a generar. Sin embargo, un catálogo de texto completo importado no usa los separadores de palabras nuevos y mejorados, por lo que es posible que, al final, le interese volver a generar los catálogos de texto completo.<br /><br /> Nota: Recompilación se puede ejecutar en modo de varios subprocesos y, si hay más de 10 CPU disponibles, la regeneración puede ejecutarse más rápidamente que el de importación si permite que el proceso de recompilación las use todas las CPU.<br /><br /> Si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados. Esta opción solo está disponible para bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .<br /><br /> Para obtener información sobre cómo elegir una opción de actualización de texto completo, vea[Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).<br /><br /> Nota: Para establecer esta propiedad en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], use la **opción de actualización de texto completo** propiedad. Para obtener más información, vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).|  
|**verify_signature**|**int**|Indica si el motor de texto completo carga únicamente binarios firmados. De forma predeterminada, solo se cargan binarios con firma de confianza.<br /><br /> 1 = Comprueba que solo se cargan binarios firmados de confianza (opción predeterminada).<br /><br /> 0 = No comprueba si los binarios están firmados.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **serveradmin** rol fijo de servidor o el administrador del sistema puede ejecutar **sp_fulltext_service**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. Actualizar la lista de idiomas registrados  
 En el ejemplo siguiente se actualiza la lista de idiomas registrados con búsqueda de texto completo.  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. Cambiar la opción de actualización de texto completo para restablecer los catálogos de texto completo  
 En el ejemplo siguiente se cambia la opción de actualización de texto completo para restablecer los catálogos de texto completo. De esta forma, se quitan completamente. En este ejemplo se especifican las palabras clave opcionales `@action` y `@value`.  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

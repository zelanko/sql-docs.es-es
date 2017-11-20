---
title: Catalog.cleanup_server_execution_keys | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 172925d5a63aa831881b6a6325f0dbcbccd4dd56
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverexecutionkeys"></a>Catalog.cleanup_server_execution_keys
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Quita certificados y claves simétricas de la base de datos de SSISDB.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cleanup_flag =] *cleanup_flag*  
 Indica si el nivel de ejecución (1) o un proyecto de nivel (2) certificados y claves simétricas que se van a quitarse.  
  
 Utilice el nivel de ejecución (1) sólo cuando el SERVER_OPERATION_ENCRYPTION_LEVEL se establece en PER_EXECUTION (1).  
  
 Utilice el nivel de proyecto (2) sólo cuando el SERVER_OPERATION_ENCRYPTION_LEVEL se establece en PER_PROJECT (2). Certificados y claves simétricas se quitan solo para los proyectos que se han eliminado y para el que se han eliminado los registros de operaciones.  
  
 [ @delete_batch_size =] *delete_batch_size*  
 El número de claves y certificados que se quiten. El valor predeterminado es 1000.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 si es correcta y 1 para el error.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y EXECUTE en el proyecto y, si procede, permisos de lectura en el entorno que se hace referencia.  
  
-   Pertenencia en el **ssis_admin** rol de base de datos.  
  
-   La pertenencia a la **sysadmin** rol de servidor.  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 Este procedimiento almacenado genera errores en los escenarios siguientes:  
  
-   Hay uno o más operaciones activas en la base de datos SSISDB.  
  
-   La base de datos SSISDB no está en modo de usuario único.  
  
## <a name="remarks"></a>Comentarios  
 SQL Server 2012 Service Pack 2 agrega la propiedad SERVER_OPERATION_ENCRYPTION_LEVEL a la **internal.catalog_properties** tabla. Esta propiedad tiene dos valores posibles:  
  
-   **PER_EXECUTION (1)** : el certificado y la clave simétrica que se usan para proteger los parámetros de ejecución confidenciales y registros de ejecución se crean para cada ejecución. Es el valor predeterminado. Puede encontrarse con problemas de rendimiento (interbloqueos, etc. de trabajos de mantenimiento con error..) en un entorno de producción porque certificados o claves se generan para cada ejecución. Sin embargo, esta configuración proporciona un mayor nivel de seguridad que el otro valor (2).  
  
-   **PER_PROJECT (2)** : el certificado y la clave simétrica usada para la protección de los parámetros confidenciales se crean para cada proyecto. Esto ofrece un mejor rendimiento que el nivel PER_EXECUTION debido a que la clave y el certificado se generan una vez para un proyecto, en lugar de para cada ejecución.  
  
 Tendrá que ejecutar el [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) procedimiento almacenado antes de poder cambiar el SERVER_OPERATION_ENCRYPTION_LEVEL entre 1 y 2 (o) de 2 a 1. Antes de ejecutar este procedimiento almacenado, haga lo siguiente:  
  
1.  Asegúrese de que el valor de la propiedad OPERATION_CLEANUP_ENABLED se establece en TRUE en el [catalog.catalog_properties &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) tabla.  
  
2.  Establezca la base de datos de Integration Services (SSISDB) en modo de usuario único. En SQL Server Management Studio, iniciar el cuadro de diálogo Propiedades de la base de datos para SSISDB, cambie a la ficha Opciones y establezca la propiedad de restringir el acceso en modo de usuario único (SINGLE_USER). Después de ejecutar el cleanup_server_log procedimiento almacenado, establezca el valor de propiedad en el valor original.  
  
3.  Ejecute el procedimiento almacenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md).  
  
4.  Ahora, continúe y cambie el valor de la propiedad SERVER_OPERATION_ENCRYPTION_LEVEL en el [catalog.catalog_properties &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) tabla.  
  
5.  Ejecute el procedimiento almacenado [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) para limpiar las claves de certificados de la base de datos SSISDB. Quitar certificados y claves de la base de datos SSISDB puede tardar mucho tiempo, por lo que debe ejecutarse periódicamente durante horas de poca actividad.  
  
     Puede especificar el ámbito o el nivel (ejecución frente a proyecto) y el número de claves va a eliminar. El tamaño de lote de predeterminado para su eliminación es 1000. Cuando el nivel se establece en 2, se eliminan las claves y certificados sólo si se han eliminado los proyectos asociados.  
  
 Para obtener más información, consulte el siguiente artículo de Knowledge Base. [CORRECCIÓN: Problemas de rendimiento al usar SSISDB como la implementación de almacenan en SQL Server 2012](http://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se llama al procedimiento almacenado de cleanup_server_execution_keys.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
  
EXEC@return_value = [internal].[cleanup_server_execution_keys]  
@cleanup_flag = 1,  
@delete_batch_size = 500  
  
SELECT'Return Value' = @return_value  
  
GO  
```  
  
  


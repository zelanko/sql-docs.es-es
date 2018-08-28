---
title: Administración del seguimiento de cambios (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: track-changes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
caps.latest.revision: 9
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a142bac7278f5719a146812bc63017663eb1bab
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070267"
---
# <a name="manage-change-tracking-sql-server"></a>Administrar el seguimiento de cambios (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo administrar el seguimiento de los cambios. También se describe cómo configurar la seguridad, así como determinar los efectos en el almacenamiento y en el rendimiento cuando se utiliza esta característica.  
  
## <a name="managing-change-tracking"></a>Administración del seguimiento de cambios  
 En las secciones siguientes se enumeran las vistas de catálogo, los permisos y los valores de configuración que son importantes para la administración del seguimiento de cambios.  
  
### <a name="catalog-views"></a>Vistas de catálogo  
 Para determinar qué tablas y bases de datos tienen el seguimiento de cambios habilitado, puede utilizar las vistas de catálogo siguientes:  
  
-   [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)  
  
-   [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
 También, la vista de catálogo [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) genera una lista de las tablas internas que se crean al habilitar el seguimiento de cambios para una tabla de usuario.  
  
### <a name="security"></a>Seguridad  
 Para tener acceso a información del seguimiento de cambios mediante las [funciones de seguimiento de cambios](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md), la entidad de seguridad debe tener los permisos siguientes:  
  
-   Permiso SELECT para la tabla que se consulta, por lo menos para las columnas de clave principal de la tabla sometida a seguimiento de cambios.  
  
-   Permiso VIEW CHANGE TRACKING  para la tabla para la que se obtienen los cambios. El permiso VIEW CHANGE TRACKING es necesario por las razones siguientes:  
  
    -   Los registros de seguimiento de cambios incluyen información sobre las filas que se han eliminado, en concreto los valores de clave principal de las filas eliminadas. Una entidad de seguridad podría haber obtenido el permiso SELECT para una tabla de seguimiento de cambios tras haberse eliminado de la misma datos confidenciales. En este caso, no sería aconsejable que esa entidad de seguridad pudiera tener acceso a la información eliminada utilizando el seguimiento de cambios.  
  
    -   El seguimiento de cambios puede contener información sobre qué columnas se han visto modificadas por las operaciones de actualización. Es posible que se le haya denegado a una entidad de seguridad el permiso para una columna que contiene información confidencial. Sin embargo, dado que la información del seguimiento de cambios está disponible, una entidad de seguridad puede determinar que el valor de una columna ha sido actualizado, pero no puede determinar el valor la citada columna.  
  
## <a name="understanding-change-tracking-overhead"></a>Descripción de la sobrecarga que supone el seguimiento de cambios  
 Al habilitar el seguimiento de cambios para una tabla, algunas operaciones de administración quedan afectadas. En la tabla siguiente se enumeran las operaciones y los efectos que se deben considerar.  
  
|Operación|Cuando el seguimiento de cambios está habilitado|  
|---------------|-------------------------------------|  
|DROP TABLE|Se quita toda la información del seguimiento de cambios para la tabla quitada.|  
|ALTER TABLE DROP CONSTRAINT|Se producirá un error en el intento de quitar la restricción PRIMARY KEY. Para poder quitar una restricción PRIMARY KEY, el seguimiento de cambios debe estar previamente deshabilitado.|  
|ALTER TABLE DROP COLUMN|Si la columna que se desea quitar forma parte de la clave principal, no se permite la eliminación, independientemente del seguimiento de cambios.<br /><br /> Si la columna que se desea quitar no forma parte de la clave principal, la columna se quita correctamente. No obstante, es preciso ser consciente del efecto que se provocará en cualquier aplicación que esté sincronizando estos datos. Si el seguimiento de cambios de la columna está habilitado para la tabla, es posible que la columna quitada siga formando parte de la información del seguimiento de cambios obtenida. El trato que se deba dar a la columna quitada es responsabilidad de la aplicación.|  
|ALTER TABLE ADD COLUMN|Si se agrega una columna nueva a la tabla sometida a seguimiento de cambios, la incorporación de la columna no se incluye en el seguimiento. Solo se realiza el seguimiento de las actualizaciones y los cambios que se efectúen en la columna nueva.|  
|ALTER TABLE ALTER COLUMN|No se realiza el seguimiento de los cambios del tipo de datos de las columnas de clave que no pertenezcan a la clave primaria.|  
|ALTER TABLE SWITCH|El intercambio de particiones produce un error si una o ambas tablas tienen el seguimiento de cambios habilitado.|  
|DROP INDEX o ALTER INDEX DISABLE|El índice que exige la clave principal no se puede quitar o deshabilitar.|  
|TRUNCATE TABLE|Es posible aplicar truncamiento sobre tablas que tengan el seguimiento de cambios habilitado. Sin embargo, no se realiza el seguimiento de las filas eliminadas por la operación, y se actualiza la versión válida mínima. Cuando una aplicación comprueba su versión, la comprobación indica que la versión es demasiado antigua y se requiere una reinicialización. Esto es lo mismo que deshabilitar el seguimiento de cambios y, a continuación, volverlo a habilitar para la tabla.|  
  
 Cuando se usa el seguimiento de cambios, se agrega cierta sobrecarga a las operaciones DML debido a que la información correspondiente se almacena como parte de la operación.  
  
### <a name="effects-on-dml"></a>Efectos en DML  
 El seguimiento de cambios se ha optimizado para minimizar la sobrecarga de rendimiento en operaciones DML. El incremento en la sobrecarga de rendimiento que se asocia al uso del seguimiento de cambios en una tabla es similar a la sobrecarga en que se incurre cuando se crea un índice para una tabla y hay que mantenerlo.  
  
 Para cada fila modificada por una operación DML, se agrega una fila a la tabla de seguimiento de cambios interna. El efecto de esta agregación en lo que respecta a la operación DML depende de factores tales como:  
  
-   El número de columnas de clave principal  
  
-   La cantidad de datos que se modifican en la fila de la tabla de usuario  
  
-   El número de operaciones que se realizan en una transacción  
  
 El aislamiento de instantánea, si se usa, también afectará al rendimiento de todas las operaciones DML, esté habilitado o no el seguimiento de cambios.  
  
### <a name="effects-on-storage"></a>Efectos en el almacenamiento  
 Los datos del seguimiento de cambios se almacenan en los tipos siguientes de tablas internas:  
  
-   Tabla de cambios interna  
  
     Hay una tabla de cambios interna para cada tabla de usuario que tenga habilitado el seguimiento de cambios.  
  
-   Tabla de transacciones interna  
  
     Hay una tabla de transacciones interna para la base de datos.  
  
 Estas tablas internas afectan a los requisitos de almacenamiento de las maneras siguientes:  
  
-   Para cada cambio realizado en cada fila de la tabla de usuario, se agrega una fila a la tabla de cambios interna. Esta fila tiene una pequeña sobrecarga fija más una sobrecarga variable equivalente al tamaño de las columnas de clave principal. La fila puede contener información de contexto opcional establecida por una aplicación. Y, si el seguimiento de la columna está habilitado, cada columna modificada requiere 4 bytes en la tabla de seguimiento.  
  
-   Por cada transacción confirmada, se agrega una fila a una tabla de transacciones interna.  
  
 Como en el caso de otras tablas internas, es posible determinar el espacio usado para las tablas de seguimiento de cambios a través del procedimiento almacenado [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) . Los nombres de las tablas internas se pueden obtener con la vista de catálogo [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) , como se muestra en el ejemplo siguiente.  
  
```sql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>Ver también  
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Propiedades de la base de datos &#40;página ChangeTracking&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Trabajar con datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  

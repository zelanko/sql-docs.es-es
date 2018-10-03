---
title: sp_pdw_remove_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 27c91a2e67f8bd9c71ee0dc5ce088ee596c7c765
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746533"
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Esto quita credenciales de red almacenadas en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para tener acceso a un recurso compartido de red. Por ejemplo, utilice este procedimiento almacenado para quitar el permiso de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para realizar copia de seguridad y restaurar las operaciones en un servidor que se encuentra en su propia red.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica el nombre de host del servidor de destino o dirección IP. Las credenciales para tener acceso a este servidor se quitará de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Esto no cambia ni quitar ningún permiso en el servidor de destino real que se administra mediante su propio equipo.  
  
 *target_server_name* se define como nvarchar(337).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere **ALTER SERVER STATE** permiso.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Se produce un error si la eliminación de credenciales no funciona en el nodo de Control y todos los nodos de proceso.  
  
## <a name="general-remarks"></a>Notas generales  
 Este procedimiento almacenado quita credenciales de red de la cuenta de NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. La cuenta NetworkService ejecuta cada instancia de SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el nodo de Control y los nodos de proceso. Por ejemplo, cuando se ejecuta una operación de copia de seguridad, el nodo de Control y cada nodo de proceso usará las credenciales de cuenta de NetworkService para tener acceso al servidor de destino.  
  
## <a name="metadata"></a>Metadatos  
 Para enumerar todas las credenciales y para comprobar que se han quitado las credenciales, utilice [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Para agregar las credenciales, utilice [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Quitar las credenciales para realizar una copia de seguridad de base de datos  
 El ejemplo siguiente quita credenciales de nombre y la contraseña de usuario para acceder al servidor de destino que tiene una dirección IP de 10.192.147.63.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  


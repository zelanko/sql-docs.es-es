---
title: sp_pdw_remove_network_credentials (almacenamiento de datos de SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a82cc5004304310c7c2bc3392ada6bad0acb617f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (almacenamiento de datos de SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Esto quita las credenciales de red almacenadas en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para tener acceso a un recurso compartido de red. Por ejemplo, usar este procedimiento almacenado para quitar el permiso de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para realizar la copia de seguridad y restaurar las operaciones en un servidor que se encuentra en su propia red.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica el nombre de host del servidor de destino o dirección IP. Las credenciales para tener acceso a este servidor se quitarán de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Esto no cambia ni quitar ningún permiso en el servidor de destino real que está administrado por su propio equipo.  
  
 *target_server_name* se define como nvarchar(337).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permissions  
 Requiere **ALTER SERVER STATE** permiso.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Se produce un error si suprimir credenciales no se realiza correctamente en el nodo de Control y todos los nodos de proceso.  
  
## <a name="general-remarks"></a>Notas generales  
 Este procedimiento almacenado quita las credenciales de red de la cuenta de NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. La cuenta NetworkService ejecuta cada instancia de SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el nodo de Control y los nodos de proceso. Por ejemplo, cuando se ejecuta una operación de copia de seguridad, el nodo de Control y cada nodo de ejecución usará las credenciales de cuenta de NetworkService para tener acceso al servidor de destino.  
  
## <a name="metadata"></a>Metadatos  
 Para enumerar todas las credenciales y para comprobar que se han quitado las credenciales, utilice [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Para agregar las credenciales, utilice [sp_pdw_add_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Quitar las credenciales para realizar una copia de seguridad de base de datos  
 En el ejemplo siguiente se quita las credenciales de nombre y contraseña de usuario para tener acceso al servidor de destino que tiene una dirección IP de 10.192.147.63.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  


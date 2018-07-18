---
title: sp_pdw_add_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7f2dfe569a163b7a8268f925a5f48849778b3454
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052263"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Esto almacena las credenciales de red en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y los asocia a un servidor. Por ejemplo, utilice este procedimiento almacenado para dar [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los permisos de lectura/escritura para realizar la copia de seguridad de base de datos y las operaciones en un servidor de destino de restauración, o para crear una copia de seguridad de un certificado que se usan para TDE adecuados.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica el nombre de host del servidor de destino o dirección IP. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] tendrá acceso a este servidor mediante las credenciales de usuario y la contraseña pasadas a este procedimiento almacenado.  
  
 Para conectarse a través de la red InfiniBand, use la dirección de InfiniBand IP del servidor de destino.  
  
 *target_server_name* se define como nvarchar(337).  
  
 '*user_name*'  
 Especifica el user_name que tenga permisos para tener acceso al servidor de destino. Si ya existen credenciales para el servidor de destino, se actualizará a las nuevas credenciales.  
  
 *user_name* se define como nvarchar (513).  
  
 '*contraseña*ꞌ  
 Especifica la contraseña de *user_name*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere **ALTER SERVER STATE** permiso.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Se produce un error si agregando las credenciales no funciona en el nodo de Control y todos los nodos de proceso.  
  
## <a name="general-remarks"></a>Notas generales  
 Este procedimiento almacenado agrega credenciales de red a la cuenta de NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. La cuenta NetworkService ejecuta cada instancia de SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el nodo de Control y los nodos de proceso. Por ejemplo, cuando se ejecuta una operación de copia de seguridad, el nodo de Control y cada nodo de proceso usará las credenciales de cuenta de NetworkService para obtener la lectura y permiso de escritura en el servidor de destino.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. Agregar credenciales para realizar una copia de seguridad de base de datos  
 El ejemplo siguiente asocia las credenciales de nombre y la contraseña de usuario para el seattle\david de usuario de dominio con un servidor de destino que tiene una dirección IP de 10.172.63.255. El seattle\david usuario tiene permisos de lectura/escritura para el servidor de destino. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] almacenará estas credenciales y usarlos para leer y escribir en el servidor de destino, según sea necesario para la copia de seguridad y las operaciones de restauración.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 El comando de copia de seguridad requiere que se escriba el nombre del servidor como una dirección IP.  
  
> [!NOTE]  
>  Para realizar la copia de seguridad de base de datos a través de InfiniBand, asegúrese de usar la dirección de InfiniBand IP del servidor de copia de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  


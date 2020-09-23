---
description: DBCC SHRINKLOG (Almacenamiento de datos paralelos)
title: DBCC SHRINKLOG (Almacenamiento de datos paralelos)
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bae2ef1468110ba89d77d5f7a6360aecb324abd0
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076698"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG (Almacenamiento de datos paralelos)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

Reduce el tamaño del registro de transacciones *en el dispositivo* para la base de datos actual de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Los datos se desfragmentan con el fin de reducir el registro de transacciones. Con el paso del tiempo, el registro de transacciones de la base de datos puede fragmentarse y volverse ineficaz. Use DBCC SHRINKLOG para reducir la fragmentación y el tamaño del registro.
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  

## <a name="arguments"></a>Argumentos

SIZE = { *target_size* [ MB \| **GB** \| TB ]  } \| **DEFAULT**.  
*target_size* es el tamaño deseado del registro de transacciones, en todos los nodos de ejecución, una vez que se complete DBCC SHRINKLOG. Es un entero mayor que 0.  
El tamaño del registro se mide en megabytes (MB), gigabytes (GB) o terabytes (TB). Es el tamaño combinado del registro de transacciones en todos los nodos de ejecución.  
De forma predeterminada, DBCC SHRINKLOG reduce el registro de transacciones al tamaño de registro almacenado en los metadatos para la base de datos. El tamaño del registro en los metadatos se determina mediante el parámetro LOG_SIZE en [CREATE DATABASE &#40;Azure Synapse Analytics&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) or [ALTER DATABASE &#40;Azure Synapse Analytics&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG reduce el tamaño del registro de transacciones al valor predeterminado de tamaño cuando se especifica `SIZE=DEFAULT`, o cuando se omite la cláusula `SIZE`.
  
WITH NO_INFOMSGS  
No se muestran mensajes informativos en los resultados de DBCC SHRINKLOG.  
  
## <a name="permissions"></a>Permisos

Requiere el permiso ALTER SERVER STATE.

## <a name="general-remarks"></a>Notas generales

DBCC SHRINKLOG no cambia el tamaño de registro almacenado en los metadatos para la base de datos. Los metadatos siguen conteniendo el parámetro LOG_SIZE especificado en la instrucción CREATE DATABASE o ALTER DATABASE.
  
## <a name="examples"></a>Ejemplos

### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. Reducción del registro de transacciones al tamaño original especificado por CREATE DATABASE.  
Imagine que el registro de transacciones de la base de datos Addresses se estableció en 100 MB al crear dicha base de datos. Es decir, la instrucción CREATE DATABASE para Addresses tenía LOG_SIZE = 100 MB. Supongamos que el registro ha aumentado a 150 MB y quiere reducirlo de nuevo a 100 MB.
  
Cada una de las siguientes instrucciones intentará reducir el registro de transacciones de la base de datos Addresses al tamaño predeterminado de 100 MB. Si la reducción del registro a 100 MB producirá una pérdida de datos, DBCC SHRINKLOG reducirá el registro al menor tamaño posible, mayor que 100 MB, sin que se pierdan datos.

```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```

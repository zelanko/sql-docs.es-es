---
title: Parámetros internos de OLTP en memoria de SQL Server para SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 09/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
author: jodebrui
ms.author: jodebrui
ms.openlocfilehash: ca36f8c9716b9160b4d6eaeee26201bf03b42927
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111742"
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>Parámetros internos de OLTP en memoria de SQL Server para SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Resumen:** OLTP en memoria, denominado normalmente por su nombre en código "Hekaton", se introdujo en SQL Server 2014.
Esta eficaz tecnología permite sacar partido de grandes cantidades de memoria y varias decenas de núcleos para aumentar el rendimiento de las operaciones OLTP de 30 a 40 veces. SQL Server 2016 continúa la inversión en OLTP en memoria mediante la eliminación de muchas de las limitaciones que se encuentran en SQL Server 2014 y la mejora de los algoritmos de procesamiento interno para que OLTP en memoria pueda proporcionar mejoras todavía mayores. En este documento se describe la implementación de la tecnología OLTP en memoria de SQL Server 2016 a partir de SQL Server 2016 RTM. Al usar OLTP en memoria, las tablas se pueden declarar como "optimizadas para memoria" con el fin de habilitar las funciones de OLTP en memoria. Las tablas optimizadas en memoria son completamente transaccionales y se puede acceder a ellas mediante Transact-SQL. Los procedimientos almacenados de Transact-SQL, los desencadenadores y los UDF escalares se pueden compilar en código de máquina para obtener nuevas mejoras de rendimiento en tablas optimizadas en memoria. El motor está diseñado para obtener una alta simultaneidad sin ningún bloqueo.    
  
**Escritor:** Kalen Delaney  
  
**Revisores técnicos:** Sunil Agarwal y Jos de Bruijn  
  
**Fecha de publicación:** Junio de 2016  
  
**Se aplica a:** SQL Server 2016  
  
Para revisar el documento, descargue el documento [Parámetros internos de OLTP en memoria de SQL Server para SQL Server 2016](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf) .   

---
title: Utilizar cursores de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4bab91e4b952b808564da4d04b1ce400bf448c14
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079156"
---
# <a name="using-server-cursors"></a>Utilizar cursores de servidor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Si una aplicación ODBC establece cualquiera de los atributos de cursor ODBC en un valor distinto de los valores predeterminados, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client solicita al servidor que implemente un cursor de servidor de API del mismo tipo. El uso de cursores de servidor de API libera memoria en el cliente y reduce significativamente el tráfico de red entre el cliente y el servidor.  
  
 El hecho de que los cursores de servidor de API no admitan actualmente todas las instrucciones SQL puede representar un inconveniente. Los cursores de servidor de API no se pueden utilizar para ejecutar lo siguiente:  
  
-   Lotes o procedimientos almacenados que devuelven varios conjuntos de resultados.  
  
-   Instrucciones SELECT que contienen cláusulas COMPUTE, COMPUTE BY, FOR BROWSE o INTO.  
  
-   Una instrucción EXECUTE que haga referencia a un procedimiento almacenado remoto.  
  
 Si se está conectado a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ejecutar una instrucción con estas características utilizando un cursor de servidor hace que el cursor se convierta en un conjunto de resultados predeterminado. Si está conectado a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Cómo se implementan los cursores](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  

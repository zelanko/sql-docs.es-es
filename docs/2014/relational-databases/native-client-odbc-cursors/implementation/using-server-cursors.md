---
title: Usar cursores de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: rothja
ms.author: jroth
ms.openlocfilehash: e596af3c46849313d813ce2d7f1dab2a7425c090
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020901"
---
# <a name="using-server-cursors"></a>Utilizar cursores de servidor
  Si una aplicación ODBC establece cualquiera de los atributos de cursor de ODBC en algo distinto de los valores predeterminados, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client solicita al servidor que implemente un cursor de servidor de API del mismo tipo. El uso de cursores de servidor de API libera memoria en el cliente y reduce significativamente el tráfico de red entre el cliente y el servidor.  
  
 El hecho de que los cursores de servidor de API no admitan actualmente todas las instrucciones SQL puede representar un inconveniente. Los cursores de servidor de API no se pueden utilizar para ejecutar lo siguiente:  
  
-   Lotes o procedimientos almacenados que devuelven varios conjuntos de resultados.  
  
-   Instrucciones SELECT que contienen cláusulas COMPUTE, COMPUTE BY, FOR BROWSE o INTO.  
  
-   Una instrucción EXECUTE que haga referencia a un procedimiento almacenado remoto.  
  
 Si se está conectado a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ejecutar una instrucción con estas características utilizando un cursor de servidor hace que el cursor se convierta en un conjunto de resultados predeterminado. Si está conectado a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], produce un error.  
  
## <a name="see-also"></a>Consulte también  
 [Cómo se implementan los cursores](how-cursors-are-implemented.md)  
  
  

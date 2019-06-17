---
title: Conectarse a una base de datos SQL Azure con SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5599bbb0aa1736ba5c88904ae5152a0d73856dc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213793"
---
# <a name="connecting-to-a-azure-sql-database-using-sql-server-native-client"></a>Conexión a una Azure SQL Database con SQL Server Native Client
  Para obtener un ejemplo que muestra cómo conectarse a un [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [desarrollo: Temas de procedimientos (Microsoft Azure SQL Database)](https://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conocidos para conectarse a una SQL Database  
 A continuación se describen problemas conocidos para conectarse a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Una conexión realizada con `SQLBrowseConnect` puede rechazarse si `SQLBrowseConnect` se utiliza en etapas.  Por ejemplo, si el nombre del controlador se envía en la primera llamada, el servidor y las credenciales (usuario y contraseña) se envían en la segunda llamada y establecen la conexión, y un nombre de base de datos y un idioma en la tercera llamada.  La tercera llamada hara que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client emita una instrucción USE para cambiar las bases de datos. Sin embargo, la instrucción USE no se admite en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], que produce el siguiente error:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  

---
title: Conectarse a una base de datos SQL Azure con SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c0734537d44382e6a638b3033d4a3d822821dbf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392653"
---
# <a name="connecting-to-a-azure-sql-database-using-sql-server-native-client"></a>Conexión a una Azure SQL Database con SQL Server Native Client
  Para obtener un ejemplo que muestra cómo conectarse a un [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [desarrollo: temas de procedimientos (Microsoft Azure SQL Database)](http://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conocidos para conectarse a una SQL Database  
 A continuación se describen problemas conocidos para conectarse a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Una conexión realizada con `SQLBrowseConnect` puede rechazarse si `SQLBrowseConnect` se utiliza en etapas.  Por ejemplo, si el nombre del controlador se envía en la primera llamada, el servidor y las credenciales (usuario y contraseña) se envían en la segunda llamada y establecen la conexión, y un nombre de base de datos y un idioma en la tercera llamada.  La tercera llamada hara que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client emita una instrucción USE para cambiar las bases de datos. Sin embargo, la instrucción USE no se admite en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], que produce el siguiente error:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  

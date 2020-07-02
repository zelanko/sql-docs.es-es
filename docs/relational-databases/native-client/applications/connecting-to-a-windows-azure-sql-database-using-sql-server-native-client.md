---
title: Conectarse a Azure SQL DB
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 322ade61b0d525f914171d092cf15a2ca2d1db1d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85657561"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>Conexión a una Azure SQL Database con SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Para obtener un ejemplo que muestra cómo conectarse a [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [desarrollo: temas de procedimientos (Azure SQL Database)](https://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conocidos para conectarse a una SQL Database  
 A continuación se describen problemas conocidos para conectarse a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Se puede rechazar una conexión realizada con **SQLBrowseConnect** si se usa **SQLBrowseConnect** en fases.  Por ejemplo, si el nombre del controlador se envía en la primera llamada, el servidor y las credenciales (usuario y contraseña) se envían en la segunda llamada y establecen la conexión, y un nombre de base de datos y un idioma en la tercera llamada.  La tercera llamada hara que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client emita una instrucción USE para cambiar las bases de datos. Sin embargo, la instrucción USE no se admite en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], que produce el siguiente error:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  

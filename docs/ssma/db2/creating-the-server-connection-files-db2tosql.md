---
title: Crear los archivos de conexión de servidor (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2eca9a88060dbc64bcb523bcf3750aa8f529fd94
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="creating-the-server-connection-files-db2tosql"></a>Crear los archivos de conexión de servidor (DB2ToSQL)
Información del servidor puede especificarse en la sección de servidores del archivo de script o en un archivo de conexión de servidor independiente. El parámetro de línea de comandos para el archivo de conexión de servidor es, `-c <serverconnectionfile>`. Si el mismo identificador de servidor se encuentra en el archivo de script y el archivo de conexión de servidor, se considera la definición del servidor en el archivo de script.  
  
**Ejemplo: 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<db2 name="<source-server-unique-name>">  
  
    <standard-mode>  
  
      <connection-provider value ="OleDB Provider"/>  
  
      <!-- Defines server manager to connect.  
  
              Available manager attribute values  
  
              • zOs      - upgrades the project (default)  
  
              • LUW       - displays an error and halts the execution-->  
  
      <database-manager value="$Db2Manager$"/>  
  
      <server-name value="$Db2HostName$" />  
  
      <port value="$Db2Port$" />  
  
      <initial-catalog value="$Db2Instance$" />  
  
      <user-id value="$Db2UserName$" />  
  
      <password value="$Db2Password$"/>  
  
    </standard-mode>  
  
</db2>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la utilización de la consola es [ejecutando la consola SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola de SSMA](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  

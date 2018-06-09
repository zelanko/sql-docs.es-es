---
title: Crear los archivos de conexión de servidor (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c6e46ab77966f6f6f392de64c076c4560c7885ab
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773631"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Crear el servidor de archivos de conexión (AccessToSQL)
Información del servidor se pueden especificar en la sección de servidores del archivo de script. Información del servidor también puede especificarse en un archivo de conexión de servidor independiente. El parámetro de línea de comandos para el archivo de conexión de servidor es `-c <serverconnectionfile>`. Si el mismo identificador de servidor se encuentra en el script y el servidor de archivos de conexión, se considera que la definición del servidor en el archivo de script.  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>Validación del archivo de conexión de servidor  
El usuario puede validar fácilmente su archivo de conexión de servidor con el archivo de definición de esquema **'A2SSConsoleScriptServersSchema.xsd'** disponible en la carpeta 'Esquemas'.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la utilización de la consola es [ejecutando la consola SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecutar la consola SSMA (Access)](http://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  

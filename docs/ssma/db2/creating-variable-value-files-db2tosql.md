---
title: Crear archivos de valor de la Variable (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 87cd293fcfa801499c7ef3cad583b05ff2ecf2a1
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774591"
---
# <a name="creating-variable-value-files-db2tosql"></a>Crear archivos de valor de la Variable (DB2ToSQL)
Archivo de valores de variable es un archivo XML que contiene los valores de parámetro de comandos como el nombre del servidor de origen o de destino que cambian con frecuencia de la migración de un servidor a otro. Cuando se produce un gran número de migraciones de base de datos, varios archivos de variable para almacenar el valor de cada servidor de origen se creará y se hace referencia en un archivo de script maestra con la **– v** cambiar en la línea de comandos. Esto ayuda a mantener los valores estáticos en unos pocos archivos de script con los valores de variables en varios archivos de variable.  
  
> [!NOTE]  
> 1.  Los nombres de variable son el prefijo y sufijo con un símbolo $ (dólar). Si las variables no se asignan un valor en el archivo de valor de la variable, se producirá un error durante el análisis del archivo de script resultante en demora el proceso de ejecución de la consola.  
> 2.  The escape character for **$** is **$$**. Si el valor de un valor de variable o estático de un parámetro contiene **$** símbolos (dólar), a continuación, **$$** debe especificarse para tratarlo como un carácter en lugar de una variable.  
> 3.  Por motivos de mantenimiento, las variables pueden declararse dentro de `‘variable-group’` variables definidas por elementos de una separación lógica del usuario.  Uso de este elemento no es obligatorio.  
  
**Ejemplos:**  
  
**Ejemplo 1:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Ejemplo 2:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la utilización de la consola es [crear los archivos de conexión de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>Vea también  
[Creación de archivos de conexión del servidor](http://msdn.microsoft.com/en-us/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  

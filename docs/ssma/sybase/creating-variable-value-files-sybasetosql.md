---
title: Creación de archivos de valor Variable (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7afced10f0be71310edc4b42ea0158ca996f3aa3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514951"
---
# <a name="creating-variable-value-files-sybasetosql"></a>Creación de archivos de valor variable (SybaseToSQL)
Archivo de valores de variable es un archivo XML que contiene los valores de parámetro de comandos, como el nombre del servidor de origen o destino que cambian con frecuencia de la migración de un servidor a otro. Cuando se produce un gran número de migraciones de base de datos, se creará varios archivos de variable para almacenar el valor de cada servidor de origen y se hace referencia en un archivo de script maestro con el **- v** cambiar en la línea de comandos. Esto ayuda a mantener los valores estáticos en unos pocos archivos de script con los valores de variables en varios archivos de variable.  
  
> [!NOTE]  
> 1.  Los nombres de variable son el prefijo y sufijo con un símbolo $ (dólar). Si las variables no se asignan un valor en el archivo de valor de la variable, se producirá un error durante el análisis del archivo de script, lo que detienen el proceso de ejecución de la consola.  
> 2.  El carácter de escape para **$** es **$$**. Si el valor de un valor estático o variable de un parámetro contiene **$** símbolos (dólar), a continuación, **$$** debe especificarse para tratarlo como un carácter en lugar de una variable.  
> 3.  Para fines de mantenimiento, se pueden declarar variables dentro `'variable-group'` elementos para una separación lógica del usuario definen las variables.  Uso de este elemento no es obligatorio.  
  
**Ejemplos:**  
  
**Ejemplo 1:**  
  
```xml  
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
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
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
  
## <a name="variable-value-file-validation"></a>Validación de archivos de valor de la variable  
El usuario puede validar fácilmente su archivo de valor de la variable en el archivo de definición de esquema **ConsoleScriptVariablesSchema.xsd** disponible en la carpeta "Esquemas".  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en el funcionamiento de la consola es [crear los archivos de conexión de servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Creación de los archivos del servidor (Sybasetosql)](https://msdn.microsoft.com/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  

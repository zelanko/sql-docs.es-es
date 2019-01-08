---
title: Creación de archivos de valor Variable (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 73919295dbd53cbaaca3847d5be119e5fe2d0bb7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530152"
---
# <a name="creating-variable-value-files-mysqltosql"></a>Creación de archivos de valor variable (MySQLToSQL)
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
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
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
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
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
El usuario puede validar fácilmente su archivo de valor de la variable en el archivo de definición de esquema **'ConsoleScriptVariablesSchema.xsd'** disponible en la carpeta "Esquemas".  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en el funcionamiento de la consola es [crear los archivos de conexión de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Creación de los archivos de conexión de servidor (MySQL)](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  

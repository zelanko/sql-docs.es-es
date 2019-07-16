---
title: Creación de archivos de valor Variable (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 051ded7d675f81998718b858c71488ba968ec680
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006595"
---
# <a name="creating-variable-value-files-accesstosql"></a>Creación de archivos de valor Variable (AccessToSQL)
Un archivo de valores de Variable es un archivo XML que contiene los valores de parámetro de comandos (por ejemplo, el nombre de servidor de origen o destino) que cambian con frecuencia a través de migraciones de servidor. Cuando se produce un gran número de migraciones de base de datos, se crean varios archivos de variable para almacenar el valor de cada servidor de origen y se hace referencia en un archivo de script maestro con el **- v** cambiar en la línea de comandos. Este comportamiento ayuda a mantener los valores estáticos en unos pocos archivos de script con los valores de variables en varios archivos de variable.  
  
> [!NOTE]  
> -  Los nombres de variable son el prefijo y sufijo con un símbolo $ (dólar). Si una variable no se asigna un valor en el archivo de valor de la variable, producirá un error durante el análisis del archivo de script, lo detienen el proceso de ejecución de la consola.  
> -  El carácter de escape para **$** es **$$** . Si el valor de un valor estático o variable de un parámetro contiene un **$** símbolos (dólar), a continuación, **$$** debe especificarse para tratarlo como un carácter en lugar de una variable.  
> -  Para fines de mantenimiento, se pueden declarar variables dentro `'variable-group'` elementos para una separación lógica de las variables definidas por el usuario.  Uso de este elemento no es obligatorio.  
  
**Ejemplos:**  
  
**Ejemplo 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**Ejemplo 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Validación de archivos de valor de la variable  
El usuario puede validar fácilmente su archivo de valor de la variable en el archivo de definición de esquema **ConsoleScriptVariablesSchema.xsd** disponible en la carpeta "Esquemas".  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en el funcionamiento de la consola es [crear los archivos de conexión de servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Creación de los archivos de conexión de servidor (acceso)](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
